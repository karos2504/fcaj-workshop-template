---
title: "Triển khai Frontend & CloudFront CDN"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6 </b> "
---

# Triển khai React SPA Frontend & CloudFront CDN

Trong phần này, bạn sẽ build ứng dụng web giao diện người dùng **React Single Page Application (SPA)**, đưa mã nguồn static lên **Amazon S3 Bucket** và phân phối toàn cầu thông qua **Amazon CloudFront CDN** tích hợp cơ chế bảo mật Header verification (`x-origin-verify`).

---

### 1. Phân tích Kiến trúc Edge Protection Layer

```
[User Browser] ➔ [Route 53] ➔ [Amazon CloudFront CDN (WAF + Shield)]
                                 ├──> [Amazon S3 Bucket (React Static Assets)]
                                 └──> [API Gateway (Header: x-origin-verify)]
```

* **Amazon S3 (`SpaBucket`):** Lưu trữ các file `index.html`, `js`, `css`, hình ảnh của ứng dụng React. Bucket được cấu hình chặn toàn bộ truy cập public trực tiếp từ ngoài Internet.
* **Amazon CloudFront:** Phân phối nội dung tĩnh tại các Edge Location toàn cầu với độ trễ thấp nhất.
* **Custom Verification Header (`x-origin-verify`):** CloudFront tự động chèn một mã token bí mật vào mọi request API gửi về API Gateway. API Gateway chỉ chấp nhận yêu cầu nếu chứa đúng Secret Header này, ngăn chặn kẻ tấn công truy cập trực tiếp URL API Gateway mà không qua CloudFront/WAF.

---

### 2. Cấu hình biến môi trường Frontend (`.env.production`)

Di chuyển vào thư mục `frontend/` và cập nhật file cấu hình môi trường với thông tin tài nguyên Backend đã triển khai từ Bài 5.3:

```bash
cd ../frontend
```

Tạo file `.env.production`:

```ini
VITE_API_BASE_URL=https://xxxxxxx.execute-api.us-east-1.amazonaws.com/prod
VITE_COGNITO_USER_POOL_ID=us-east-1_xxxxxxxxx
VITE_COGNITO_CLIENT_ID=xxxxxxxxxxxxxxxxxxxxxxxxxx
VITE_AWS_REGION=us-east-1
```

---

### 3. Build ứng dụng React SPA

Tiến hành cài đặt thư viện và đóng gói ứng dụng:

```bash
npm install
npm run build
```

Thư mục `dist/` chứa toàn bộ file static của ứng dụng web sẽ được tạo ra:

```text
dist/
├── assets/
│   ├── index-xxxx.js
│   └── index-xxxx.css
├── favicon.ico
└── index.html
```

---

### 4. Upload Static Files lên Amazon S3 Bucket

Sử dụng AWS CLI để khởi tạo Bucket và đồng bộ thư mục `dist/` lên S3 SPA Bucket:

```bash
# Tạo S3 Bucket chứa Frontend
aws s3 mb s3://smart-attendance-spa-hosting-<AWS_ACCOUNT_ID> --region ap-southeast-1

# Đồng bộ file build lên S3 Bucket
aws s3 sync dist/ s3://smart-attendance-spa-hosting-<AWS_ACCOUNT_ID> --delete
```

![Kết quả upload static files lên S3 Bucket](/images/5-Workshop/5.6-Frontend-CloudFront/upload_static_files.png)

> [!TIP]
> **Xử lý lỗi `Your account must be verified before you can add new CloudFront resources`:**  
> Lỗi này xuất hiện trên các tài khoản AWS mới do chính sách bảo mật tạm thời khóa tạo CloudFront.  
>
> * **Giải pháp dùng ngay (S3 Website Endpoint):** Bạn có thể bật S3 Static Website Hosting để xem trước giao diện lập tức:
>
>   ```bash
>   aws s3 website s3://smart-attendance-spa-hosting-<AWS_ACCOUNT_ID>/ --index-document index.html
>   ```
>
>   Truy cập link: `http://smart-attendance-spa-hosting-<AWS_ACCOUNT_ID>.s3-website.ap-southeast-1.amazonaws.com`
> * **Mở khóa CloudFront:** Mở ticket tại [AWS Support Center](https://console.aws.amazon.com/support/home#/) chọn **Account Verification** để kích hoạt dịch vụ CloudFront.

---

### 5. Kiểm tra ứng dụng trên CloudFront CDN

1. Truy cập [Amazon CloudFront Console](https://console.aws.amazon.com/cloudfront/).
2. Chọn Distribution tương ứng với project `smart-attendance`.
3. Khởi tạo **Invalidation** để xóa cache cũ:

   ```bash
   aws cloudfront create-invalidation --distribution-id <DISTRIBUTION_ID> --paths "/*"
   ```

4. Mở đường dẫn Domain CloudFront (ví dụ: `https://dxxxxxxxxx.cloudfront.net`) hoặc S3 Website Endpoint trên trình duyệt để kiểm tra giao diện ứng dụng!

