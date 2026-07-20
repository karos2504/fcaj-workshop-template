---
title: "Worklog Tuần 11"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11

* Hiểu các giải pháp bảo mật dữ liệu, mã hóa và tuân thủ trên AWS (AWS KMS, Secrets Manager, WAF, GuardDuty).
* Tìm hiểu giải pháp chuyển đổi cơ sở dữ liệu (Migration) với AWS DMS & SCT.
* Khám phá tổng quan về Data Lake & Phân tích dữ liệu serverless với Amazon Athena.

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Tìm hiểu AWS KMS (Key Management Service) & AWS Secrets Manager: <br>&emsp; + Customer Managed Keys (CMK), Envelope Encryption & Key Policies <br>&emsp; + Quản lý, xoay vòng tự động (Automatic Rotation) credentials DB trong Secrets Manager | 13/07/2026 | 13/07/2026 | <https://000033.awsstudygroup.com> <br> <https://000096.awsstudygroup.com> |
| 3 | - Tìm hiểu AWS WAF (Web Application Firewall) & Threat Detection: <br>&emsp; + Managed Rule Groups (SQLi, XSS, OWASP Top 10) & Rate Limiting <br>&emsp; + Giám sát an ninh với AWS GuardDuty & AWS Security Hub | 14/07/2026 | 14/07/2026 | <https://000026.awsstudygroup.com> <br> <https://000098.awsstudygroup.com> |
| 4 | - **Thực hành:** <br>&emsp; + Tạo KMS Key mã hóa S3 Bucket & EBS Volume <br>&emsp; + Cấu hình AWS WAF Web ACL bảo vệ Application Load Balancer <br>&emsp; + Lưu trữ DB password trong Secrets Manager và lấy credential từ ứng dụng Lambda | 15/07/2026 | 15/07/2026 | <https://000033.awsstudygroup.com> <br> <https://000026.awsstudygroup.com> |
| 5 | - Tìm hiểu Chuyển đổi dữ liệu (AWS Migration): <br>&emsp; + AWS Schema Conversion Tool (SCT) chuyển đổi schema On-Premises sang Cloud <br>&emsp; + AWS Database Migration Service (DMS) đồng bộ hóa dữ liệu thời gian thực (CDC) | 16/07/2026 | 16/07/2026 | <https://000043.awsstudygroup.com> |
| 6 | - Tìm hiểu Data & Analytics trên AWS: <br>&emsp; + Mô hình Data Lake trên Amazon S3 & AWS Glue Crawler/Data Catalog <br>&emsp; + Thực vấn dữ liệu trực tiếp trên S3 bằng câu lệnh SQL với Amazon Athena | 17/07/2026 | 17/07/2026 | <https://000035.awsstudygroup.com> <br> <https://000106.awsstudygroup.com> |

### Kết quả đạt được tuần 11

* Triển khai giải pháp mã hóa dữ liệu tĩnh (At-Rest) và dữ liệu chuyển động (In-Transit) sử dụng AWS KMS.
* Bảo vệ ứng dụng web chống tấn công mạng phổ biến (SQLi/XSS) với WAF Web ACLs.
* Loại bỏ việc hardcode mật khẩu nhờ quản lý tập trung trên AWS Secrets Manager.
* Hiểu quy trình dịch chuyển cơ sở dữ liệu lớn không làm gián đoạn hệ thống (AWS DMS/SCT) và phân tích dữ liệu serverless với Athena.
