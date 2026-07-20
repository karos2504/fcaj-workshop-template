---
title: "Worklog Tuần 13"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.13. </b> "
---

### Mục tiêu tuần 13

* Kiểm thử tích hợp toàn bộ hệ thống (Integration Testing), đo đạc hiệu năng và tối ưu chi phí cho **SaaS Timekeeping Platform** theo đúng quy trình xử lý `Process Flow (1 - 16a)` từ sơ đồ `Demo.drawio`.
* Cấu hình khả năng quan sát (Observability): Kích hoạt **AWS X-Ray** để truy vết giao dịch phân tán (Distributed Tracing), xây dựng **CloudWatch Dashboards**, audit an toàn thông tin với **AWS Security Hub & GuardDuty**.
* Hoàn thiện tài liệu hướng dẫn Workshop chi tiết từng bước, xuất bản bài blog kỹ thuật, dựng video demo và Thuyết trình báo cáo thực tập trước Mentors AWS vào ngày **30/07/2026**.

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - **Kiểm thử Tích hợp & Kiểm thử Chịu tải (Integration & Load Testing):** <br>&emsp; + Kiểm thử end-to-end theo toàn bộ 16 luồng xử lý (`Process Flow 1 - 16a`): Route 53 -> CloudFront -> WAF -> Cognito Auth -> API Gateway -> Lambda Functions -> DynamoDB Single-Table -> Step Functions -> SQS -> SES & Payment Webhook <br>&emsp; + Chạy công cụ giả lập tải cao trên API Gateway & Lambda để đánh giá hạn ngạch (Throttling/Rate Limits) và khả năng tự động co giãn | 27/07/2026 | 27/07/2026 | <https://cloudjourney.awsstudygroup.com> |
| 3 | - **Distributed Tracing, Security Audit & Tối ưu Chi phí:** <br>&emsp; + Kích hoạt **AWS X-Ray** truy vết end-to-end các request từ API Gateway đến Lambda, DynamoDB và Step Functions để phát hiện bottleneck <br>&emsp; + Audit an toàn thông tin hệ thống với **AWS Security Hub**, **AWS GuardDuty** và xác nhận xoay vòng khóa tự động trên **AWS Secrets Manager** <br>&emsp; + Rà soát chi phí lưu trữ trên Amazon S3 (Intelligent-Tiering) và thiết lập cảnh báo ngưỡng chi phí chặt chẽ với AWS Budgets | 28/07/2026 | 28/07/2026 | <https://cloudjourney.awsstudygroup.com> |
| 4 | - **Soạn thảo Tài liệu Workshop, Bài Blog Kỹ thuật & Video Demo:** <br>&emsp; + **Tài liệu Workshop:** Viết hướng dẫn từng bước (Step-by-step Hands-on guide) triển khai SaaS Timekeeping Platform kèm sơ đồ kiến trúc `Demo.drawio` và phần hướng dẫn Teardown/Cleanup xóa tài nguyên <br>&emsp; + **Bài Blog Kỹ thuật:** Xuất bản bài viết kỹ thuật chủ đề *"Xây dựng hệ thống SaaS Điểm danh & Chấm công Multi-Tenant theo kiến trúc AWS Serverless (Cognito, DynamoDB Single-Table, Step Functions & EventBridge)"* <br>&emsp; + Quay và dựng Video Demo hoạt động thực tế của giải pháp | 29/07/2026 | 29/07/2026 | <https://cloudjourney.awsstudygroup.com> |
| 5 | - **Tổng kết & Báo cáo Thực tập (30/07/2026):** <br>&emsp; + Tổng kết kết quả và khép lại chương trình thực tập 13 tuần (05/05/2026 - 30/07/2026) | 30/07/2026 | 30/07/2026 | <https://cloudjourney.awsstudygroup.com> |

### Kết quả đạt được tuần 13

* Kiểm thử thành công và tối ưu hóa toàn bộ 16 luồng xử lý nghiệp vụ của hệ thống SaaS Timekeeping Platform theo sơ đồ `Demo.drawio`.
* Làm chủ AWS X-Ray trong việc quan sát và tối ưu hóa hiệu năng microservices serverless phân tán.
* Hoàn thành bộ tài liệu Workshop hướng dẫn thực hành chất lượng cao và xuất bản bài blog kỹ thuật chuyên sâu.
* Thuyết trình xuất sắc dự án Capstone trước Mentors, hoàn thành chương trình thực tập AWS Cloud Journey (05/05/2026 - 30/07/2026).
