---
title: "Kiểm thử End-to-End & Dọn dẹp Tài nguyên"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.7 </b> "
---

# Kiểm thử End-to-End & Dọn dẹp Tài nguyên

Chúc mừng bạn đã hoàn thành việc xây dựng và triển khai toàn bộ hệ thống **Smart Attendance SaaS Platform**! Trong phần cuối cùng này, bạn sẽ tiến hành thử nghiệm toàn bộ quy trình nghiệp vụ (End-to-End Testing) và thực hiện dọn dẹp các tài nguyên đã tạo trên AWS để tránh phát sinh chi phí ngoài ý muốn.

---

### 1. Kịch bản Kiểm thử End-to-End (E2E Test)

Hãy thực hiện kiểm thử theo 5 kịch bản thực tế sau trên ứng dụng Web:

#### Kịch bản 1: Đăng ký Doanh nghiệp mới & Đăng nhập (Multi-tenant Auth)

1. Mở trang Web App trên đường dẫn CloudFront CDN Domain.
2. Chọn **Đăng ký Doanh nghiệp (Register Tenant)**. Nhập thông tin Công ty A (`tenantId`: `tenant-company-a`), Email và Mật khẩu.
3. Kiểm tra mã OTP xác thực gửi về Email và hoàn tất xác thực.
4. Đăng nhập hệ thống với tài khoản Admin vừa tạo. Màn hình Dashboard quản trị hiển thị chính xác context `tenantId`.

#### Kịch bản 2: Điểm danh Nhân viên (Employee Check-in / Check-out)

1. Tạo 1 tài khoản Nhân viên (`user-employee-1`) gán vào `tenant-company-a`.
2. Đăng nhập tài khoản Nhân viên trên thiết bị di động hoặc giả lập trình duyệt.
3. Bấm nút **Check-in (Chấm công vào)** -> Hệ thống gửi request mang JWT Token lên API Gateway -> Hàm Lambda `CheckInFunction` ghi nhận dữ liệu thành công dưới 200ms.
4. Bấm nút **Check-out (Chấm công ra)** -> Hệ thống cập nhật thời gian ra ca vào DynamoDB.

#### Kịch bản 3: Truy vấn Lịch sử Chấm công (DynamoDB Query)

1. Mở mục **Lịch sử Chấm công (History)**.
2. Hệ thống thực hiện Query DynamoDB theo Partition Key `TENANT#tenant-company-a` và trả về danh sách điểm danh theo thời gian thực dưới 50ms.

#### Kịch bản 4: Xuất Báo cáo Excel/PDF (Step Functions & SES)

1. Trên giao diện Admin, chọn **Xuất Báo Cáo Tháng** -> Bấm nút **Tạo Báo Cáo**.
2. Giao diện hiển thị thông báo "Yêu cầu đang được xử lý".
3. Mở AWS Step Functions Console để quan sát Express State Machine khởi chạy và tạo file báo cáo.
4. Kiểm tra hộp thư Email nhận được mail tự động từ **Amazon SES** chứa liên kết tải file báo cáo Excel/PDF an toàn từ S3 Bucket.

#### Kịch bản 5: Thanh toán B2B & Webhook

1. Đăng nhập Admin -> Chọn gói cước Pro -> Bấm **Thanh toán**.
2. Giả lập cổng thanh toán gửi Webhook thông báo thành công về URL `/billing/webhook`.
3. Hàm `WebhookFunction` xác thực chữ ký Webhook qua **AWS Secrets Manager** và cập nhật trạng thái doanh nghiệp thành `ACTIVE` trong DynamoDB.

---

### 2. Dọn dẹp Tài nguyên AWS (Cleanup)

Để tránh bị tính phí hạ tầng sau khi kết thúc bài thực hành, hãy làm theo các bước sau để xóa toàn bộ tài nguyên AWS:

#### Bước 1: Xóa các file trong S3 Buckets

S3 Buckets chứa file không thể bị xóa trực tiếp từ CloudFormation. Hãy dọn dẹp nội dung buckets trước bằng AWS CLI:

```bash
# 1. Xóa nội dung S3 Report Bucket
aws s3 rm s3://saas-attendance-reports-<AWS_ACCOUNT_ID>-<REGION> --recursive

# 2. Xóa nội dung S3 SPA Hosting Bucket
aws s3 rm s3://smart-attendance-spa-hosting-<AWS_ACCOUNT_ID> --recursive
```

#### Bước 2: Xóa CloudFormation Stack bằng AWS SAM

Di chuyển vào thư mục `backend/` và thực hiện lệnh xóa stack:

```bash
cd backend
sam delete
```

Xác nhận lệnh xóa:

```text
Are you sure you want to delete the stack smart-attendance-backend in region us-east-1? [y/N]: y
Are you sure you want to delete the folder smart-attendance-backend in S3? [y/N]: y
```

Chờ khoảng 3–5 phút để CloudFormation tự động hủy toàn bộ 18+ tài nguyên AWS (Cognito, API Gateway, Lambda, DynamoDB, Step Functions, SQS, SES, KMS Keys).

---

### Kết luận

Chúc mừng bạn đã hoàn thành xuất sắc bài thực hành **Smart Attendance SaaS Platform Workshop**! Bạn đã nắm vững tư duy kiến trúc **AWS Serverless** và kỹ năng thực tế xây dựng ứng dụng SaaS quy mô lớn trên nền tảng đám mây AWS.
