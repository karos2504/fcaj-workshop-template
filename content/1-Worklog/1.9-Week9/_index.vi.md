---
title: "Worklog Tuần 9"
date: 2026-06-29
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9

* **Chỉnh sửa sơ đồ cấu trúc dự án & Thiết kế kiến trúc:** Tiến hành rà soát, chỉnh sửa và chuẩn hóa sơ đồ cấu trúc dự án (`platform_architecture.drawio`), tối ưu luồng xử lý giữa các tầng Edge, Auth, Compute và Storage.
* **Tiếp tục học trên CloudJourney:** Học chuyên sâu các mẫu thiết kế kiến trúc chuẩn AWS Well-Architected và mô hình dữ liệu đệm DynamoDB Single-Table (`https://cloudjourney.awsstudygroup.com/`).
* Hoàn thiện hồ sơ sơ đồ kiến trúc và các chỉ mục dữ liệu phục vụ phát triển ứng dụng.

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - **Chỉnh sửa Sơ đồ Cấu trúc Dự án (29/06/2026 – 05/07/2026):** <br>&emsp; + Rà soát và chỉnh sửa bản vẽ sơ đồ kiến trúc `platform_architecture.drawio` cho hệ thống SaaS Timekeeping Platform <br>&emsp; + Tiếp tục học các chuyên đề thiết kế kiến trúc tối ưu trên CloudJourney | 29/06/2026 | 29/06/2026 | <https://cloudjourney.awsstudygroup.com> |
| 3 | - **Chỉnh sửa Sơ đồ Luồng Dữ liệu (Data Flow Diagram):** <br>&emsp; + Cập nhật luồng xử lý dữ liệu giữa API Gateway, các hàm Lambda và DynamoDB Single-Table Design <br>&emsp; + Chuẩn hóa cấu trúc Partition Key (PK) và Sort Key (SK) phân lập theo `tenantId` | 30/06/2026 | 30/06/2026 | <https://000060.awsstudygroup.com> <br> <https://000039.awsstudygroup.com> |
| 4 | - **Tối ưu hóa Sơ đồ Chỉ mục Phụ (GSI Indexing Structure):** <br>&emsp; + Chỉnh sửa sơ đồ `GSI1-PK` / `GSI1-SK` phục vụ truy vấn lịch sử chấm công theo phòng ban <br>&emsp; + Chỉnh sửa sơ đồ `GSI2-PK` / `GSI2-SK` phục vụ tổng hợp dữ liệu báo cáo doanh nghiệp | 01/07/2026 | 01/07/2026 | <https://000060.awsstudygroup.com> |
| 5 | - **Chỉnh sửa Sơ đồ Phân quyền Xác thực (Auth Architecture):** <br>&emsp; + Cập nhật sơ đồ tích hợp Amazon Cognito User Pools và cấu hình Custom Claims (`{tenantId, role}`) <br>&emsp; + Học bài giảng bảo mật tầng API trên CloudJourney | 02/07/2026 | 02/07/2026 | <https://000141.awsstudygroup.com> |
| 6 | - **Hoàn thiện Hồ sơ Kiến trúc & Chuẩn hóa API Contract:** <br>&emsp; + Chốt bản vẽ sơ đồ cấu trúc hệ thống hoàn chỉnh sau khi chỉnh sửa <br>&emsp; + Hoàn thiện tài liệu OpenAPI/Swagger định nghĩa dữ liệu API Gateway endpoints | 03/07/2026 | 03/07/2026 | <https://000066.awsstudygroup.com> |

### Kết quả đạt được tuần 9

* Hoàn thành việc chỉnh sửa và chuẩn hóa sơ đồ cấu trúc dự án (`platform_architecture.drawio`) đáp ứng tiêu chuẩn AWS Well-Architected.
* Tiếp tục học và áp dụng thành công các kiến thức thiết kế hệ thống từ CloudJourney vào dự án.
* Thống nhất sơ đồ luồng dữ liệu, cấu trúc DynamoDB Single-Table và hợp đồng API giữa các thành phần.
