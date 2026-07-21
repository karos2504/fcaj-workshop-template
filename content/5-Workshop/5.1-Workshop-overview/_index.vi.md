---
title: "Tổng quan về workshop"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1 </b> "
---

# Tổng quan về Workshop Smart Attendance SaaS Platform

### Giới thiệu bài lab

Trong bài lab này, bạn sẽ được tìm hiểu bức tranh tổng thể về bài toán xây dựng phần mềm chấm công dạng dịch vụ (**SaaS - Software-as-a-Service**) hỗ trợ đa doanh nghiệp (Multi-tenant) chạy 100% trên đám mây **AWS Serverless**.

### Sơ đồ Kiến trúc Hệ thống

Dưới đây là mô hình kiến trúc hạ tầng Serverless hoàn chỉnh mà bạn sẽ triển khai trong toàn bộ bài workshop:

![Smart Attendance SaaS Architecture](/images/5-Workshop/5.1-Workshop-overview/platform_architecture.png)

### Các mục tiêu đạt được sau bài lab

Sau khi hoàn thành chuỗi bài lab này, bạn sẽ làm chủ các kỹ năng thực tế:

1. **Infrastructure as Code (IaC):** Sử dụng **AWS SAM (Serverless Application Model)** để định nghĩa và quản lý tự động toàn bộ tài nguyên AWS qua mã lệnh (`template.yaml`).
2. **Xác thực Đa doanh nghiệp (Multi-Tenant Auth):** Thiết lập **Amazon Cognito User Pool** chứa Custom Attributes (`tenantId`, `role`) và kết nối với **Amazon API Gateway HTTP API v2** thông qua Cognito JWT Authorizer.
3. **Thiết kế Cơ sở dữ liệu NoSQL tối ưu:** Xây dựng mô hình **Single-Table Design** trên **Amazon DynamoDB**, mã hóa dữ liệu với **AWS KMS CMK**, bật tính năng **DynamoDB Streams** bắt sự kiện biến động (CDC).
4. **Xử lý sự kiện bất đồng bộ:** Tích hợp **EventBridge Pipe**, **AWS Step Functions Express Workflow**, **Amazon SQS Queue** và **Amazon SES** để tạo và gửi file báo cáo điểm danh Excel/PDF tự động tới email người dùng.
5. **Phân phối Web SPA & Bảo mật Edge:** Triển khai Single Page Application (React + Vite) lên **Amazon S3 Bucket**, phân phối toàn cầu qua **Amazon CloudFront CDN** bảo mật bằng Custom Verification Header (`x-origin-verify`).

### Thời lượng ước tính

* **Thời gian thực hiện:** 60 - 90 phút.
* **Mức độ:** Intermediate to Advanced (Trung bình - Nâng cao).
