---
title: "Worklog Tuần 3"
date: 2026-05-18
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3

* Hiểu tổng quan và cách hoạt động của Amazon RDS (Relational Database Service) và các database engines (MySQL, PostgreSQL, Aurora).
* Tìm hiểu cơ chế High Availability với Multi-AZ Deployment và mở rộng khả năng đọc với Read Replicas.
* Tiếp cận cơ sở dữ liệu NoSQL với Amazon DynamoDB (Tables, Primary Key, Sort Key, Indexing) và bộ nhớ đệm In-Memory Caching với Amazon ElastiCache.

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - **Database Essentials with Amazon RDS:** <br>&emsp; + Database Engines (MySQL, PostgreSQL, Aurora) <br>&emsp; + Instance Classes, Storage Types (gp3, io2) & Subnet Groups <br>&emsp; + Automated Backups, Snapshots & Parameter Groups | 18/05/2026 | 18/05/2026 | <https://000005.awsstudygroup.com> |
| 3 | - **RDS High Availability & Scaling:** <br>&emsp; + Multi-AZ deployment (Synchronous replication & Automatic Failover) <br>&emsp; + Read Replicas (Asynchronous replication cho read scaling) <br>&emsp; + **Thực hành:** Khởi tạo Amazon RDS MySQL Multi-AZ trong Private Subnets, cấu hình Security Group hạn chế truy cập | 19/05/2026 | 19/05/2026 | <https://000005.awsstudygroup.com> |
| 4 | - **NoSQL Database Essentials with Amazon DynamoDB:** <br>&emsp; + Partition Key, Sort Key & Composite Primary Key <br>&emsp; + Read/Write Capacity Modes (On-Demand vs Provisioned) <br>&emsp; + Local Secondary Indexes (LSI) & Global Secondary Indexes (GSI) | 20/05/2026 | 20/05/2026 | <https://000060.awsstudygroup.com> |
| 5 | - **In-Memory Caching with Amazon ElastiCache:** <br>&emsp; + Tổng quan bộ nhớ đệm In-Memory Caching (Redis vs Memcached) <br>&emsp; + Chiến lược Cache-Aside và Write-Through tối ưu hiệu năng truy vấn DB <br>&emsp; + **Thực hành:** Tạo bảng DynamoDB và thực thi các thao tác CRUD từ AWS CLI/SDK | 21/05/2026 | 21/05/2026 | <https://000061.awsstudygroup.com> <br> <https://000060.awsstudygroup.com> |
| 6 | - **Database Migration Overview (AWS DMS & SCT):** <br>&emsp; + Tổng quan chuyển đổi dữ liệu với AWS Schema Conversion Tool (SCT) và AWS Database Migration Service (DMS) <br>&emsp; + So sánh và lựa chọn giải pháp lưu trữ: Relational (RDS) vs NoSQL (DynamoDB) vs Cache (ElastiCache) | 22/05/2026 | 22/05/2026 | <https://000043.awsstudygroup.com> |

### Kết quả đạt được tuần 3

* Làm chủ việc khởi tạo, bảo mật và kết nối Amazon RDS instance từ môi trường ứng dụng trong Private Subnet.
* Hiểu sâu cơ chế sao lưu tự động và khả năng khôi phục Multi-AZ High Availability của RDS.
* Thành thạo mô hình dữ liệu NoSQL, thiết lập chỉ mục GSI/LSI và truy vấn dữ liệu trên Amazon DynamoDB.
* Đánh giá và áp dụng được giải pháp In-Memory Caching tăng tốc độ phản hồi ứng dụng web.

