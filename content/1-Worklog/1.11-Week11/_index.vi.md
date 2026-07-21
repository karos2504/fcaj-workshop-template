---
title: "Worklog Tuần 11"
date: 2026-07-13
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11

* **Thực hiện chỉnh sửa cập nhật giao diện frontend và backend:** Tiến hành cập nhật, nâng cấp mã nguồn giao diện người dùng (React/Vite) và mã nguồn xử lý backend (AWS Lambda) cho dự án.
* **Tiếp tục học trên CloudJourney:** Học chuyên sâu phương pháp phát triển Web Application kết nối Serverless Backend và quy trình tự động hóa CI/CD (`https://cloudjourney.awsstudygroup.com/`).
* Hoàn thiện hạ tầng CDK v2 và thiết lập đường ống tự động hóa triển khai (AWS CodePipeline).

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - **Chỉnh sửa Cập nhật Giao diện Frontend (13/07/2026 – 19/07/2026):** <br>&emsp; + Cập nhật giao diện React/Vite: Tối ưu UI/UX màn hình Dashboard, bảng điều khiển Admin và giao diện Check-in GPS <br>&emsp; + Học bài giảng tích hợp Frontend trên CloudJourney | 13/07/2026 | 13/07/2026 | <https://cloudjourney.awsstudygroup.com> <br> <https://000141.awsstudygroup.com> |
| 3 | - **Chỉnh sửa Cập nhật Mã nguồn Backend (AWS Lambda):** <br>&emsp; + Refactor và tối ưu mã nguồn các hàm Lambda xử lý nghiệp vụ: `CheckInFunction`, `CheckOutFunction`, `AttendanceSummary` và `AdminFunction` <br>&emsp; + Xử lý định dạng dữ liệu phản hồi API chuẩn hóa | 14/07/2026 | 14/07/2026 | <https://000060.awsstudygroup.com> |
| 4 | - **Tích hợp Tương tác Frontend & Backend API Gateway:** <br>&emsp; + Kết nối các lệnh gọi HTTP API từ Frontend tới API Gateway v2 <br>&emsp; + Xử lý truyền Authorization Header (Bearer JWT Token) và cơ chế tự động làm mới Token | 15/07/2026 | 15/07/2026 | <https://000066.awsstudygroup.com> |
| 5 | - **Cập nhật Bộ Mã nguồn Hạ tầng AWS CDK v2:** <br>&emsp; + Cập nhật các stack hạ tầng: `DatabaseStack`, `AuthStack`, `ApiStack` và `FrontendStack` (S3 + CloudFront OAC) <br>&emsp; + Kiểm tra thực thi `cdk synth` và `cdk diff` | 16/07/2026 | 16/07/2026 | <https://000076.awsstudygroup.com> |
| 6 | - **Cập nhật CI/CD Pipeline & Kiểm thử Liên thông:** <br>&emsp; + Viết lại tệp `buildspec.yml` tự động build React UI, chạy unit tests và thực thi `cdk deploy` <br>&emsp; + Thực hiện kiểm thử toàn trình giữa Frontend và Backend sau khi cập nhật | 17/07/2026 | 17/07/2026 | <https://000152.awsstudygroup.com> |

### Kết quả đạt được tuần 11

* Hoàn thành việc chỉnh sửa, nâng cấp giao diện Frontend và mã nguồn Backend xử lý mượt mà.
* Tiếp tục học tập và áp dụng các kỹ thuật tự động hóa triển khai từ CloudJourney.
* Kết nối liên thông thành công giữa giao diện Web React và hệ thống Serverless Backend qua API Gateway.


