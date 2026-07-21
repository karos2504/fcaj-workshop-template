---
title: "Chuẩn bị môi trường"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2 </b> "
---

# Chuẩn bị Môi trường Triển khai

Trước khi bắt đầu thực hành xây dựng hệ thống **Smart Attendance SaaS Platform**, bạn cần đảm bảo máy tính cá nhân (hoặc môi trường **AWS Cloud9**) đã cài đặt đầy đủ các công cụ sau.

### 1. Yêu cầu Tài khoản & Công cụ

1. **Tài khoản AWS (AWS Account):** Quyền `AdministratorAccess` hoặc các quyền quản trị trên các dịch vụ Cognito, API Gateway, Lambda, DynamoDB, Step Functions, SQS, SES, S3, CloudFront.
2. **AWS CLI v2:** Công cụ dòng lệnh tương tác với AWS APIs.
3. **AWS SAM CLI (Serverless Application Model):** Công cụ đóng gói, build và deploy hạ tầng Serverless.
4. **Node.js (v18 trở lên, khuyến nghị v20.x):** Môi trường chạy cho Lambda backend và React Vite frontend.
5. **Git:** Quản lý mã nguồn.

---

### 2. Kiểm tra các công cụ cài đặt

Mở Terminal (hoặc Command Prompt / Cloud9 Terminal) và chạy các câu lệnh sau để kiểm tra phiên bản:

```bash
# 1. Kiểm tra AWS CLI
aws --version

# 2. Kiểm tra AWS SAM CLI
sam --version

# 3. Kiểm tra Node.js và npm
node -v
npm -v
```

> **Lưu ý:** Kết quả trả về cần hiển thị thông tin phiên bản hợp lệ của từng công cụ.

---

### 3. Cấu hình AWS Credentials

Kiểm tra và cấu hình tài khoản AWS CLI bằng lệnh:

```bash
aws configure
```

Nhập các thông tin tương ứng:

* **AWS Access Key ID:** `[Key ID của bạn]`
* **AWS Secret Access Key:** `[Secret Key của bạn]`
* **Default region name:** `us-east-1` (hoặc `ap-southeast-1`)
* **Default output format:** `json`

Kiểm tra quyền truy cập tài khoản bằng lệnh:

```bash
aws sts get-caller-identity
```

---

### 4. Tải Mã nguồn Dự án

Tải mã nguồn dự án **Smart Attendance SaaS Platform** về máy:

```bash
git clone https://github.com/your-repo/smart-attendance-saas.git
cd smart-attendance-saas
```

Cấu trúc thư mục của dự án như sau:

```
smart-attendance-saas/
├── platform_architecture.drawio                # Sơ đồ kiến trúc hệ thống
├── backend/                   # Mã nguồn Serverless Backend & AWS SAM Template
│   ├── template.yaml          # File IaC AWS SAM quy định toàn bộ tài nguyên AWS
│   ├── src/                   # Logic các hàm Lambda (Auth, Attendance, Reports, Admin)
│   └── package.json
└── frontend/                  # Mã nguồn React SPA Dashboard & Mobile Web
    ├── src/
    └── package.json
```

Đến bước này, môi trường phát triển của bạn đã sẵn sàng cho bài lab tiếp theo!
