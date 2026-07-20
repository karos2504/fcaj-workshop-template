---
title: "Worklog Tuần 10"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10

* Hiểu quy trình phát triển phần mềm hiện đại với các khái niệm CI/CD (Continuous Integration / Continuous Delivery & Deployment).
* Làm chủ bộ công cụ lập trình AWS Developer Tools (CodeCommit, CodeBuild, CodeDeploy & CodePipeline).
* Tự động hóa hoàn toàn quy trình đóng gói, kiểm thử và triển khai ứng dụng Serverless & ECS Container.

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Tìm hiểu văn hóa DevOps & Khái niệm CI/CD: <br>&emsp; + Sự khác biệt giữa CI, CD & Continuous Deployment <br>&emsp; + Tổng quan các dịch vụ AWS Developer Tools <br>&emsp; + Source control với AWS CodeCommit / GitHub integration | 06/07/2026 | 06/07/2026 | <https://000017.awsstudygroup.com> |
| 3 | - Tìm hiểu AWS CodeBuild: <br>&emsp; + Cấu trúc tệp cấu hình `buildspec.yml` (phases: install, pre_build, build, post_build) <br>&emsp; + Environment Images, Build Artifacts & Environment Variables | 07/07/2026 | 07/07/2026 | <https://000017.awsstudygroup.com> <br> <https://000051.awsstudygroup.com> |
| 4 | - Tìm hiểu AWS CodeDeploy & Chiến lược triển khai: <br>&emsp; + In-place deployment vs Blue/Green deployment <br>&emsp; + Deployment groups, AppSpec file (`appspec.yml`) & Rollback triggers | 08/07/2026 | 08/07/2026 | <https://000023.awsstudygroup.com> |
| 5 | - Tìm hiểu AWS CodePipeline: <br>&emsp; + Các Stages (Source, Build, Test, Deploy, Manual Approval) <br>&emsp; + Tích hợp Webhooks từ GitHub / CodeCommit tự động kích hoạt Pipeline khi có git push | 09/07/2026 | 09/07/2026 | <https://000023.awsstudygroup.com> <br> <https://000152.awsstudygroup.com> |
| 6 | - **Thực hành:** <br>&emsp; + Thiết lập CI/CD Pipeline hoàn chỉnh tự động build Docker Image, push ECR & deploy lên ECS Fargate mỗi khi phát sinh commit mới <br>&emsp; + Cấu hình thông báo Slack/Email qua CloudWatch Events khi pipeline thành công hoặc thất bại | 10/07/2026 | 10/07/2026 | <https://000152.awsstudygroup.com> |

### Kết quả đạt được tuần 10

* Nắm vững các bước xây dựng quy trình phân phối phần mềm tự động hóa CI/CD trên AWS.
* Viết thành thạo `buildspec.yml` và `appspec.yml` quản lý giai đoạn build và deploy ứng dụng.
* Xây dựng thành công pipeline tự động hóa end-to-end cho ứng dụng Container/Serverless.
* Áp dụng thành công chiến lược Blue/Green deployment hạn chế tối đa thời gian gián đoạn dịch vụ (Zero Downtime).
