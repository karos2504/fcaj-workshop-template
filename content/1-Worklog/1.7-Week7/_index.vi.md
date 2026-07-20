---
title: "Worklog Tuần 7"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7

* Hiểu triết lý Hạ tầng dưới dạng mã (Infrastructure as Code - IaC) và các lợi ích trong quản lý tự động hóa hạ tầng đám mây.
* Làm chủ AWS CloudFormation: Viết tài liệu mẫu YAML tự động hóa khởi tạo VPC, Subnets, EC2, RDS & Security Groups.
* Tiếp cận và lập trình hạ tầng nâng cao với AWS Cloud Development Kit (AWS CDK v2) bằng ngôn ngữ TypeScript/Python.

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Tìm hiểu kiến thức cốt lõi AWS CloudFormation: <br>&emsp; + Cú pháp tài liệu mẫu (JSON/YAML): Cấu trúc FormatVersion, Mô tả (Description), Tham số (Parameters), Ánh xạ (Mappings), Điều kiện (Conditions), Tài nguyên (Resources), Đầu ra (Outputs) <br>&emsp; + Quản lý vòng đời Stack (Khởi tạo, Cập nhật, Phát hiện sai lệch Drift Detection, Khôi phục Rollback & Xóa stack) | 15/06/2026 | 15/06/2026 | <https://000037.awsstudygroup.com> |
| 3 | - **Thực hành:** <br>&emsp; + Viết CloudFormation Template khởi tạo toàn bộ hạ tầng VPC, Subnets, Internet Gateway & Security Groups <br>&emsp; + Thực thi triển khai stack qua AWS CLI & Kiểm tra phát hiện sai lệch hạ tầng (Drift Detection) khi chỉnh sửa thủ công | 16/06/2026 | 16/06/2026 | <https://000037.awsstudygroup.com> |
| 4 | - Tìm hiểu nền tảng AWS Cloud Development Kit (AWS CDK): <br>&emsp; + Kiến trúc CDK: Ứng dụng (App), Stacks & Các cấu trúc Constructs (L1, L2, L3 constructs) <br>&emsp; + Bộ lệnh CDK CLI (`cdk init`, `cdk synth`, `cdk diff`, `cdk deploy`, `cdk destroy`) | 17/06/2026 | 17/06/2026 | <https://000038.awsstudygroup.com> |
| 5 | - Tìm hiểu kỹ thuật AWS CDK nâng cao: <br>&emsp; + Kiến trúc nhiều Stack (Multi-stack) & Tham chiếu chéo dữ liệu giữa các Stack <br>&emsp; + Viết các Custom Constructs tái sử dụng trong doanh nghiệp <br>&emsp; + Áp dụng CDK Aspects & Kiểm thử đơn vị (Unit Testing) cho hạ tầng bằng Jest/PyTest | 18/06/2026 | 18/06/2026 | <https://000076.awsstudygroup.com> <br> <https://000102.awsstudygroup.com> |
| 6 | - **Thực hành:** <br>&emsp; + Xây dựng dự án AWS CDK khởi tạo hệ thống Web App 3-Tier (VPC + ALB + EC2 ASG + RDS) bằng mã nguồn TypeScript/Python <br>&emsp; + Thực hiện `cdk synth` sinh mẫu CloudFormation và `cdk deploy` triển khai hạ tầng tự động lên môi trường AWS | 19/06/2026 | 19/06/2026 | <https://000076.awsstudygroup.com> |

### Kết quả đạt được tuần 7

* Thành thạo cú pháp CloudFormation YAML để đóng gói và triển khai hạ tầng nhất quán.
* Hiểu cơ chế phát hiện sai lệch hạ tầng (Drift Detection) và xử lý sự cố rollback stack.
* Làm chủ AWS CDK v2: Lập trình hạ tầng bằng ngôn ngữ cao cấp (TypeScript/Python) sử dụng L2 Constructs.
* Tự động hóa hoàn toàn việc dựng hạ tầng phức tạp 3-tier chỉ với một câu lệnh CLI.
