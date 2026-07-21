---
title: "Worklog Tuần 7"
date: 2026-06-15
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7

* Hiểu triết lý Hạ tầng dưới dạng mã (Infrastructure as Code - IaC) với AWS CloudFormation & AWS CDK v2 (TypeScript/Python).
* Tìm hiểu công nghệ Container hóa ứng dụng với Docker (Dockerfile, Multi-stage builds) và quản lý lưu trữ container image riêng tư trên Amazon ECR.
* Triển khai container microservices với Amazon ECS trên Serverless AWS Fargate và tìm hiểu tổng quan Amazon EKS (Kubernetes).

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - **Infrastructure as Code (AWS CloudFormation & AWS CDK):** <br>&emsp; + CloudFormation Template syntax (YAML/JSON) & Stack Drift Detection <br>&emsp; + Kiến trúc AWS CDK v2: App, Stacks & L2 Constructs <br>&emsp; + Các câu lệnh CDK CLI (`cdk init`, `cdk synth`, `cdk diff`, `cdk deploy`) | 15/06/2026 | 15/06/2026 | <https://000037.awsstudygroup.com> <br> <https://000038.awsstudygroup.com> |
| 3 | - **Containerization with Docker & Amazon ECR:** <br>&emsp; + Viết Dockerfile chuẩn hóa & kỹ thuật Multi-stage build tối ưu kích thước image <br>&emsp; + Khởi tạo kho lưu trữ Amazon ECR Private Repository và đẩy (push) container image | 16/06/2026 | 16/06/2026 | <https://000015.awsstudygroup.com> |
| 4 | - **Amazon ECS & AWS Fargate:** <br>&emsp; + Cấu hình Task Definitions (CPU, Memory, Logs) & ECS Services <br>&emsp; + Khởi tạo cụm máy chủ ECS Cluster chạy theo mô hình Serverless AWS Fargate <br>&emsp; + Tích hợp ECS Service với bộ cân bằng tải Application Load Balancer (ALB) | 17/06/2026 | 17/06/2026 | <https://000067.awsstudygroup.com> |
| 5 | - **Amazon EKS (Elastic Kubernetes Service) Overview:** <br>&emsp; + Kiến trúc EKS Control Plane, Worker Nodes và EKS Blueprints cho AWS CDK <br>&emsp; + So sánh kịch bản sử dụng: EC2 vs Serverless Lambda vs ECS Fargate vs EKS Kubernetes | 18/06/2026 | 18/06/2026 | <https://000126.awsstudygroup.com> <br> <https://000065.awsstudygroup.com> |
| 6 | - **Thực hành Tự động hóa Container IaC:** <br>&emsp; + Viết mã AWS CDK định nghĩa toàn bộ hạ tầng ECR, ECS Cluster Fargate, ALB & CloudWatch Logs <br>&emsp; + Triển khai thành công ứng dụng containerized qua câu lệnh `cdk deploy` | 19/06/2026 | 19/06/2026 | <https://000076.awsstudygroup.com> <br> <https://000067.awsstudygroup.com> |

### Kết quả đạt được tuần 7

* Thành thạo lập trình hạ tầng theo mô hình Hướng đối tượng với AWS CDK v2.
* Đóng gói ứng dụng web thành container image nhỏ gọn nhờ Docker Multi-stage build và quản lý bảo mật trên Amazon ECR.
* Triển khai hệ thống ứng dụng container chạy hoàn toàn không máy chủ (Serverless Container) trên Amazon ECS Fargate.
* Nắm vững kiến thức nền tảng về Kubernetes và giải pháp quản lý cụm EKS trên AWS.

