---
title: "Worklog Tuần 10"
date: 2026-07-06
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10

* **Thực hiện cấu hình bảo mật cơ bản cho dự án:** Triển khai các lớp bảo mật cho dữ liệu tĩnh, dữ liệu truyền tải, tầng API và phân quyền dịch vụ cho dự án SaaS Timekeeping Platform.
* **Tiếp tục học trên CloudJourney:** Tìm hiểu các tiêu chuẩn an toàn thông tin trên AWS, giải pháp mã hóa KMS, Secrets Manager & AWS WAF v2 (`https://cloudjourney.awsstudygroup.com/`).
* Đảm bảo hệ thống đạt chuẩn an toàn bảo mật, chống khai thác lỗ hổng và rò rỉ dữ liệu nhạy cảm.

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - **Nghiên cứu Giải pháp Bảo mật AWS (06/07/2026 – 12/07/2026):** <br>&emsp; + Học các bài giảng bảo mật dữ liệu và quản lý khóa mã hóa trên CloudJourney <br>&emsp; + Phân tích mô hình bảo mật 3 tầng cho dự án: Tầng Biên (WAF), Tầng Xác thực (Cognito/IAM) & Tầng Dữ liệu (KMS) | 06/07/2026 | 06/07/2026 | <https://cloudjourney.awsstudygroup.com> <br> <https://000033.awsstudygroup.com> |
| 3 | - **Cấu hình Mã hóa Dữ liệu với AWS KMS (CMK):** <br>&emsp; + Tạo Customer Managed Keys (CMK) mã hóa bảng DynamoDB Single-Table và S3 Bucket lưu trữ báo cáo <br>&emsp; + Cấu hình KMS Key Policy giới hạn quyền truy cập cho dịch vụ Lambda | 07/07/2026 | 07/07/2026 | <https://000033.awsstudygroup.com> |
| 4 | - **Quản lý Thông tin Nhạy cảm với AWS Secrets Manager:** <br>&emsp; + Lưu trữ API keys, kết nối database và thông tin cấu hình nhạy cảm lên Secrets Manager <br>&emsp; + Cấu hình tự động xoay vòng (Automatic Secrets Rotation) và tích hợp lấy bí mật từ mã nguồn Lambda | 08/07/2026 | 08/07/2026 | <https://000096.awsstudygroup.com> |
| 5 | - **Cấu hình Bảo mật Tầng Biên với AWS WAF v2:** <br>&emsp; + Thiết lập WAF Web ACL gắn vào Amazon CloudFront & API Gateway HTTP API v2 <br>&emsp; + Áp dụng các nhóm luật AWS Managed Rules (chống SQL Injection, XSS) và cấu hình Rate-based Rule ngăn chặn tấn công DDoS | 09/07/2026 | 09/07/2026 | <https://000026.awsstudygroup.com> |
| 6 | - **Rà soát Phân quyền IAM & Kiểm thử Bảo mật:** <br>&emsp; + Cấu hình IAM Execution Roles cho tất cả các hàm Lambda theo chuẩn Quyền Tối thiểu (Least Privilege) <br>&emsp; + Thực hiện audit bảo mật cơ bản cho toàn bộ API Gateway endpoints | 10/07/2026 | 10/07/2026 | <https://000002.awsstudygroup.com> |

### Kết quả đạt được tuần 10

* Hoàn thành cấu hình bảo mật cơ bản cho toàn bộ hạ tầng dự án SaaS Timekeeping Platform.
* Tiếp tục nâng cao kiến thức bảo mật đám mây nhờ các bài học hướng dẫn trên CloudJourney.
* Mã hóa an toàn dữ liệu tĩnh với AWS KMS CMK và bảo vệ tầng API chống lại các cuộc tấn công phổ biến với AWS WAF.


