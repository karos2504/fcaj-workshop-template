---
title: "Worklog Tuần 5"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5

* Hiểu các khái niệm giám sát (Monitoring), ghi log (Logging) và khả năng quan sát (Observability) trên AWS.
* Sử dụng thành thạo Amazon CloudWatch (Metrics, Dashboards, Alarms & Logs Insights).
* Tích hợp CloudWatch với Amazon SNS để cảnh báo và khám phá tích hợp CloudWatch với Grafana.

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Tìm hiểu Amazon CloudWatch Core Concepts: <br>&emsp; + Metrics (System metrics vs Custom metrics) <br>&emsp; + CloudWatch Agent cài đặt trên EC2 thu thập Memory/Disk metrics <br>&emsp; + CloudWatch Dashboards trực quan hóa dữ liệu | 01/06/2026 | 01/06/2026 | <https://000008.awsstudygroup.com> |
| 3 | - Tìm hiểu CloudWatch Logs & Amazon SNS: <br>&emsp; + Log Groups, Log Streams & Retention Policies <br>&emsp; + CloudWatch Alarms (Static Threshold & Anomaly Detection) <br>&emsp; + Tích hợp CloudWatch Alarms với Amazon SNS gửi email cảnh báo | 02/06/2026 | 02/06/2026 | <https://000008.awsstudygroup.com> <br> <https://000077.awsstudygroup.com> |
| 4 | - **Thực hành:** <br>&emsp; + Cài đặt CloudWatch Agent lên EC2 instance <br>&emsp; + Tạo Dashboard tổng quan hiển thị CPU, RAM, Disk I/O & Network <br>&emsp; + Cấu hình Alarm cảnh báo CPU > 85% và phát email thông báo qua SNS | 03/06/2026 | 03/06/2026 | <https://000008.awsstudygroup.com> |
| 5 | - Tìm hiểu CloudWatch Logs Insights & Observability nâng cao: <br>&emsp; + Viết câu truy vấn ngữ pháp CloudWatch Logs Insights (filter, fields, stats) <br>&emsp; + Giới thiệu tích hợp Amazon Managed Grafana với CloudWatch | 04/06/2026 | 04/06/2026 | <https://000036.awsstudygroup.com> <br> <https://000029.awsstudygroup.com> |
| 6 | - **Thực hành:** <br>&emsp; + Thu thập application logs từ EC2 và truy vấn log lỗi bằng Logs Insights <br>&emsp; + Xây dựng kịch bản phản hồi sự cố dựa trên cảnh báo tự động | 05/06/2026 | 05/06/2026 | <https://000029.awsstudygroup.com> |

### Kết quả đạt được tuần 5

* Cài đặt và cấu hình thành công CloudWatch Agent thu thập custom metrics (RAM/Disk).
* Xây dựng Dashboard giám sát trực quan chuyên nghiệp cho hạ tầng EC2 & RDS.
* Thiết lập quy trình tự động phát cảnh báo sự cố hạ tầng qua SNS Email Notification.
* Thành thạo kỹ năng truy vấn log bằng CloudWatch Logs Insights để nhanh chóng phát hiện lỗi.
