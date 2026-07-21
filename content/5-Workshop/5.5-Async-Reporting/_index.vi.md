---
title: "Workflow Xuất Báo cáo Bất đồng bộ"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5 </b> "
---

# Xây dựng Workflow Xuất Báo cáo Bất đồng bộ với Step Functions, SQS & SES

Trong các ứng dụng doanh nghiệp lớn, việc tổng hợp báo cáo chấm công hàng tháng cho hàng ngàn nhân viên có thể tốn từ 10–60 giây tính toán. Nếu xử lý đồng bộ qua API Gateway, client sẽ bị **HTTP Timeout (30s limit)** và làm nghẽn giao diện người dùng.

Trong bài lab này, bạn sẽ tìm hiểu giải pháp xử lý bất đồng bộ kết hợp **AWS Step Functions Express State Machine**, **Amazon SQS Queue Buffer**, **Amazon S3** và **Amazon SES Email Worker**.

---

### 1. Luồng xử lý Báo cáo Bất đồng bộ (Async Flow)

```
[Admin Request] ➔ [API Gateway] ➔ [SQS ReportQueue] ➔ [Step Functions Engine]
                                                               │
                                                               ▼
[Amazon SES Email] ◄─ [Lambda Email Worker] ◄─ [Amazon S3 Bucket (Report PDF/Excel)]
```

1. **Gửi yêu cầu (Trigger):** Admin bấm "Xuất Báo Cáo Tháng". Frontend gửi HTTP POST tới API Gateway. Request lập tức được đẩy vào **SQS ReportQueue** và API trả về ngay phản hồi `202 Accepted` (UI không bị treo).
2. **Khởi chạy State Machine:** **AWS Step Functions Express Workflow (`ReportStateMachine`)** tiêu thụ yêu cầu từ SQS và kích hoạt luồng 5 bước:
   * `ValidateRequest`: Kiểm tra tính hợp lệ của tham số `yearMonth` và `tenantId`.
   * `InitializeReportStatus`: Cập nhật trạng thái `PROCESSING` vào DynamoDB.
   * `GenerateReportFile`: Gọi hàm Lambda đọc lịch sử chấm công trong tháng và tạo file Excel/PDF.
   * `WriteFileToS3`: Lưu file trực tiếp vào **Amazon S3 Bucket (`SaaSReportBucket`)** mã hóa KMS CMK với chế độ Lifecycle **S3 Intelligent-Tiering**.
   * `FinalizeReportStatus`: Cập nhật trạng thái `COMPLETED` và link S3 Key vào DynamoDB.
3. **Phát sự kiện & Gửi Mail:** EventBridge ghi nhận sự kiện `ReportGenerated`, đẩy thông báo vào **SQS EmailQueue**. Hàm **Lambda Email Worker** tiêu thụ message và gọi **Amazon SES** để gửi mail chứa đường dẫn tải báo cáo bảo mật tới Admin.

---

### 2. Định nghĩa AWS Step Functions State Machine (`template.yaml`)

Dưới đây là đoạn mã định nghĩa Express State Machine trong AWS SAM:

```yaml
ReportStateMachine:
  Type: AWS::Serverless::StateMachine
  Properties:
    Type: EXPRESS
    Role: !GetAtt ReportWorkflowRole.Arn
    Definition:
      StartAt: ValidateRequest
      States:
        ValidateRequest:
          Type: Pass
          ResultPath: "$.validation"
          Next: InitializeReportStatus
        InitializeReportStatus:
          Type: Task
          Resource: arn:aws:states:::dynamodb:putItem
          Parameters:
            TableName: !Ref SaaSAttendanceTable
            Item:
              PK: { S.$: '$.PK' }
              SK: { S.$: '$.SK' }
              Status: { S: "PROCESSING" }
          Next: GenerateReportFile
        GenerateReportFile:
          Type: Pass
          Result:
            S3Key: "reports/monthly-attendance-report.xlsx"
          ResultPath: "$.fileDetails"
          Next: WriteFileToS3
        WriteFileToS3:
          Type: Task
          Resource: arn:aws:states:::aws-sdk:s3:putObject
          Parameters:
            Bucket: !Ref SaaSReportBucket
            Key.$: '$.fileDetails.S3Key'
            Body: "Report Binary Content"
          Next: FinalizeReportStatus
        FinalizeReportStatus:
          Type: Task
          Resource: arn:aws:states:::dynamodb:updateItem
          Parameters:
            TableName: !Ref SaaSAttendanceTable
            Key:
              PK: { S.$: '$.PK' }
              SK: { S.$: '$.SK' }
            UpdateExpression: "SET #status = :val, #file = :file"
            ExpressionAttributeNames:
              "#status": "Status"
              "#file": "ReportFileKey"
            ExpressionAttributeValues:
              ":val": { S: "COMPLETED" }
              ":file": { S.$: '$.fileDetails.S3Key' }
          End: true
```

---

### 3. Cấu hình SQS Queue và Email Dead Letter Queue (DLQ)

Để đảm bảo không bị mất email thông báo trong trường hợp dịch vụ SES hoặc mạng gặp sự cố, hệ thống sử dụng cơ chế **Dead Letter Queue (DLQ)**:

```yaml
EmailDLQ:
  Type: AWS::SQS::Queue
  Properties:
    QueueName: smart-attendance-email-dlq

EmailQueue:
  Type: AWS::SQS::Queue
  Properties:
    QueueName: smart-attendance-email-queue
    VisibilityTimeout: 30
    RedrivePolicy:
      deadLetterTargetArn: !GetAtt EmailDLQ.Arn
      maxReceiveCount: 3
```

> **Giải thích:** Nếu hàm `EmailWorkerFunction` xử lý lỗi quá 3 lần (`maxReceiveCount: 3`), tin nhắn sẽ tự động được chuyển sang `EmailDLQ` để quản trị viên kiểm tra và xử lý sau.
