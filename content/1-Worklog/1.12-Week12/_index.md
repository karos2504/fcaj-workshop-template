---
title: "Week 12 Worklog"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.12. </b> "
---

### Week 12 Objectives

* Design and implement Phase 1 of the Capstone Project: **SaaS Timekeeping Platform (Multi-Tenant AWS Serverless Architecture)** aligned with the authoritative `Demo.drawio` architecture specification.
* Program infrastructure using AWS CDK (TypeScript/Python): Provision VPC Private Subnets, CloudFront CDN, Route 53, AWS WAF v2, Amazon Cognito Auth & API Gateway HTTP API v2.
* Construct core application layers: DynamoDB Single-Table Design (tenant data isolation), business AWS Lambda functions (Check-in, Check-out, Attendance, Admin, Subscription), AWS Step Functions Workflow for async report generation, and Event-Driven Notification Bus.

### Tasks to be carried out this week

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | - **Architecture Analysis & System Design:** <br>&emsp; + Analyze `Demo.drawio` architecture specification for **SaaS Timekeeping Platform** <br>&emsp; + Design Multi-Tenancy isolation pattern using Partition Key (`tenantId`) strategy on DynamoDB <br>&emsp; + Establish RBAC permission matrix & Estimate monthly cost using AWS Pricing Calculator | 20/07/2026 | 20/07/2026 | <https://cloudjourney.awsstudygroup.com> |
| 3 | - **Provision IaC Infrastructure & Edge/Auth Layer (AWS CDK):** <br>&emsp; + Initialize AWS CDK project to provision VPC Private Subnets, Route 53 & CloudFront CDN (integrated with AWS WAF v2 & AWS Shield) <br>&emsp; + Configure Amazon Cognito User Pools with Custom Claims (`{tenantId, role, userId}`) <br>&emsp; + Provision Amazon API Gateway (HTTP API v2) with JWT Authorizer & Custom Header Verification | 21/07/2026 | 21/07/2026 | <https://000076.awsstudygroup.com> <br> <https://000141.awsstudygroup.com> |
| 4 | - **Provision Data Layer & Core Compute (Lambda Functions):** <br>&emsp; + Provision **Amazon DynamoDB Single-Table Design** (`Attendance`, `Users`, `Tenants`) with **DynamoDB Streams (CDC)** & Data Encryption via **AWS KMS CMK** <br>&emsp; + Write business logic for Lambda functions: `Lambda Check-in`, `Lambda Check-out`, `Lambda Attendance`, and `Lambda Admin` <br>&emsp; + Store API Keys & DB Credentials in **AWS Secrets Manager** with Auto Rotation | 22/07/2026 | 22/07/2026 | <https://000060.awsstudygroup.com> <br> <https://000096.awsstudygroup.com> |
| 5 | - **Implement Workflow Engine & Event Notification Layer:** <br>&emsp; + Build async attendance report generation pipeline using **AWS Step Functions Engine** (Standard Workflow) & **Amazon SQS Queue + DLQ** <br>&emsp; + Provision **Amazon S3** (Intelligent-Tiering, KMS Encryption) storing report files (PDF, Excel, CSV) <br>&emsp; + Configure event pipeline: **DynamoDB Streams -> EventBridge Event Bus -> SQS Email Queue -> Lambda Email Worker -> Amazon SES** | 23/07/2026 | 23/07/2026 | <https://000047.awsstudygroup.com> <br> <https://000077.awsstudygroup.com> |
| 6 | - **Webhook Integration & DevOps CI/CD Pipeline Setup:** <br>&emsp; + Configure `Lambda Subscription` & `Lambda Webhook` handling inbound B2B subscription payment webhooks <br>&emsp; + Create **AWS CodePipeline** & **AWS CodeBuild** automating Build, Test & Vulnerability Scanning via **Amazon Inspector** | 24/07/2026 | 24/07/2026 | <https://000152.awsstudygroup.com> |

### Week 12 Achievements

* Designed and deployed a complete end-to-end Multi-Tenant Serverless SaaS Timekeeping Platform based on `Demo.drawio`.
* Mastered DynamoDB Single-Table Design combined with DynamoDB Streams for Change Data Capture (CDC).
* Implemented scalable asynchronous report processing using AWS Step Functions and Amazon SQS queues.
* Fully automated multi-tier cloud infrastructure deployment using AWS CDK v2 and CodePipeline CI/CD.
