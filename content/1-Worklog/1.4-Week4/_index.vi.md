---
title: "Worklog Tuần 4"
date: 2026-05-25
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4

* Hiểu các khái niệm Giám sát (Monitoring), Ghi log (Logging) và Khả năng quan sát (Observability) trên AWS.
* Sử dụng thành thạo Amazon CloudWatch (Metrics, Custom CloudWatch Agent, Dashboards, Alarms & Logs Insights).
* Giám sát lưu lượng mạng bằng VPC Flow Logs và khám phá tích hợp CloudWatch với Amazon Managed Grafana.

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - **Monitoring with Amazon CloudWatch:** <br>&emsp; + Metrics (System metrics vs Custom metrics) <br>&emsp; + Cài đặt CloudWatch Agent trên EC2 thu thập Memory & Disk utilization metrics <br>&emsp; + Xây dựng CloudWatch Dashboards trực quan hóa dữ liệu hạ tầng | 25/05/2026 | 25/05/2026 | <https://000008.awsstudygroup.com> |
| 3 | - **CloudWatch Logs & SNS Alarms:** <br>&emsp; + Log Groups, Log Streams & Retention Policies <br>&emsp; + CloudWatch Alarms (Static Threshold & Anomaly Detection) <br>&emsp; + Tích hợp CloudWatch Alarms với Amazon SNS phát email cảnh báo tự động | 26/05/2026 | 26/05/2026 | <https://000008.awsstudygroup.com> <br> <https://000077.awsstudygroup.com> |
| 4 | - **Network Monitoring with VPC Flow Logs:** <br>&emsp; + Khởi tạo VPC Flow Logs thu thập IP traffic chấp nhận (ACCEPT) và từ chối (REJECT) <br>&emsp; + Đẩy Flow Logs về CloudWatch Logs & Amazon S3 <br>&emsp; + **Thực hành:** Phân tích sự cố kết nối Security Group / NACL từ VPC Flow Logs | 27/05/2026 | 27/05/2026 | <https://000074.awsstudygroup.com> |
| 5 | - **CloudWatch Logs Insights & Observability:** <br>&emsp; + Truy vấn ngữ pháp CloudWatch Logs Insights (`filter`, `fields`, `stats`, `sort`) <br>&emsp; + Tích hợp nguồn dữ liệu CloudWatch với Amazon Managed Grafana cho Dashboard nâng cao | 28/05/2026 | 28/05/2026 | <https://000036.awsstudygroup.com> <br> <https://000029.awsstudygroup.com> |
| 6 | - **Cost & Resource Optimization:** <br>&emsp; + Phân tích xu hướng chi tiêu tài nguyên với AWS Cost & Usage Management <br>&emsp; + **Thực hành:** Viết câu truy vấn Logs Insights tìm lỗi trong application log và thiết lập quy trình phản hồi sự cố tự động | 29/05/2026 | 29/05/2026 | <https://000064.awsstudygroup.com> <br> <https://000029.awsstudygroup.com> |

### Kết quả đạt được tuần 4

* Cài đặt và cấu hình thành công CloudWatch Agent thu thập custom metrics (RAM/Disk) trên EC2.
* Xây dựng Dashboard giám sát trực quan chuyên nghiệp cho toàn bộ hệ thống.
* Thu thập và phân tích lưu lượng mạng thực tế với VPC Flow Logs để phát hiện truy cập bất thường.
* Thành thạo kỹ năng truy vấn log bằng CloudWatch Logs Insights giúp rút ngắn thời gian khắc phục sự cố.

