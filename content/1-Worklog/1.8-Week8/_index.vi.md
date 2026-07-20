---
title: "Worklog Tuần 8"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8

* Hiểu triết lý thiết kế ứng dụng Không máy chủ (Serverless), Kiến trúc hướng sự kiện (Event-Driven Architecture) trên AWS.
* Làm chủ AWS Lambda (Môi trường thực thi, Execution Role, Layers, Cấu hình bộ nhớ/Timeout & Các nguồn kích hoạt Triggers).
* Xây dựng Serverless APIs với Amazon API Gateway, quản lý luồng công việc phức tạp bằng AWS Step Functions & công cụ AWS SAM.

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Tìm hiểu kiến thức cốt lõi AWS Lambda: <br>&emsp; + Mô hình xử lý theo sự kiện (Event-driven model), Môi trường thực thi & Giới hạn xử lý đồng thời (Concurrency limits) <br>&emsp; + IAM Execution Roles & Phân quyền truy cập tài nguyên Resource-based policies <br>&emsp; + Sử dụng Lambda Layers để tái sử dụng mã nguồn và thư viện chung | 22/06/2026 | 22/06/2026 | <https://000022.awsstudygroup.com> |
| 3 | - Tìm hiểu Amazon API Gateway: <br>&emsp; + So sánh REST API, HTTP API và WebSocket API <br>&emsp; + Cơ chế Tích hợp Lambda Proxy, Kiểm tra tính hợp lệ dữ liệu (Request Validation) & Biến đổi dữ liệu <br>&emsp; + Các giải pháp xác thực: Cognito User Pools đối chiếu với Custom Lambda Authorizers | 23/06/2026 | 23/06/2026 | <https://000066.awsstudygroup.com> <br> <https://000141.awsstudygroup.com> |
| 4 | - **Thực hành:** <br>&emsp; + Lập trình các hàm Lambda xử lý nghiệp vụ bằng Node.js/Python <br>&emsp; + Tạo REST API trên API Gateway định nghĩa các điểm truy cập CRUD kết nối với Lambda & DynamoDB <br>&emsp; + Cấu hình CORS & API Key / Thử nghiệm kiểm thử gọi API từ Postman | 24/06/2026 | 24/06/2026 | <https://000066.awsstudygroup.com> <br> <https://000133.awsstudygroup.com/> |
| 5 | - Tìm hiểu AWS Step Functions & AWS SAM (Serverless Application Model): <br>&emsp; + Máy trạng thái State Machines (Quy trình Standard vs Express), Các luồng điều kiện (Choice States) & Xử lý ngoại lệ lỗi <br>&emsp; + Cú pháp tài liệu mẫu AWS SAM (`template.yaml`) & Bộ lệnh SAM CLI (`sam build`, `sam local`, `sam deploy`) | 25/06/2026 | 25/06/2026 | <https://000047.awsstudygroup.com> <br> <https://000080.awsstudygroup.com/> |
| 6 | - **Thực hành:** <br>&emsp; + Xây dựng quy trình xử lý đơn hàng đa bước phức tạp bằng Step Functions điều phối nhiều hàm Lambda <br>&emsp; + Đóng gói, kiểm thử cục bộ và triển khai tự động toàn bộ ứng dụng Serverless bằng AWS SAM | 26/06/2026 | 26/06/2026 | <https://000047.awsstudygroup.com> <br> <https://000080.awsstudygroup.com/> |

### Kết quả đạt được tuần 8

* Làm chủ lập trình và cấu hình tối ưu các hàm AWS Lambda theo mô hình Hướng sự kiện (Event-Driven).
* Triển khai hệ thống Serverless REST API hoàn chỉnh tích hợp API Gateway, Lambda và DynamoDB.
* Quản lý các quy trình nghiệp vụ nhiều bước phức tạp bằng AWS Step Functions với khả năng xử lý ngoại lệ tự động.
* Đóng gói, kiểm thử cục bộ và triển khai ứng dụng Serverless bằng công cụ chuẩn AWS SAM.
