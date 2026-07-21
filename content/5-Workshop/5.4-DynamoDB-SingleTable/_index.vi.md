---
title: "Thiết kế DynamoDB Single-Table & DynamoDB Streams"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4 </b> "
---

# Thiết kế DynamoDB Single-Table & DynamoDB Streams CDC

Trong mô hình SaaS Đa doanh nghiệp (Multi-tenant), việc lựa chọn và thiết kế kiến trúc cơ sở dữ liệu đóng vai trò quyết định đến **chi phí hạ tầng**, **tốc độ truy vấn** và **khả năng cô lập dữ liệu (Tenant Data Isolation)**.

Trong phần này, bạn sẽ tìm hiểu cấu trúc **Single-Table Design** trên Amazon DynamoDB và cơ chế bắt sự kiện biến động dữ liệu **DynamoDB Streams (Change Data Capture)**.

---

### 1. Phân tích Cấu trúc Single-Table Design

Thay vì tạo nhiều bảng riêng lẻ cho từng doanh nghiệp hoặc từng thực thể (Users, Attendance, Tenants, Subscriptions), hệ thống lưu toàn bộ vào **1 Bảng duy nhất (`smart-attendance-database`)** với cấu trúc HASH (`PK`) & RANGE (`SK`):

| Entity (Thực thể) | Partition Key (`PK`) | Sort Key (`SK`) | Attributes (Thuộc tính đính kèm) |
| :--- | :--- | :--- | :--- |
| **Tenant Record** | `TENANT#<tenantId>` | `METADATA` | `tenantName`, `plan`, `status`, `createdAt` |
| **User Profile** | `TENANT#<tenantId>` | `USER#<userId>` | `email`, `fullName`, `role`, `department` |
| **Attendance Log** | `TENANT#<tenantId>` | `ATTENDANCE#<userId>#<timestamp>` | `checkInTime`, `checkOutTime`, `status`, `location` |
| **Subscription Billing**| `TENANT#<tenantId>` | `SUB#<billingId>` | `planTier`, `amount`, `paymentStatus`, `expiryDate` |

#### Nguyên tắc cô lập dữ liệu tuyệt đối (Tenant Isolation)
* Mỗi truy vấn (Query) của hàm Lambda **bắt buộc** truyền Partition Key có dạng `TENANT#<tenantId>`.
* Giúp ngăn chặn 100% rủi ro truy cập nhầm dữ liệu giữa các công ty khác nhau (Cross-tenant data leak).

---

### 2. Kiểm tra DynamoDB Table trên AWS Console

1. Mở [Amazon DynamoDB Console](https://console.aws.amazon.com/dynamodbv2/).
2. Chọn mục **Tables** -> Chọn bảng `smart-attendance-database`.
3. Kiểm tra mục **Overview**:
   * **Read/Write capacity mode:** `On-Demand` (Tự động mở rộng theo lưu lượng thực tế).
   * **Encryption:** `KMS` (Mã hóa bằng Customer Managed Key `DataKMSKey`).
   * **Point-in-time recovery (PITR):** `ENABLED`.
   * **DynamoDB Streams:** `ENABLED (NEW_AND_OLD_IMAGES)`.

---

### 3. Tích hợp EventBridge Pipe từ DynamoDB Streams

Để truyền sự kiện biến động dữ liệu (CDC) sang các dịch vụ xử lý khác mà không làm tăng độ trễ hàm Check-in Lambda, hệ thống sử dụng **AWS EventBridge Pipes**:

```yaml
DdbToEventBridgePipe:
  Type: AWS::Pipes::Pipe
  Properties:
    Name: smart-attendance-ddb-stream-pipe
    Source: !GetAtt SaaSAttendanceTable.StreamArn
    Target: !Sub 'arn:aws:events:${AWS::Region}:${AWS::AccountId}:event-bus/default'
```

* Khi một lượt check-in mới được ghi vào DynamoDB, **DynamoDB Streams** tự động tạo ra một thay đổi dữ liệu (Stream Record).
* **EventBridge Pipe** đọc các bản ghi này và đẩy thẳng sự kiện `AttendanceCreated` sang **EventBridge Event Bus** để kích hoạt các tiến trình gửi email hoặc bắn Webhook thời gian thực.
