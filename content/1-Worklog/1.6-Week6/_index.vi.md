---
title: "Worklog Tuần 6"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6

* Hiểu các nguyên lý thiết kế hệ thống tính sẵn sàng cao (High Availability) và tự động mở rộng (Scalability).
* Cấu hình Elastic Load Balancing (Application Load Balancer - ALB) phân phối lưu lượng truy cập.
* Thiết lập EC2 Auto Scaling Group và Route 53 Health Checks & DNS Failover.

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Tìm hiểu Elastic Load Balancing (ELB): <br>&emsp; + ALB (Layer 7) vs NLB (Layer 4) <br>&emsp; + Target Groups, Health Checks & Listener Rules <br>&emsp; + SSL/TLS Termination với AWS Certificate Manager (ACM) | 08/06/2026 | 08/06/2026 | <https://000006.awsstudygroup.com> |
| 3 | - Tìm hiểu EC2 Auto Scaling Groups (ASG): <br>&emsp; + Launch Templates vs Launch Configurations <br>&emsp; + Scaling Policies: Target Tracking, Step Scaling & Scheduled Scaling <br>&emsp; + Dynamic Scaling dựa trên CPU utilization / ALB Request count | 09/06/2026 | 09/06/2026 | <https://000006.awsstudygroup.com> |
| 4 | - **Thực hành:** <br>&emsp; + Tạo Launch Template định nghĩa Web Server EC2 <br>&emsp; + Khởi tạo ALB trên 2 Public Subnets và gắn Target Group <br>&emsp; + Tạo Auto Scaling Group spanning 2 Private Subnets tích hợp với ALB | 10/06/2026 | 10/06/2026 | <https://000006.awsstudygroup.com> |
| 5 | - Tìm hiểu Amazon Route 53 & Hybrid DNS: <br>&emsp; + Hosted Zones (Public vs Private) <br>&emsp; + Routing Policies: Simple, Weighted, Latency, Failover & Geolocation <br>&emsp; + Route 53 Health Checks cấu hình DNS Failover | 11/06/2026 | 11/06/2026 | <https://000010.awsstudygroup.com> <br> <https://000101.awsstudygroup.com> |
| 6 | - **Thực hành:** <br>&emsp; + Giả lập tải cao bằng công cụ Stress Test trên EC2 để kiểm tra Auto Scaling tự động tăng/giảm số lượng instance <br>&emsp; + Cấu hình Route 53 Failover Routing thử nghiệm chuyển hướng lưu lượng khi primary region gặp sự cố | 12/06/2026 | 12/06/2026 | <https://000101.awsstudygroup.com> |

### Kết quả đạt được tuần 6

* Triển khai thành công bộ cân bằng tải Application Load Balancer phân phối lưu lượng truy cập đa AZ.
* Thiết lập Auto Scaling Group tự động co giãn tài nguyên EC2 theo nhu cầu thực tế.
* Làm chủ các chiến lược định tuyến Route 53 DNS và cơ chế tự động chuyển hướng khi xảy ra thảm họa (Disaster Recovery Failover).
