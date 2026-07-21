---
title: "Asynchronous Reporting Workflow"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5 </b> "
---

# Building Asynchronous Reporting Workflows with Step Functions, SQS & SES

In large enterprise applications, generating monthly attendance reports for thousands of employees can require significant computation time (10–60 seconds). Processing these synchronously over API Gateway causes **HTTP Timeouts (30s limit)** and freezes the frontend user interface.

In this lab, you will learn how to design a decoupled asynchronous architecture combining an **AWS Step Functions Express State Machine**, **Amazon SQS Queue Buffers**, **Amazon S3**, and an **Amazon SES Email Worker**.

---

### 1. Asynchronous Report Processing Architecture

```
[Admin Request] ➔ [API Gateway] ➔ [SQS ReportQueue] ➔ [Step Functions Engine]
                                                               │
                                                               ▼
[Amazon SES Email] ◄─ [Lambda Email Worker] ◄─ [Amazon S3 Bucket (Report PDF/Excel)]
```

1. **Trigger Request:** The HR admin clicks "Export Monthly Report". The React frontend dispatches an HTTP POST request. API Gateway pushes the payload into the **SQS ReportQueue** and immediately returns `202 Accepted` to the client.
2. **Workflow Execution:** An **AWS Step Functions Express State Machine (`ReportStateMachine`)** consumes tasks from SQS, executing a 5-step state workflow:
   * `ValidateRequest`: Validates input parameters (`tenantId` and `yearMonth`).
   * `InitializeReportStatus`: Sets execution status to `PROCESSING` in DynamoDB.
   * `GenerateReportFile`: Invokes Lambda microservice to calculate monthly metrics and compile Excel/PDF files.
   * `WriteFileToS3`: Writes the binary payload to an **Amazon S3 Bucket (`SaaSReportBucket`)** encrypted via KMS CMK with **S3 Intelligent-Tiering** lifecycle rules.
   * `FinalizeReportStatus`: Updates state to `COMPLETED` and saves the S3 object key in DynamoDB.
3. **Event Publishing & Delivery:** EventBridge picks up the `ReportGenerated` event and forwards an email job to **SQS EmailQueue**. The **Lambda Email Worker** processes messages in batches and calls **Amazon SES** to email secure download links directly to the admin.

---

### 2. AWS Step Functions State Machine Definition (`template.yaml`)

Below is the declarative SAM definition for the Express State Machine:

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

### 3. SQS Queue & Dead Letter Queue (DLQ) Setup

To guarantee zero email notification loss during network anomalies or SES rate-limits, the system relies on a **Dead Letter Queue (DLQ)** pattern:

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

> **Note:** If `EmailWorkerFunction` encounters execution errors 3 times (`maxReceiveCount: 3`), the message is automatically redirected to `EmailDLQ` for administrator inspection.
