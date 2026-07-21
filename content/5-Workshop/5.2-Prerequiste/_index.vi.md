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

### 2. Hướng dẫn chi tiết Tạo IAM User & Khởi tạo Access Keys

Để đảm bảo nguyên tắc bảo mật, không bao giờ dùng tài khoản Root (Root Account) để thực hành bài lab. Bạn sẽ tạo một **IAM User** dành riêng cho việc quản trị và triển khai tài nguyên theo các bước sau:

#### Bước 2.1: Tạo IAM User trên AWS Management Console
1. Đăng nhập vào [AWS IAM Console](https://console.aws.amazon.com/iam/).
2. Tại menu bên trái, chọn **Users** ➔ Bấm nút **Create user**.
3. Điền thông tin User:
   * **User name:** `WorkshopAdmin` (hoặc tên tùy chọn).
   * **Provide user access to the AWS Management Console:** *Có thể tích chọn nếu muốn cho phép User đăng nhập giao diện Web Console*.
4. Bấm **Next**.

#### Bước 2.2: Gán Quyền (Permissions)
1. Tại phần **Permissions options**, chọn **Attach policies directly**.
2. Tìm kiếm và tích chọn policy: `AdministratorAccess` *(Quyền quản trị tối thiểu cần thiết để SAM CLI tạo các tài nguyên CloudFormation, IAM Roles, Lambda, DynamoDB, API Gateway, Cognito, S3, CloudFront, SQS, Step Functions...)*.
3. Bấm **Next** ➔ Kiểm tra lại thông tin ➔ Bấm **Create user**.

#### Bước 2.3: Tạo Access Key ID & Secret Access Key cho AWS CLI
1. Nhấp vào tên User vừa tạo (`WorkshopAdmin`) trong danh sách **Users**.
2. Chọn tab **Security credentials**.
3. Cuộn xuống phần **Access keys** ➔ Bấm nút **Create access key**.
4. Chọn mục đích sử dụng: **Command Line Interface (CLI)**.
5. Tích chọn vào ô cam kết *"I understand the above recommendation and want to proceed to create an access key."* ➔ Bấm **Next**.
6. (Tùy chọn) Nhập mô tả Tag (ví dụ: `AWS CLI for Workshop`) ➔ Bấm **Create access key**.
7. **LƯU Ý QUAN TRỌNG:** Tải file `.csv` chứa **Access Key ID** và **Secret Access Key** về máy hoặc sao chép ngay. *(Bạn sẽ không thể xem lại Secret Access Key sau khi đóng cửa sổ này)*.

---

### 3. Cấu hình Tài khoản AWS CLI trên Máy tính

Sau khi có Access Key, mở Terminal và chạy lệnh cấu hình credentials:

```bash
aws configure
```

Nhập các thông tin đã tạo ở Bước 2.3:

```text
AWS Access Key ID [None]: AKIAXXXXXXXXXXXXXXXX
AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
Default region name [None]: ap-southeast-1
Default output format [None]: json
```

Kiểm tra kết nối tài khoản thành công:

```bash
aws sts get-caller-identity
```

Kết quả trả về dạng JSON hiển thị `UserId` và `Arn` của `WorkshopAdmin` là bạn đã cấu hình thành công!

---

### 4. Tải Mã nguồn Dự án (Source Code)

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
