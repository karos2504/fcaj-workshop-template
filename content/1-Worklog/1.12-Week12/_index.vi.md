---
title: "Worklog Tuần 12"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.12. </b> "
---

### Mục tiêu tuần 12

* Thiết kế và triển khai Giai đoạn 1 dự án Capstone: **SaaS Timekeeping Platform (Hệ thống Điểm danh & Chấm công Multi-Tenant theo kiến trúc AWS Serverless)** dựa trên sơ đồ thiết kế kiến trúc chuẩn `Demo.drawio`.
* Lập trình mã nguồn hạ tầng tự động hóa bằng AWS CDK (TypeScript/Python): Dựng VPC Private Subnets, CloudFront CDN, Route 53, AWS WAF v2, Amazon Cognito Auth & API Gateway HTTP API v2.
* Xây dựng các lớp dịch vụ cốt lõi: DynamoDB Single-Table Design (phân lập dữ liệu multi-tenant), tập hợp các hàm AWS Lambda nghiệp vụ (Check-in, Check-out, Attendance, Admin, Subscription), AWS Step Functions Workflow cho quy trình xuất báo cáo và Event-Driven Notification Bus.

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - **Phân tích Kiến trúc & Thiết kế Giải pháp:** <br>&emsp; + Phân tích sơ đồ kiến trúc `Demo.drawio` cho dự án **SaaS Timekeeping Platform** <br>&emsp; + Thiết kế mô hình Multi-Tenancy với cơ chế phân lập dữ liệu theo Partition Key (`tenantId`) trên DynamoDB <br>&emsp; + Xây dựng ma trận phân quyền RBAC (Role-Based Access Control) & Ước tính chi phí vận hành bằng AWS Pricing Calculator | 20/07/2026 | 20/07/2026 | <https://cloudjourney.awsstudygroup.com> |
| 3 | - **Triển khai Hạ tầng IaC & Edge/Auth Layer (AWS CDK):** <br>&emsp; + Khởi tạo dự án AWS CDK dựng VPC Private Subnets, Amazon Route 53 & Amazon CloudFront CDN (tích hợp AWS WAF v2 & AWS Shield) <br>&emsp; + Cấu hình Amazon Cognito User Pools chứa Custom Claims (`{tenantId, role, userId}`) <br>&emsp; + Dựng Amazon API Gateway (HTTP API v2) tích hợp JWT Authorizer & Custom Header Verification | 21/07/2026 | 21/07/2026 | <https://000076.awsstudygroup.com> <br> <https://000141.awsstudygroup.com> |
| 4 | - **Triển khai Data Layer & Core Compute (Lambda Functions):** <br>&emsp; + Khởi tạo **Amazon DynamoDB Single-Table Design** (bảng `Attendance`, `Users`, `Tenants`) tích hợp **DynamoDB Streams (CDC)** và mã hóa dữ liệu với **AWS KMS CMK** <br>&emsp; + Viết mã nguồn cho các hàm Lambda nghiệp vụ: `Lambda Check-in` (Clock-In), `Lambda Check-out` (Clock-Out), `Lambda Attendance` (Query & Summary) và `Lambda Admin` <br>&emsp; + Lưu trữ API Keys & DB Credentials trên **AWS Secrets Manager** với cơ chế Auto Rotation | 22/07/2026 | 22/07/2026 | <https://000060.awsstudygroup.com> <br> <https://000096.awsstudygroup.com> |
| 5 | - **Triển khai Workflow Engine & Event Notification Layer:** <br>&emsp; + Xây dựng quy trình xuất báo cáo chấm công bất đồng bộ với **AWS Step Functions Engine** (Standard Workflow) & **Amazon SQS Queue + DLQ** <br>&emsp; + Khởi tạo **Amazon S3** (Intelligent-Tiering, mã hóa KMS) lưu trữ file báo cáo (PDF, Excel, CSV) <br>&emsp; + Cấu hình luồng sự kiện: **DynamoDB Streams -> EventBridge Event Bus -> SQS Email Queue -> Lambda Email Worker -> Amazon SES** gửi email báo cáo & cảnh báo tự động | 23/07/2026 | 23/07/2026 | <https://000047.awsstudygroup.com> <br> <https://000077.awsstudygroup.com> |
| 6 | - **Tích hợp Webhook & Thiết lập DevOps CI/CD Pipeline:** <br>&emsp; + Cấu hình `Lambda Subscription` & `Lambda Webhook` tiếp nhận phản hồi thanh toán B2B Subscription từ Payment Gateway <br>&emsp; + Khởi tạo **AWS CodePipeline** & **AWS CodeBuild** tự động hóa quy trình Build, Test & Scan an toàn thông tin mã nguồn với **Amazon Inspector** | 24/07/2026 | 24/07/2026 | <https://000152.awsstudygroup.com> |

### Kết quả đạt được tuần 12

* Thiết kế và triển khai hoàn chỉnh hạ tầng Serverless Multi-Tenant cho ứng dụng SaaS Timekeeping Platform theo sơ đồ `Demo.drawio`.
* Làm chủ kỹ thuật DynamoDB Single-Table Design kết hợp DynamoDB Streams để xử lý Change Data Capture (CDC).
* Xây dựng luồng xuất báo cáo bất đồng bộ chịu tải cao nhờ AWS Step Functions kết hợp Amazon SQS.
* Tự động hóa hoàn toàn việc khởi tạo hạ tầng đa tầng bằng AWS CDK v2 và kết nối CI/CD Pipeline trên AWS.
