---
title: "Prerequisites & Environment Setup"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2 </b> "
---

# Prerequisites & Development Environment Setup

Before starting the hands-on deployment of the **Smart Attendance SaaS Platform**, ensure your workstation (or **AWS Cloud9** environment) has the following prerequisites configured.

### 1. Requirements & Tools

1. **AWS Account:** With `AdministratorAccess` permissions or administrative rights to Cognito, API Gateway, Lambda, DynamoDB, Step Functions, SQS, SES, S3, and CloudFront.
2. **AWS CLI v2:** Command-line tool for interacting with AWS services.
3. **AWS SAM CLI (Serverless Application Model):** Tool for building, testing, and deploying Serverless infrastructure.
4. **Node.js (v18+, v20.x recommended):** Runtime environment for Lambda functions and React Vite frontend.
5. **Git:** Source code version control.

---

### 2. Verify Installed Tools

Open your Terminal (or AWS Cloud9 Terminal) and execute the following commands to check tool versions:

```bash
# 1. Verify AWS CLI
aws --version

# 2. Verify AWS SAM CLI
sam --version

# 3. Verify Node.js and npm
node -v
npm -v
```

> **Note:** Each command should output a valid version string without errors.

---

### 3. Configure AWS Credentials

Initialize and verify your AWS CLI credentials:

```bash
aws configure
```

Provide your parameters when prompted:

* **AWS Access Key ID:** `[Your Access Key ID]`
* **AWS Secret Access Key:** `[Your Secret Access Key]`
* **Default region name:** `us-east-1` (or `ap-southeast-1`)
* **Default output format:** `json`

Verify your AWS IAM identity:

```bash
aws sts get-caller-identity
```

---

### 4. Clone Project Source Code

Clone the **Smart Attendance SaaS Platform** repository to your workspace:

```bash
git clone https://github.com/your-repo/smart-attendance-saas.git
cd smart-attendance-saas
```

The workspace directory structure is organized as follows:

```
smart-attendance-saas/
├── platform_architecture.drawio                # Architecture diagram
├── backend/                   # Serverless Backend & AWS SAM Template
│   ├── template.yaml          # Infrastructure as Code (IaC) defining AWS resources
│   ├── src/                   # Lambda functions logic (Auth, Attendance, Reports, Admin)
│   └── package.json
└── frontend/                  # React SPA Dashboard & Mobile Web frontend
    ├── src/
    └── package.json
```

Your environment is now completely set up for the next lab!
