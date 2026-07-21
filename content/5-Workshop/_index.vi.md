---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Xây dựng Nền tảng Chấm công Thông minh Multi-Tenant với AWS Serverless Architecture

#### Tổng quan

Trong chuỗi bài thực hành Workshop này, bạn sẽ từng bước xây dựng và triển khai một nền tảng **Smart Attendance SaaS Platform** hoàn chỉnh dành cho mô hình đa doanh nghiệp (Multi-tenant) dựa trên kiến trúc **AWS Serverless Optimized Pro**.

Bạn sẽ trực tiếp thao tác đóng gói hạ tầng bằng mã với **AWS SAM (Serverless Application Model)**, cấu hình bảo mật xác thực với **Amazon Cognito User Pool**, làm việc với **Amazon DynamoDB (Single-Table Design)** cô lập dữ liệu theo `tenantId`, triển khai **AWS Step Functions Express Workflow** và **Amazon SQS / SES** xử lý báo cáo bất đồng bộ, phân phối ứng dụng React SPA qua **Amazon S3** và **Amazon CloudFront CDN**.

#### Nội dung thực hành

1. [Tổng quan về workshop](5.1-Workshop-overview/)
2. [Chuẩn bị môi trường](5.2-Prerequiste/)
3. [Triển khai Backend Serverless với AWS SAM](5.3-Deploy-Backend/)
4. [Cấu hình DynamoDB Single-Table & DynamoDB Streams](5.4-DynamoDB-SingleTable/)
5. [Xây dựng Workflow Xuất Báo cáo Bất đồng bộ](5.5-Async-Reporting/)
6. [Triển khai React SPA Frontend & CloudFront CDN](5.6-Frontend-CloudFront/)
7. [Kiểm thử End-to-End & Dọn dẹp Tài nguyên](5.7-Testing-Cleanup/)
