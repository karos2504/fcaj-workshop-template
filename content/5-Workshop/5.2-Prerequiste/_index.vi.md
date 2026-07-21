---
title: "Chuẩn bị môi trường"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2 </b> "
---

# Chuẩn bị Môi trường Triển khai

Để bắt đầu chuỗi thực hành triển khai dự án **Smart Attendance SaaS Platform**, bạn cần chuẩn bị các công cụ và cấu hình môi trường dưới đây trên máy tính cá nhân hoặc môi trường AWS Cloud9.

---

### 1. Yêu cầu Cài đặt Công cụ (Prerequisites)

Hãy đảm bảo máy tính của bạn đã được cài đặt các công cụ lệnh sau:

* **AWS CLI (v2.x):** Công cụ dòng lệnh giao tiếp với tài nguyên AWS Cloud.
  ```bash
  aws --version
  ```
* **AWS SAM CLI:** Công cụ xây dựng và đóng gói ứng dụng Serverless.
  ```bash
  sam --version
  ```
* **Node.js (v20.x trở lên) & npm:** Môi trường thực thi JavaScript cho Lambda microservices & React SPA.
  ```bash
  node -v
  npm -v
  ```
* **Git:** Quản lý mã nguồn.
  ```bash
  git --version
  ```

---

### 2. Cấu hình Tài khoản AWS & Credentials

1. Tạo một tài khoản AWS (nếu chưa có) và khởi tạo một người dùng IAMUser có quyền quản trị tối thiểu cho bài lab (`AdministratorAccess` hoặc các quyền dịch vụ bao gồm Lambda, API Gateway, DynamoDB, Cognito, S3, CloudFront, SQS, Step Functions, KMS, SES).
2. Chạy câu lệnh cấu hình AWS CLI credentials:

```bash
aws configure
```

Nhập các thông tin tương ứng:

```text
AWS Access Key ID [None]: AKIAXXXXXXXXXXXXXXXX
AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
Default region name [None]: us-east-1
Default output format [None]: json
```

Kiểm tra kết nối thành công:

```bash
aws sts get-caller-identity
```

---

### 3. Tải Mã nguồn Dự án (Source Code)

Clone repository mã nguồn dự án `smart-attendance-saas` về máy local:

```bash
cd ~/Documents/AWS
git clone https://github.com/your-repo/smart-attendance-saas.git
cd smart-attendance-saas
```

Cấu trúc thư mục mã nguồn bao gồm:

```text
smart-attendance-saas/
├── backend/                  # Mã nguồn Serverless Backend (AWS SAM)
│   ├── src/                  # Các hàm Lambda microservices
│   ├── template.yaml         # AWS SAM Infrastructure Template
│   └── samconfig.toml        # Cấu hình tham số deployment
├── frontend/                 # Mã nguồn React SPA Frontend (Vite + Tailwind)
│   ├── src/                  # Components và giao diện Dashboard
│   └── package.json          # Quản lý dependencies
└── platform_architecture.drawio # Sơ đồ kiến trúc hệ thống
```

Bạn đã sẵn sàng để bước sang bài thực hành tiếp theo!
