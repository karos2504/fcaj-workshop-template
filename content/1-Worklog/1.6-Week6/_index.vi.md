---
title: "Worklog Tuần 6"
date: 2026-06-08
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6

* Hiểu triết lý thiết kế ứng dụng Không máy chủ (Serverless) và Kiến trúc hướng sự kiện (Event-Driven Architecture) trên AWS.
* Làm chủ AWS Lambda (Môi trường thực thi, Execution Role, Layers & Triggers) và xác thực người dùng với Amazon Cognito.
* Xây dựng Serverless APIs với Amazon API Gateway, quản lý luồng công việc phức tạp bằng AWS Step Functions & công cụ AWS SAM CLI.

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - **Serverless Automation with AWS Lambda:** <br>&emsp; + Mô hình xử lý Event-driven model, Execution Environment & Concurrency limits <br>&emsp; + IAM Execution Roles & Resource-based policies <br>&emsp; + Sử dụng Lambda Layers tái sử dụng thư viện dùng chung | 08/06/2026 | 08/06/2026 | <https://000022.awsstudygroup.com> |
| 3 | - **Building Serverless APIs with Amazon API Gateway:** <br>&emsp; + So sánh REST API vs HTTP API vs WebSocket API <br>&emsp; + Cơ chế Tích hợp Lambda Proxy, Request Validation & cấu hình CORS <br>&emsp; + Xác thực người dùng qua Amazon Cognito User Pools | 09/06/2026 | 09/06/2026 | <https://000066.awsstudygroup.com> <br> <https://000141.awsstudygroup.com> |
| 4 | - **Thực hành:** <br>&emsp; + Lập trình các hàm Lambda xử lý nghiệp vụ bằng Node.js/Python <br>&emsp; + Tạo REST API trên API Gateway kết nối với Lambda & DynamoDB <br>&emsp; + Thử nghiệm kiểm thử gọi API từ Postman và kiểm tra phân quyền JWT Token | 10/06/2026 | 10/06/2026 | <https://000066.awsstudygroup.com> |
| 5 | - **Workflow Orchestration with AWS Step Functions:** <br>&emsp; + Máy trạng thái State Machines (Standard vs Express Workflow) <br>&emsp; + Rẽ nhánh điều kiện (Choice States), song song (Parallel States) & xử lý lỗi (Catch/Retry) <br>&emsp; + Giới thiệu chuẩn cấu trúc AWS SAM (`template.yaml`) | 11/06/2026 | 11/06/2026 | <https://000047.awsstudygroup.com> <br> <https://000080.awsstudygroup.com/> |
| 6 | - **Thực hành Serverless Application Model (AWS SAM):** <br>&emsp; + Xây dựng quy trình xử lý bất đồng bộ phức tạp điều phối nhiều hàm Lambda qua Step Functions <br>&emsp; + Sử dụng SAM CLI (`sam build`, `sam local`, `sam deploy`) đóng gói và triển khai ứng dụng Serverless tự động | 12/06/2026 | 12/06/2026 | <https://000047.awsstudygroup.com> <br> <https://000080.awsstudygroup.com/> |

### Kết quả đạt được tuần 6

* Thành thạo viết và tối ưu hóa các hàm AWS Lambda theo mô hình Event-Driven.
* Triển khai hệ thống Serverless REST API hoàn chỉnh tích hợp API Gateway, Lambda, Cognito và DynamoDB.
* Quản lý quy trình nghiệp vụ nhiều bước phức tạp bằng AWS Step Functions với khả năng tự động khôi phục khi gặp lỗi.
* Đóng gói, kiểm thử cục bộ và triển khai tự động toàn bộ ứng dụng Serverless chuẩn hóa bằng AWS SAM CLI.

