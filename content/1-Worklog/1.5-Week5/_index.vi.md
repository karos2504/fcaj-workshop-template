---
title: "Worklog Tuần 5"
date: 2026-06-01
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5

* Hiểu các nguyên lý thiết kế hệ thống tính sẵn sàng cao (High Availability) và tự động mở rộng (Scalability) trên AWS.
* Cấu hình bộ cân bằng tải Elastic Load Balancing (Application Load Balancer - ALB) phân phối lưu lượng truy cập đa AZ.
* Thiết lập EC2 Auto Scaling Group, Amazon Route 53 DNS Routing Policies & VPC Peering kết nối mạng.

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - **Elastic Load Balancing (ELB Essentials):** <br>&emsp; + So sánh ALB (Layer 7) vs NLB (Layer 4) <br>&emsp; + Target Groups, Health Checks & Listener Rules <br>&emsp; + SSL/TLS Termination với chứng chỉ AWS Certificate Manager (ACM) | 01/06/2026 | 01/06/2026 | <https://000006.awsstudygroup.com> |
| 3 | - **EC2 Auto Scaling Groups (ASG):** <br>&emsp; + Launch Templates vs Launch Configurations <br>&emsp; + Scaling Policies: Target Tracking, Step Scaling & Scheduled Scaling <br>&emsp; + Dynamic Scaling dựa trên CPU utilization / ALB Request count | 02/06/2026 | 02/06/2026 | <https://000006.awsstudygroup.com> |
| 4 | - **Thực hành:** <br>&emsp; + Khởi tạo Launch Template định nghĩa Web Server EC2 <br>&emsp; + Dựng ALB trên 2 Public Subnets và gắn Target Group <br>&emsp; + Tạo Auto Scaling Group spanning 2 Private Subnets tích hợp với ALB | 03/06/2026 | 03/06/2026 | <https://000006.awsstudygroup.com> |
| 5 | - **Amazon Route 53 & Hybrid DNS:** <br>&emsp; + Public vs Private Hosted Zones <br>&emsp; + Các quy tắc định tuyến Routing Policies: Simple, Weighted, Latency, Failover & Geolocation <br>&emsp; + Route 53 Health Checks & VPC Peering (kết nối 2 VPC riêng biệt) | 04/06/2026 | 04/06/2026 | <https://000010.awsstudygroup.com> <br> <https://000019.awsstudygroup.com/> |
| 6 | - **Building Highly Available Web Applications:** <br>&emsp; + Giả lập tải cao bằng công cụ Stress Test trên EC2 để kiểm tra Auto Scaling tự động mở rộng instance <br>&emsp; + Cấu hình Route 53 Failover Routing thử nghiệm chuyển hướng lưu lượng khi xảy ra sự cố | 05/06/2026 | 05/06/2026 | <https://000101.awsstudygroup.com> |

### Kết quả đạt được tuần 5

* Triển khai thành công bộ cân bằng tải Application Load Balancer phân phối lưu lượng truy cập mượt mà qua các Availability Zones.
* Thiết lập Auto Scaling Group tự động co giãn số lượng EC2 instance theo nhu cầu thực tế.
* Làm chủ các chiến lược định tuyến DNS với Amazon Route 53 và cơ chế tự động chuyển hướng sự cố (Disaster Recovery Failover).
* Kết nối hai hạ tầng VPC riêng biệt thông qua giải pháp VPC Peering.

