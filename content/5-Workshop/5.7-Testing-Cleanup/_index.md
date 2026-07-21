---
title: "End-to-End Testing & Resource Cleanup"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.7 </b> "
---

# End-to-End Testing & AWS Resource Cleanup

Congratulations on building and deploying the entire **Smart Attendance SaaS Platform**! In this final section, you will validate the system through end-to-end testing scenarios and clean up all deployed AWS resources to avoid unnecessary cloud charges.

---

### 1. End-to-End (E2E) Testing Scenarios

Validate the platform across 5 real-world production scenarios using your web browser:

#### Scenario 1: Multi-Tenant Tenant Registration & Login

1. Open the Web Application in your browser using the CloudFront CDN domain URL.
2. Click **Register Tenant**. Enter your organization info (`tenantId`: `tenant-company-a`), Admin Email, and Password.
3. Retrieve the email verification OTP sent by Cognito/SES and confirm registration.
4. Log into the platform with your newly created Admin credentials. Observe the Admin Dashboard rendering claims matching `tenant-company-a`.

#### Scenario 2: Employee Clock-In / Clock-Out

1. Create a new Employee account (`user-employee-1`) assigned to `tenant-company-a`.
2. Sign in as the employee on a mobile browser or developer tools simulator.
3. Click **Check-in** -> The client issues an API call carrying the Cognito JWT to API Gateway -> `CheckInFunction` Lambda logs the timestamp in DynamoDB in under 200ms.
4. Click **Check-out** -> The system updates the clock-out timestamp in DynamoDB.

#### Scenario 3: Attendance History Querying

1. Open the **Attendance History** view.
2. The client triggers a query against DynamoDB filtered by Partition Key `TENANT#tenant-company-a`. Real-time records render in under 50ms.

#### Scenario 4: Asynchronous Report Generation & Delivery

1. From the Admin Dashboard, select **Export Monthly Report** -> Click **Generate Report**.
2. The UI instantly displays "Processing request...".
3. Open the AWS Step Functions Console to monitor the `ReportStateMachine` Express Workflow executing its task states.
4. Check your inbox for an automated email dispatched via **Amazon SES** containing a secure download link for the Excel/PDF file stored in S3.

#### Scenario 5: B2B Subscription Billing & Webhook Processing

1. Navigate to Subscription Settings -> Select Pro Plan -> Click **Pay**.
2. Simulate a payment gateway callback posting a payload to `/billing/webhook`.
3. `WebhookFunction` validates the webhook signature against secrets stored in **AWS Secrets Manager** and updates the tenant status to `ACTIVE` in DynamoDB.

---

### 2. Cleaning Up AWS Resources

To avoid incurring ongoing charges for AWS resources, execute the following teardown steps:

#### Step 1: Empty S3 Buckets

S3 buckets containing objects cannot be deleted directly by CloudFormation. Empty the bucket contents via AWS CLI:

```bash
# 1. Empty S3 Report Bucket
aws s3 rm s3://saas-attendance-reports-<AWS_ACCOUNT_ID>-<REGION> --recursive

# 2. Empty S3 SPA Hosting Bucket
aws s3 rm s3://smart-attendance-spa-hosting-<AWS_ACCOUNT_ID> --recursive
```

#### Step 2: Delete Stack via AWS SAM CLI

Navigate to the `backend/` directory and execute SAM teardown:

```bash
cd backend
sam delete
```

Confirm stack deletion when prompted:

```text
Are you sure you want to delete the stack smart-attendance-backend in region us-east-1? [y/N]: y
Are you sure you want to delete the folder smart-attendance-backend in S3? [y/N]: y
```

CloudFormation will automatically deprovision all 18+ AWS infrastructure resources (Cognito, API Gateway, Lambda, DynamoDB, Step Functions, SQS, SES, KMS Keys) in 3–5 minutes.

---

### Conclusion

Congratulations on completing the **Smart Attendance SaaS Platform Workshop**! You have mastered production-grade **AWS Serverless** architectural patterns and hands-on cloud application development.
