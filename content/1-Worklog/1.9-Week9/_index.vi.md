---
title: "Worklog Tuần 9"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9

* Hiểu các khái niệm Container hóa (Containerization) với Docker (Dockerfile, Images, Containers, Multi-stage builds).
* Quản lý kho lưu trữ Container Images riêng tư với Amazon Elastic Container Registry (ECR).
* Điều phối container nâng cao trên Amazon ECS (Elastic Container Service) với AWS Fargate & Tổng quan về Amazon EKS (Elastic Kubernetes Service).

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Tìm hiểu kiến thức cốt lõi Docker: <br>&emsp; + Kiến trúc Docker, Hình ảnh (Images), Container & Kho lưu trữ (Registries) <br>&emsp; + Cú pháp Dockerfile chuẩn hóa & Kỹ thuật xây dựng nhiều giai đoạn (Multi-stage builds) giúp tối ưu dung lượng image <br>&emsp; + Mạng trong Docker (Docker Networking) & Cấu hình lưu trữ dữ liệu bền vững (Volumes) | 29/06/2026 | 29/06/2026 | <https://000015.awsstudygroup.com> |
| 3 | - **Thực hành:** <br>&emsp; + Viết Dockerfile tối ưu cho ứng dụng Web (Node.js/Python/Go) <br>&emsp; + Khởi tạo, chạy và gỡ lỗi (debug) containers ở môi trường máy cục bộ <br>&emsp; + Tạo kho lưu trữ Amazon ECR Private Repository, xác thực qua AWS CLI và tải (push) image lên ECR | 30/06/2026 | 30/06/2026 | <https://000015.awsstudygroup.com> <br> <https://000067.awsstudygroup.com> |
| 4 | - Tìm hiểu kiến trúc Amazon ECS: <br>&emsp; + Định nghĩa nhiệm vụ Task Definitions (Cấu hình CPU, Bộ nhớ, Biến môi trường, Nhật ký Logs) <br>&emsp; + Các thành phần ECS Services, Clusters & Phương thức triển khai Launch Types (Máy chủ EC2 đối chiếu với Serverless Fargate) <br>&emsp; + Tự động mở rộng ECS Service Auto Scaling & Tích hợp bộ cân bằng tải Application Load Balancer | 01/07/2026 | 01/07/2026 | <https://000016.awsstudygroup.com> <br> <https://000067.awsstudygroup.com> |
| 5 | - **Thực hành:** <br>&emsp; + Khởi tạo cụm máy chủ ECS Cluster chạy theo mô hình Serverless AWS Fargate <br>&emsp; + Tạo Task Definition kéo image từ ECR & Khởi tạo ECS Service tích hợp với ALB <br>&emsp; + Kiểm tra khả năng mở rộng tự động (Auto Scaling) và quy trình cập nhật cuộn không gián đoạn (Rolling update deployment) | 02/07/2026 | 02/07/2026 | <https://000067.awsstudygroup.com> |
| 6 | - Tìm hiểu Amazon EKS (Elastic Kubernetes Service) & Mã nguồn hạ tầng Container: <br>&emsp; + Kiến trúc Control Plane & Các nút thợ Worker Nodes của cụm máy chủ Kubernetes/EKS <br>&emsp; + Giới thiệu bộ mẫu EKS Blueprints cho AWS CDK để triển khai EKS tự động | 03/07/2026 | 03/07/2026 | <https://000126.awsstudygroup.com> <br> <https://000065.awsstudygroup.com> |

### Kết quả đạt được tuần 9

* Đóng gói ứng dụng thành công bằng Docker với kỹ thuật multi-stage build tối ưu dung lượng.
* Quản lý vòng đời lưu trữ container images bảo mật trên Amazon ECR.
* Triển khai hệ thống microservices dạng container chạy hoàn toàn theo mô hình Serverless trên Amazon ECS Fargate.
* Hiểu tổng quan về Kubernetes và kiến trúc khởi tạo cluster nâng cao với Amazon EKS.
