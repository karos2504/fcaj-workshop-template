---
title: "Triển khai Backend Serverless với AWS SAM"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3 </b> "
---

# Triển khai Backend Serverless với AWS SAM & Cognito

Trong phần này, bạn sẽ sử dụng **AWS SAM (Serverless Application Model)** để đóng gói và triển khai toàn bộ hạ tầng Backend Serverless bao gồm **Amazon Cognito User Pool**, **HTTP API Gateway v2**, bộ microservices **AWS Lambda**, **Amazon DynamoDB Single-Table** và **AWS KMS Keys**.

---

### 1. Phân tích AWS SAM Template (`template.yaml`)

File `template.yaml` định nghĩa toàn bộ tài nguyên hạ tầng của dự án dưới dạng mã (IaC). Hãy xem qua các thành phần cốt lõi:

* **Cognito User Pool (`CognitoUserPool`):** Quản lý đăng ký, đăng nhập và cấp mã Token JWT. Khai báo Custom Attributes `tenantId` và `role` để hỗ trợ đa doanh nghiệp (Multi-tenant).
* **HTTP API Gateway (`AttendanceApi`):** Cấu hình `CognitoAuthorizer` sử dụng chuẩn OAuth2/JWT với Issuer URL trỏ về Cognito User Pool.
* **KMS Key (`DataKMSKey`):** Khóa CMK mã hóa dữ liệu tại chỗ (Data at rest) cho DynamoDB và S3.
* **DynamoDB Table (`SaaSAttendanceTable`):** Bảng Single-Table Design với HASH Key `PK` và RANGE Key `SK`, chế độ On-Demand Billing và DynamoDB Streams (CDC enabled).
* **Lambda Microservices:**
  * `AuthFunction`: Đăng nhập, đăng ký và xác thực tài khoản (`/auth/*`).
  * `CheckInFunction`: Ghi nhận dữ liệu check-in nhân viên (`/attendance/check-in`).
  * `CheckOutFunction`: Ghi nhận dữ liệu check-out (`/attendance/check-out`).
  * `AttendanceHistoryFunction`: Truy vấn lịch sử chấm công (`/attendance/history`).
  * `AdminFunction`: Quản trị nhân sự và tổng hợp dữ liệu doanh nghiệp (`/admin/*`).
  * `ReportFunction`: Tiếp nhận yêu cầu xuất báo cáo và khởi chạy async workflow.
  * `WebhookFunction`: Xử lý webhook thanh toán B2B và thông báo hệ thống ngoài.

---

### 2. Biên dịch hạ tầng với `sam build`

Di chuyển vào thư mục `backend/` và tiến hành build mã nguồn các hàm Lambda:

```bash
cd backend
sam build
```

Kết quả báo thành công:

```text
Build Succeeded

Built Artifacts  : .aws-sam/build
Valid Templates  : .aws-sam/build/template.yaml
```

---

### 3. Triển khai hạ tầng lên AWS Cloud với `sam deploy`

Chạy câu lệnh triển khai tương tác:

```bash
sam deploy --guided
```

Nhập các tham số cấu hình:

```text
Configuring SAM deploy
======================

	Stack Name [sam-app]: smart-attendance-backend
	AWS Region [us-east-1]: us-east-1
	Parameter AllowedOrigin [https://your-cloudfront-domain.cloudfront.net]: https://localhost:3000
	Parameter OriginVerifySecret [SaaS-Secure-Verification-Token-2026]: SaaS-Secure-Verification-Token-2026
	Confirm changes before deploy [Y/n]: n
	Allow SAM CLI IAM role creation [Y/n]: Y
	Disable rollback [y/N]: N
	Save arguments to configuration file [Y/n]: Y
	SAM configuration file [samconfig.toml]: samconfig.toml
	SAM configuration environment [default]: default
```

Quá trình khởi tạo các tài nguyên CloudFormation sẽ diễn ra trong khoảng 2–3 phút.

> [!TIP]
> **Xử lý lỗi `Error: S3 Bucket does not exist`:**  
> Nếu gặp thông báo lỗi S3 Bucket chưa tồn tại khi deploy, hãy thêm cờ `--resolve-s3` để SAM CLI tự động khởi tạo mới S3 Deployment Bucket cho tài khoản AWS của bạn:
> ```bash
> sam deploy --guided --resolve-s3
> ```

---

### 4. Kiểm tra kết quả Đầu ra (Outputs)

Khi quá trình deploy kết thúc, màn hình Terminal sẽ trả về thông tin `Outputs`:

```text
Key                 AttendanceApiUrl
Description         Link API Endpoint
Value               https://xxxxxxx.execute-api.us-east-1.amazonaws.com/prod

Key                 CognitoUserPoolId
Description         Cognito User Pool ID
Value               us-east-1_xxxxxxxxx

Key                 CognitoUserPoolClientId
Description         Cognito App Client ID
Value               xxxxxxxxxxxxxxxxxxxxxxxxxx
```

> [!IMPORTANT]
> Hãy lưu lại các giá trị `AttendanceApiUrl`, `CognitoUserPoolId`, và `CognitoUserPoolClientId` để cấu hình cho ứng dụng Frontend ở bài lab tiếp theo!
