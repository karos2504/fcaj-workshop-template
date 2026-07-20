---
title: "Worklog Tuần 4"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4

* Hiểu tổng quan và cách hoạt động của Amazon RDS (Relational Database Service) và các database engine hỗ trợ (MySQL, PostgreSQL).
* Tìm hiểu cơ chế High Availability với Multi-AZ Deployment và mở rộng đọc với Read Replicas.
* Tiếp cận NoSQL Database với Amazon DynamoDB (Tables, Primary Key, Sort Key, Capacity Modes, Indexing).

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Tìm hiểu Amazon RDS Core: <br>&emsp; + Database Engines (MySQL, PostgreSQL, Aurora) <br>&emsp; + Instance Classes, Storage Types (gp3, io2) & Subnet Groups <br>&emsp; + Automated Backups, Snapshots & Parameter Groups | 25/05/2026 | 25/05/2026 | <https://000005.awsstudygroup.com> |
| 3 | - Tìm hiểu kiến trúc RDS High Availability: <br>&emsp; + Multi-AZ deployment (Synchronous replication & Failover) <br>&emsp; + Read Replicas (Asynchronous replication cho read scaling) | 26/05/2026 | 26/05/2026 | <https://000005.awsstudygroup.com> |
| 4 | - **Thực hành:** <br>&emsp; + Khởi tạo Amazon RDS MySQL Multi-AZ instance trong Private Subnets <br>&emsp; + Cấu hình Security Group chỉ cho phép kết nối từ Web EC2 instance <br>&emsp; + Thử nghiệm kết nối ứng dụng từ EC2 và thực hiện manual failover test | 27/05/2026 | 27/05/2026 | <https://000005.awsstudygroup.com> |
| 5 | - Tìm hiểu Amazon DynamoDB NoSQL: <br>&emsp; + Partition Key, Sort Key & Composite Primary Key <br>&emsp; + Read/Write Capacity Modes (On-Demand vs Provisioned) <br>&emsp; + Local Secondary Indexes (LSI) & Global Secondary Indexes (GSI) | 28/05/2026 | 28/05/2026 | <https://000060.awsstudygroup.com> |
| 6 | - **Thực hành:** <br>&emsp; + Tạo bảng DynamoDB và thực thi các thao tác CRUD từ AWS CLI/SDK <br>&emsp; + So sánh hiệu năng, chi phí và kịch bản áp dụng RDS (Relational) vs DynamoDB (NoSQL) | 29/05/2026 | 29/05/2026 | <https://000060.awsstudygroup.com> |

### Kết quả đạt được tuần 4

* Làm chủ việc khởi tạo, bảo mật và kết nối Amazon RDS instance từ môi trường ứng dụng.
* Hiểu cơ chế sao lưu tự động và khả năng phục hồi dữ liệu Multi-AZ của RDS.
* Hiểu cấu trúc NoSQL và các nguyên tắc thiết kế bảng trên Amazon DynamoDB.
* Phân biệt rõ kịch bản chọn lựa giữa Relational DB (RDS) và NoSQL DB (DynamoDB).
