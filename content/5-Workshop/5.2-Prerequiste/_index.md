---
title: "Prerequisites"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2 </b> "
---

# Environment Prerequisites & Setup

Before starting the hands-on deployment of the **Smart Attendance SaaS Platform**, ensure your local development environment or AWS Cloud9 workspace is configured with the necessary tools and credentials.

---

### 1. Required Tooling Setup

Verify that the following CLI tools are installed on your workstation:

* **AWS CLI (v2.x):** Command-line interface for communicating with AWS services.
  ```bash
  aws --version
  ```
* **AWS SAM CLI:** Tool for building, testing, and deploying Serverless applications.
  ```bash
  sam --version
  ```
* **Node.js (v20.x+) & npm:** JavaScript runtime for Lambda microservices & React SPA frontend.
  ```bash
  node -v
  npm -v
  ```
* **Git:** Source control management.
  ```bash
  git --version
  ```

---

### 2. Configure AWS Account Credentials

1. Create an IAM User with appropriate administrative permissions (`AdministratorAccess` or service permissions covering Lambda, API Gateway, DynamoDB, Cognito, S3, CloudFront, SQS, Step Functions, KMS, SES).
2. Execute the CLI configuration wizard:

```bash
aws configure
```

Provide your credentials when prompted:

```text
AWS Access Key ID [None]: AKIAXXXXXXXXXXXXXXXX
AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
Default region name [None]: us-east-1
Default output format [None]: json
```

Verify your authentication identity:

```bash
aws sts get-caller-identity
```

---

### 3. Clone Project Source Repository

Clone the project source repository into your working directory:

```bash
cd ~/Documents/AWS
git clone https://github.com/your-repo/smart-attendance-saas.git
cd smart-attendance-saas
```

Source project file structure:

```text
smart-attendance-saas/
├── backend/                  # Serverless Backend Infrastructure (AWS SAM)
│   ├── src/                  # Lambda microservice handler functions
│   ├── template.yaml         # AWS SAM Infrastructure Template
│   └── samconfig.toml        # Deployment parameter configurations
├── frontend/                 # React SPA Frontend (Vite + TailwindCSS)
│   ├── src/                  # Components and Dashboard pages
│   └── package.json          # Node dependencies
└── platform_architecture.drawio # System architecture diagram
```

You are now ready to proceed to the backend deployment module!
