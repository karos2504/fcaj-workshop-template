---
title: "Worklog Tuần 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2

* Nắm vững kiến thức nền tảng về hạ tầng mạng Amazon VPC và bảo mật mạng trên AWS.
* Thiết kế và triển khai custom VPC tích hợp Public Subnets, Private Subnets, Internet Gateway và NAT Gateway.
* Hiểu sâu về phân quyền IAM (Users, Groups, Roles, Policies) và giám sát lưu lượng mạng với VPC Flow Logs.

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Tìm hiểu chuyên sâu IAM (Identity and Access Management): <br>&emsp; + IAM Users, Groups, Roles & Policies (Managed vs Inline) <br>&emsp; + Principle of Least Privilege & Bật MFA bảo mật | 11/05/2026 | 11/05/2026 | <https://000002.awsstudygroup.com> |
| 3 | - Tìm hiểu lý thuyết Amazon VPC Core Components: <br>&emsp; + CIDR Blocks, Public Subnets & Private Subnets <br>&emsp; + Internet Gateway (IGW), NAT Gateway & Route Tables | 12/05/2026 | 12/05/2026 | <https://000003.awsstudygroup.com> <br> <https://000092.awsstudygroup.com> |
| 4 | - **Thực hành:** <br>&emsp; + Khởi tạo Custom VPC với 2 Public Subnets và 2 Private Subnets trên 2 AZs <br>&emsp; + Cấu hình Internet Gateway cho Public Subnet & NAT Gateway cho Private Subnet | 13/05/2026 | 13/05/2026 | <https://000003.awsstudygroup.com> |
| 5 | - Tìm hiểu cơ chế bảo mật mạng: Security Groups (Stateful) vs Network ACLs (Stateless) <br> - Tìm hiểu VPC Peering và VPC Flow Logs giám sát lưu lượng mạng | 14/05/2026 | 14/05/2026 | <https://000019.awsstudygroup.com/> <br> <https://000074.awsstudygroup.com> |
| 6 | - **Thực hành:** <br>&emsp; + Thiết lập Security Groups & NACL rules cho Web Server và Bastion Host <br>&emsp; + Cấu hình VPC Flow Logs đẩy log về CloudWatch Logs <br>&emsp; + Kiểm tra kết nối mạng giữa các subnet và xác nhận tính riêng tư của Private Subnet | 15/05/2026 | 15/05/2026 | <https://000074.awsstudygroup.com> |

### Kết quả đạt me được tuần 2

* Thành thạo phân quyền tối thiểu IAM và thiết lập MFA cho các tài khoản.
* Làm chủ kiến trúc mạng VPC: Tự tay thiết kế và cấu hình VPC hoàn chỉnh đáp ứng chuẩn thiết kế multi-AZ.
* Phân biệt rõ sự khác nhau và kết hợp hiệu quả giữa Security Groups và Network ACLs.
* Thu thập và phân tích được lưu lượng mạng bằng VPC Flow Logs.
