---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Smart Attendance SaaS Platform

## Giải pháp Nền tảng Chấm công Đa doanh nghiệp (Multi-Tenant) dựa trên Kiến trúc AWS Serverless Toàn diện

### 1. Tóm tắt điều hành

**Smart Attendance SaaS Platform** là nền tảng quản lý điểm danh, chấm công và quản trị nhân sự đám mây thiết kế chuẩn SaaS (Software-as-a-Service) dành cho các doanh nghiệp vừa và nhỏ (SMEs) cũng như các tập đoàn đa chi nhánh. Hệ thống cho phép hàng trăm doanh nghiệp (**Tenants**) vận hành trên hạ tầng đám mây dùng chung nhưng đảm bảo tuyệt đối khả năng **Cô lập dữ liệu (Tenant Data Isolation)**, phản hồi thời gian thực dưới 200ms và khả năng tự động mở rộng (Elastic Auto-scaling) khi có hàng ngàn yêu cầu điểm danh đồng thời vào khung giờ cao điểm.

Bằng cách tận dụng 100% hệ sinh thái **AWS Serverless** (bao gồm *Amazon CloudFront, AWS WAF v2, AWS Shield, Amazon Cognito, Amazon API Gateway, AWS Lambda, AWS Step Functions, Amazon DynamoDB, Amazon S3, Amazon EventBridge, Amazon SQS, Amazon SES, AWS KMS, AWS Secrets Manager*), hệ thống loại bỏ hoàn toàn chi phí bảo trì máy chủ, tối ưu chi phí hạ tầng ở mức gần như bằng 0 khi không có lượt truy cập (Pay-as-you-go) và đạt độ sẵn sàng cao (**High Availability 99.99%**).

---

### 2. Tuyên bố vấn đề

#### Vấn đề hiện tại

* **Chấm công thủ công và nghẽn mạng giờ cao điểm:** Các doanh nghiệp truyền thống sử dụng máy chấm công vân tay/thẻ từ hoặc file Excel thủ công. Vào các khung giờ cao điểm (7:45 AM - 8:15 AM), hàng ngàn nhân viên đồng thời điểm danh gây ra điểm nghẽn (bottleneck), quá tải API và đơ lag hệ thống.
* **Chi phí hạ tầng và bảo trì cao:** Việc tự triển khai hệ thống chấm công trên máy chủ truyền thống (EC2 / RDS / On-Premise) đòi hỏi chi phí đầu tư ban đầu lớn, chi phí duy trì máy chủ 24/7 dù ngoài giờ làm việc hệ thống không có lưu lượng sử dụng.
* **Thách thức Multi-Tenancy và Bảo mật:** Các giải pháp phần mềm thông thường dễ gặp rủi ro rò rỉ dữ liệu giữa các công ty (Cross-tenant data leakage) nếu không được thiết kế kiến trúc phân tách phân vùng dữ liệu (Partition Key Isolation) và phân quyền chặt chẽ từ tầng API.
* **Thiếu khả năng tự động hóa báo cáo và cảnh báo:** Việc tổng hợp và xuất báo cáo bảng công hàng tháng tốn nhiều thời gian xử lý thủ công của phòng HR, dễ sai sót và không tích hợp tự động với email notification hay webhook hệ thống bên thứ ba.

#### Giải pháp đề xuất

Nền tảng **Smart Attendance SaaS** giải quyết triệt để các bài toán trên thông qua kiến trúc **AWS Serverless Optimized Pro**:

1. **Edge & API Protection Layer:** Sử dụng **Amazon CloudFront** kết hợp **AWS WAF v2** và **AWS Shield** để phân phối ứng dụng React SPA, chặn truy cập trái phép, rate-limit chống tấn công DDoS/Botnet và bảo mật đường truyền API bằng Token xác thực độc quyền (`x-origin-verify`).
2. **Multi-tenant Identity Management:** **Amazon Cognito User Pool** quản lý xác thực người dùng tích hợp sẵn Custom Attributes (`tenantId`, `role`, `userId`), hỗ trợ xác thực 2 yếu tố (TOTP MFA) và Advanced Security Mode.
3. **High-Performance Compute & Microservices:** Bộ hàm **AWS Lambda** (Auth, Check-in, Check-out, Attendance History, Admin Management, Export Report API, Webhook, Subscription) xử lý song song không trạng thái (stateless), tự động mở rộng theo nhu cầu cao điểm.
4. **Single-Table Design Database:** **Amazon DynamoDB** lưu trữ toàn bộ dữ liệu (Attendance, Users, Tenants) trong 1 bảng duy nhất (Single-Table Design) với Partition Key `TENANT#<tenantId>`, mang lại tốc độ truy xuất dưới 10ms và bảo mật cô lập tuyệt đối dữ liệu doanh nghiệp.
5. **Asynchronous Reporting Engine:** Kết hợp **AWS Step Functions Express Workflow** và **Amazon SQS** để xử lý tạo báo cáo PDF/Excel/CSV bất đồng bộ, lưu trữ trên **Amazon S3 (Intelligent-Tiering)** và tự động gửi mail báo cáo qua **Amazon SES**.

#### Lợi ích và Hoàn vốn đầu tư (ROI)

* **Tối ưu chi phí đến 90%:** Kiến trúc Serverless giúp doanh nghiệp chỉ trả tiền cho số lượng request và thời gian thực thi thực tế. Chi phí hạ tầng cho quy mô 100 Tenants (5,000 nhân viên) chỉ khoảng **~$9.93 USD/tháng**, cực kỳ tiết kiệm so với việc vận hành máy chủ EC2/RDS 24/7 ($120 - $150 USD/tháng).
* **Khả năng mở rộng vô hạn (Elastic Scalability):** Hệ thống có khả năng đáp ứng mượt mà từ vài chục đến hàng trăm ngàn lượt check-in mỗi phút trong khung giờ cao điểm mà không cần can thiệp thủ công.
* **Thời gian hoàn vốn (ROI):** Tiết kiệm 95% thời gian tổng hợp bảng công hàng tháng của bộ phận HR, đồng thời các nhà cung cấp SaaS có thể thu hồi vốn đầu tư chỉ sau 2-3 tháng vận hành thương mại.

---

### 3. Kiến trúc giải pháp

Nền tảng áp dụng mô hình kiến trúc **AWS Serverless Multi-Layered Architecture** hoàn chỉnh:

![Smart Attendance SaaS Architecture](/images/2-Proposal/platform_architecture.png)

#### Các tầng dịch vụ AWS sử dụng

| Tầng Kiến Trúc | Dịch Vụ AWS | Vai Trò & Chức Năng Chi Tiết |
| :--- | :--- | :--- |
| **Global Edge Layer** | Amazon Route 53 | Quản lý DNS resolution toàn cầu, định tuyến tên miền chính xác. |
| | AWS WAF v2 | Bảo vệ API & Web trước DDoS, Rate Limiting (1000 req/IP), chặn Bot & OWASP Top 10. |
| | AWS Shield | Bảo vệ chống tấn công DDoS tầng 3/4 tự động. |
| | Amazon CloudFront | CDN toàn cầu phân phối React SPA và mã hóa/proxy bảo mật cho API Gateway với Custom Header Verification. |
| **Auth & Ingress Layer** | Amazon Cognito | Quản lý người dùng, JWT Token gắn kèm context `{tenantId, role, userId}`, TOTP MFA. |
| | Amazon API Gateway | HTTP API v2 với Cognito JWT Authorizer, xác thực Header bảo mật từ CloudFront. |
| | AWS Secrets Manager | Quản lý và tự động xoay vòng (Auto-rotation) Webhook API Keys & Credentials. |
| **Compute Layer** | AWS Lambda | Xử lý logic microservices (Auth, Check-in/out, History, Admin, Export Report API, Billing, Webhook). |
| | AWS Step Functions | Điều phối Express Workflow bất đồng bộ phức tạp cho công tác tạo báo cáo hàng loạt. |
| **Data & Storage Layer** | Amazon DynamoDB | Lưu trữ NoSQL Single-Table Design, mã hóa KMS CMK, bật DynamoDB Streams (CDC). |
| | Amazon S3 | Lưu trữ React SPA & file Báo cáo (PDF/Excel/CSV) với chế độ Intelligent-Tiering và Force SSL policy. |
| **Event & Messaging** | Amazon EventBridge | EventBus & EventBridge Pipe định tuyến sự kiện CDC từ DynamoDB Streams (`AttendanceCreated`, `ReportGenerated`). |
| | Amazon SQS | Hàng chờ thông báo & Email Queue kèm Dead Letter Queue (DLQ) đảm bảo không mất tin. |
| | Amazon SES | Gửi email tự động chứa báo cáo, cảnh báo điểm danh và hóa đơn thanh toán. |
| **Operations & Security** | AWS KMS | Quản lý khóa mã hóa dữ liệu Customer Managed Keys (CMK) cho DynamoDB, S3, SQS. |
| | Amazon CloudWatch | Thu thập Log, Metrics, thiết lập Dashboard và Alarms cảnh báo sự cố API/Lambda tự động. |
| | AWS X-Ray | Distributed Tracing giám sát hiệu năng và thời gian phản hồi end-to-end. |
| | AWS Security Hub & Inspector | Quản trị an ninh hạ tầng, phát hiện lỗ hổng và cảnh báo mối đe dọa (GuardDuty). |
| | CodePipeline & CodeBuild | Quy trình CI/CD tự động hóa kiểm thử, build artifact và deploy qua AWS SAM/CloudFormation. |

#### Quy trình vận hành & Dòng dữ liệu (16-Step Process Flow)

Dựa trên sơ đồ kiến trúc `platform_architecture.drawio`, luồng dữ liệu hoạt động theo 16 bước được mã hóa chi tiết:

1. **DNS Resolution (`1`):** Người dùng gửi yêu cầu DNS qua **Amazon Route 53**.
2. **HTTPS Ingress (`2`):** Yêu cầu HTTPS đến **Amazon CloudFront**, được bảo vệ bởi **AWS WAF v2** & **AWS Shield**.
3. **Static Content (`3`):** Web App (React SPA) được tải trực tiếp từ **Amazon S3** thông qua CloudFront CDN.
4. **Authentication (`4`):** Người dùng/Mobile App đăng nhập qua **Amazon Cognito**, nhận về Cognito JWT Token mang thông tin `{tenantId, role, userId}`.
5. **API Proxy Path (`4a` & `5`):** Yêu cầu API gửi kèm JWT Token và Secret Header `x-origin-verify` từ CloudFront đến **API Gateway**.
6. **API Gateway Execution (`6`):** API Gateway kiểm tra JWT Authorizer & Header, sau đó kích hoạt hàm **AWS Lambda** tương ứng (Check-in, Check-out, History).
7. **Async Report Request (`7`):** Khi yêu cầu xuất báo cáo lớn, request được đẩy vào **Amazon SQS Queue** để giải phóng giao diện lập tức.
8. **CDC Capture (`8a` & `8b`):** **DynamoDB Streams** ghi nhận biến động dữ liệu (Change Data Capture) và đẩy sang **EventBridge Pipe** tới **Amazon EventBridge**.
9. **Workflow Execution (`9`):** **AWS Step Functions Engine** nhận request từ SQS, điều phối các hàm Lambda tạo file báo cáo chi tiết.
10. **Transactional Data Ops (`10`):** Lambda trực tiếp ghi/đọc dữ liệu vào **Amazon DynamoDB** theo chuẩn Single-Table Design với Partition Key `TENANT#<tenantId>`.
11. **Report Storage (`11`):** File báo cáo (PDF, Excel, CSV) được lưu vào **Amazon S3 Bucket** (cấu hình S3 Intelligent-Tiering để tối ưu chi phí).
12. **Notification Event (`12` & `13`):** EventBridge kích hoạt đẩy thông báo vào **SQS Email Queue**, hàm **Lambda Email Worker** tiêu thụ tin nhắn theo lô (batch).
13. **Secured Email Delivery (`14`):** Lambda Email Worker gọi **Amazon SES** để gửi mail kèm link tải báo cáo an toàn cho người dùng.
14. **Outbound Webhook (`15`):** **Lambda Webhook** gửi cảnh báo thời gian thực đến các hệ thống bên ngoài (Slack, Teams, HRM).
15. **B2B Billing Integration (`16` & `16a`):** **Lambda Subscription** tương tác với Cổng thanh toán (Payment Gateway). Khi thanh toán hoàn tất, Webhook trả về API Gateway (`16a`) để cập nhật trạng thái doanh nghiệp.

---

### 4. Triển khai kỹ thuật

#### Các giai đoạn triển khai

Dự án được triển khai theo 4 giai đoạn chuẩn hóa:

1. **Giai đoạn 1: Thiết kế Kiến trúc & Data Model (Tuần 1–2)**
   * Thiết kế Single-Table Design trên DynamoDB (Access Patterns: Employee Check-in, Check-out, Monthly Summary, Tenant Admin Query).
   * Cấu hình Cognito User Pool, Custom Attributes (`tenantId`, `role`) và Security Policies.
   * Lập sơ đồ kiến trúc tổng thể và luồng bảo mật trên CloudFront + WAF v2 + API Gateway.
2. **Giai đoạn 2: Xây dựng Core Serverless Backend với AWS SAM (Tuần 3–5)**
   * Đóng gói hạ tầng dưới dạng mã (IaC) sử dụng **AWS SAM / CloudFormation** (`template.yaml`).
   * Lập trình các hàm Lambda (Node.js 20) cho Auth, Check-in/out, History, Admin, Report Export API, Webhook.
   * Cấu hình EventBridge Pipe, SQS Queue, SQS Email DLQ và Step Functions Express Workflows.
3. **Giai đoạn 3: Phát triển Frontend React SPA & CloudFront Integration (Tuần 6–7)**
   * Xây dựng giao diện Dashboard cho Admin và Employee Web App bằng React + Vite + TailwindCSS.
   * Tích hợp Cognito SDK cho Đăng nhập/Đăng ký, Refresh Token và phân quyền vai trò.
   * Đóng gói static site và triển khai lên S3 Bucket + CloudFront Distribution với Secret Origin Verification Header.
4. **Giai đoạn 4: Kiểm thử, Bảo mật, CI/CD & Đưa vào Vận hành (Tuần 8)**
   * Xây dựng luồng CI/CD với **AWS CodePipeline** và **AWS CodeBuild** (quét lỗ hổng với Amazon Inspector).
   * Kiểm thử tải (Load Testing) giả lập 10,000 lượt check-in đồng thời trong 1 phút.
   * Đánh giá an ninh hạ tầng với **AWS Security Hub**, bật theo dõi **AWS X-Ray** & **CloudWatch Alarms**.

#### Yêu cầu kỹ thuật & Công nghệ

* **Frontend:** React.js, Vite, TailwindCSS, AWS Amplify/Cognito JS SDK.
* **Backend:** Node.js 20.x (Runtime AWS Lambda), AWS SAM (Serverless Application Model), AWS SDK v3.
* **Database:** Amazon DynamoDB (Single-Table Design, On-Demand Capacity Mode, DynamoDB Streams).
* **Storage & CDN:** Amazon S3 (Static Web & Report Storage), Amazon CloudFront (Edge Network, TLS 1.3).
* **Security & Auth:** Amazon Cognito, AWS WAF v2, AWS KMS (CMK), AWS Secrets Manager.
* **Orchestration & Events:** AWS Step Functions, Amazon EventBridge, Amazon SQS.

---

### 5. Lộ trình & Mốc triển khai

```
+-----------------------------------------------------------------------------------+
| Tháng 1: Khảo sát & Kế hoạch    | Tháng 2: Triển khai Backend & Data              |
| - Chốt yêu cầu & Data Schema    | - Xây dựng AWS SAM Template                     |
| - Thiết kế OpenAPI & Cognito    | - Lập trình Lambda Microservices & DynamoDB     |
+---------------------------------+-------------------------------------------------+
| Tháng 3: Frontend & Integration | Tháng 4: Testing, Security & Go-Live            |
| - Phát triển React Dashboard    | - Load test cao điểm, Audit AWS Security Hub    |
| - Kết nối API Gateway & SES     | - Thiết lập CI/CD CodePipeline & Chạy chính thức|
+-----------------------------------------------------------------------------------+
```

* **Mốc 1 (Cuối Tháng 1):** Hoàn tất bản vẽ kiến trúc chi tiết, SAM template mẫu và Cognito User Pool.
* **Mốc 2 (Cuối Tháng 2):** Hoàn thành bộ API Backend (Check-in/out, Báo cáo, Webhook) và DynamoDB Single-Table.
* **Mốc 3 (Cuối Tháng 3):** Hoàn thiện Web Dashboard cho Admin/HR và Employee App.
* **Mốc 4 (Cuối Tháng 4):** Đưa toàn bộ hệ thống lên môi trường Production trên AWS Cloud.

---

### 6. Phân tích Chi phí & ROI

#### Chi phí Hạ tầng Hàng tháng (Ước tính cho 100 Tenants ~ 5,000 Nhân viên)

| Dịch Vụ AWS | Mức Sử Dụng Thực Tế | Chi Phí Ước Tính (USD/Tháng) |
| :--- | :--- | :--- |
| **Amazon Cognito** | 5,000 MAUs (Free Tier 50,000 MAUs) | **$0.00** |
| **Amazon API Gateway** | 3,000,000 HTTP Requests/tháng | **$3.00** |
| **AWS Lambda** | 3,000,000 invocations (128MB RAM, avg 100ms) | **$0.60** |
| **Amazon DynamoDB** | On-Demand (Storage 5GB, 3M Writes, 6M Reads) | **$4.25** |
| **Amazon S3** | 10GB Reports & Web Assets (Intelligent-Tiering) | **$0.23** |
| **Amazon CloudFront** | 50GB Data Transfer Out (Free Tier 1TB/month) | **$0.00** |
| **AWS Step Functions** | 10,000 Express Executions | **$0.05** |
| **Amazon SQS & SES** | 10,000 emails sent | **$1.00** |
| **AWS KMS & Secrets Manager** | 1 CMK Key & Secrets | **$0.80** |
| **TỔNG CHI PHÍ HẠ TẦNG** | | **~$9.93 USD/tháng** |

> [!TIP]
> **Hiệu quả đầu tư (ROI):** So với giải pháp hạ tầng truyền thống duy trì máy chủ EC2/RDS 24/7 (khoảng **$120 - $150 USD/tháng**), giải pháp AWS Serverless giúp doanh nghiệp tiết kiệm **hơn 90% chi phí vận hành hạ tầng**.
