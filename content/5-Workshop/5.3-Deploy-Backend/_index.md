---
title: "Deploying Serverless Backend with AWS SAM"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3 </b> "
---

# Deploying Serverless Backend with AWS SAM & Cognito

In this module, you will use **AWS SAM (Serverless Application Model)** to package and deploy the entire Serverless Backend infrastructure including **Amazon Cognito User Pool**, **HTTP API Gateway v2**, **AWS Lambda** microservices, **Amazon DynamoDB Single-Table**, and **AWS KMS Keys**.

---

### 1. Understanding the SAM Template (`template.yaml`)

The `template.yaml` file defines the Infrastructure as Code (IaC) for your entire platform:

* **Cognito User Pool (`CognitoUserPool`):** Manages sign-up, login, and JWT token issuance with Custom Attributes `tenantId` and `role` for multi-tenant isolation.
* **HTTP API Gateway (`AttendanceApi`):** Configures a `CognitoAuthorizer` enforcing JWT authentication against your Cognito User Pool issuer.
* **KMS Key (`DataKMSKey`):** Customer Managed Key (CMK) providing data-at-rest encryption for DynamoDB and S3.
* **DynamoDB Table (`SaaSAttendanceTable`):** Single-Table Design with Partition Key `PK` and Sort Key `SK` operating in On-Demand capacity mode.
* **Lambda Microservices:**
  * `AuthFunction`: Registration, login, and token verification (`/auth/*`).
  * `CheckInFunction`: Employee check-in recording (`/attendance/check-in`).
  * `CheckOutFunction`: Employee check-out recording (`/attendance/check-out`).
  * `AttendanceHistoryFunction`: Attendance history querying (`/attendance/history`).
  * `AdminFunction`: HR admin tenant & employee management (`/admin/*`).

---

### 2. Build the SAM Project

Navigate to the `backend/` folder and build your Lambda functions:

```bash
cd backend
sam build
```

Expected output:

```text
Build Succeeded

Built Artifacts  : .aws-sam/build
Valid Templates  : .aws-sam/build/template.yaml
```

---

### 3. Deploy Stack to AWS Cloud

Run guided deployment using SAM CLI:

```bash
sam deploy --guided
```

Fill in the prompt parameters:

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

CloudFormation resource creation takes approximately 2–3 minutes.

---

### 4. Verify Output Details

Once deployment completes, SAM will print the stack outputs in your terminal:

```text
Key                 AttendanceApiUrl
Description         Link API Endpoint
Value               https://xxxxxxx.execute-api.us-east-1.amazonaws.com/prod
```

> **Important:** Save the `AttendanceApiUrl` along with your `CognitoUserPoolId` and `CognitoUserPoolClientId` for configuring the frontend in upcoming steps!
