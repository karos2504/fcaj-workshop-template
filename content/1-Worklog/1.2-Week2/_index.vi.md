---
title: "Worklog Tuần 2"
date: 2026-05-11
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2

* Nắm vững dịch vụ lưu trữ đối tượng Amazon S3 (Simple Storage Service), Storage Classes và các quy tắc quản lý vòng đời dữ liệu S3 Lifecycle.
* Tìm hiểu bảo mật S3 Bucket Policies, SSE Encryption và triển khai Hosting Website tĩnh trên S3.
* Cấu hình Amazon CloudFront CDN tăng tốc phân phối nội dung web, tìm hiểu CloudFront Edge Computing (Lambda@Edge) và quản lý tài nguyên bằng AWS CLI / AWS Cloud9.

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - **Command Line Operations with AWS CLI & AWS Cloud9:** <br>&emsp; + Khởi tạo môi trường lập trình đám mây AWS Cloud9 <br>&emsp; + Cài đặt & cấu hình AWS CLI (Access Key, Secret Key, Default Region) <br>&emsp; + Thao tác quản lý tài nguyên AWS bằng câu lệnh CLI | 11/05/2026 | 11/05/2026 | <https://000049.awsstudygroup.com> <br> <https://000011.awsstudygroup.com> |
| 3 | - **Static Website Hosting with Amazon S3:** <br>&emsp; + Buckets, Objects & Storage Classes (Standard, IA, Glacier, Deep Archive) <br>&emsp; + S3 Versioning, Object Locking & Quy tắc S3 Lifecycle chuyển đổi lớp lưu trữ tự động | 12/05/2026 | 12/05/2026 | <https://000057.awsstudygroup.com> |
| 4 | - **S3 Security Best Practices:** <br>&emsp; + Cấu hình Bucket Policies, ACLs, Block Public Access settings <br>&emsp; + Mã hóa dữ liệu tĩnh S3 SSE-S3 / SSE-KMS <br>&emsp; + **Thực hành:** Bật S3 Static Website Hosting, phân quyền đọc công khai cho website tĩnh | 13/05/2026 | 13/05/2026 | <https://000069.awsstudygroup.com> |
| 5 | - **Content Delivery with Amazon CloudFront:** <br>&emsp; + Khái niệm Mạng phân phối nội dung (CDN), Edge Locations, Distributions <br>&emsp; + Cấu hình Origin Access Control (OAC) bảo vệ S3 Bucket chỉ cho phép CloudFront truy cập <br>&emsp; + Tích hợp chứng chỉ SSL/TLS miễn phí qua AWS Certificate Manager (ACM) | 14/05/2026 | 14/05/2026 | <https://000094.awsstudygroup.com> |
| 6 | - **Edge Computing with CloudFront & Lambda@Edge:** <br>&emsp; + Khái niệm tính toán tại điểm biên Edge Computing với CloudFront Functions & Lambda@Edge <br>&emsp; + **Thực hành:** Triển khai CloudFront Distribution cho Website tĩnh S3, kiểm thử tốc độ tải và cấu hình Origin Access Control (OAC) | 15/05/2026 | 15/05/2026 | <https://000130.awsstudygroup.com> |

### Kết quả đạt được tuần 2

* Thành thạo thao tác điều khiển AWS CLI và môi trường phát triển AWS Cloud9.
* Quản lý tối ưu lưu trữ đối tượng trên Amazon S3 và thiết lập quy tắc Lifecycle tự động chuyển đổi tầng lưu trữ giúp tiết kiệm chi phí.
* Làm chủ bảo mật S3 Bucket Policies và mã hóa dữ liệu theo chuẩn Best Practices.
* Triển khai thành công Website tĩnh chuẩn sản xuất với Amazon S3, bảo mật bằng CloudFront OAC và tăng tốc qua CloudFront CDN.

