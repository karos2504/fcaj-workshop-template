---
title: "Worklog Tuần 8"
date: 2026-06-22
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8

* **Lên ý tưởng thiết kế dự án & Phân tích yêu cầu:** Hình thành ý tưởng kiến trúc mô hình Multi-Tenant SaaS Timekeeping Platform (Hệ thống Điểm danh & Chấm công Đa người dùng), khảo sát bài toán và phân tích các yêu cầu kỹ thuật.
* **Tiếp tục học trên CloudJourney:** Nghiên cứu kiến trúc Serverless, mô hình dữ liệu đệm và phương pháp phân lập dữ liệu Multi-Tenancy trên AWS (`https://cloudjourney.awsstudygroup.com/`).
* Xây dựng tài liệu Yêu cầu Hệ thống (SRS) và lập kế hoạch triển khai chi tiết cho các tuần dự án tiếp theo.

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - **Lên ý tưởng Đề tài Dự án (22/06/2026 – 28/06/2026):** <br>&emsp; + Tìm hiểu bối cảnh doanh nghiệp và nhu cầu quản lý chấm công thời gian thực theo mô hình Multi-Tenant SaaS <br>&emsp; + Tiếp tục học bài giảng tổng quan kiến trúc đệm & serverless trên CloudJourney | 22/06/2026 | 22/06/2026 | <https://cloudjourney.awsstudygroup.com> |
| 3 | - **Phân tích Yêu cầu Chức năng (Functional Requirements):** <br>&emsp; + Phân tích các nghiệp vụ Check-in/Check-out GPS, quản lý ca làm việc, tính công và xuất báo cáo tự động <br>&emsp; + Xác định luồng người dùng cho các nhóm: SuperAdmin, TenantAdmin và Employee | 23/06/2026 | 23/06/2026 | <https://cloudjourney.awsstudygroup.com> |
| 4 | - **Khảo sát Mô hình Multi-Tenancy trên AWS (Học trên CloudJourney):** <br>&emsp; + So sánh mô hình Phân lập Dữ liệu: Silo Model vs Pool Model trên Amazon DynamoDB <br>&emsp; + Nghiên cứu cơ chế phân lập dữ liệu cách ly theo `tenantId` và xác thực tập trung Amazon Cognito | 24/06/2026 | 24/06/2026 | <https://000060.awsstudygroup.com> <br> <https://000039.awsstudygroup.com> |
| 5 | - **Đánh giá Công nghệ & Đăng ký Gói Dịch vụ (Tech Stack Selection):** <br>&emsp; + Lựa chọn bộ công nghệ: Frontend (React/Vite), Backend (AWS Lambda), Auth (Cognito), Database (DynamoDB), IaC (AWS CDK) <br>&emsp; + Ước tính chi phí hạ tầng Serverless bằng AWS Pricing Calculator | 25/06/2026 | 25/06/2026 | <https://000022.awsstudygroup.com> <br> <https://000141.awsstudygroup.com> |
| 6 | - **Lập Kế hoạch & Phân rã Công việc (WBS):** <br>&emsp; + Hoàn thiện tài liệu Yêu cầu Hệ thống (System Requirements Specification) <br>&emsp; + Phân chia kế hoạch tuần: Thiết kế sơ đồ, Cấu hình Bảo mật, Cập nhật UI/UX Frontend & Backend | 26/06/2026 | 26/06/2026 | <https://cloudjourney.awsstudygroup.com> |

### Kết quả đạt được tuần 8

* Chốt ý tưởng thiết kế dự án Mô hình Multi-Tenant SaaS Timekeeping Platform và hoàn thành tài liệu Phân tích Yêu cầu.
* Tiếp tục học và nắm vững các mô hình kiến trúc Multi-Tenancy Serverless trên CloudJourney.
* Lựa chọn xong bộ công nghệ triển khai (Tech Stack) và hoàn thành bảng phân rã công việc WBS cho các tuần tiếp theo.

