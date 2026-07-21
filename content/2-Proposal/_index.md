---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Smart Attendance SaaS Platform

## A Unified Multi-Tenant Timekeeping & Attendance Solution Built on End-to-End AWS Serverless Architecture

### 1. Executive Summary

**Smart Attendance SaaS Platform** is a cloud-native attendance management and human resource tracking platform engineered for small and medium-sized enterprises (SMEs) as well as multi-branch corporations. The platform allows hundreds of business organizations (**Tenants**) to operate on a shared cloud infrastructure while maintaining **strict Tenant Data Isolation**, sub-200ms real-time response times, and automated elastic scaling during peak morning check-in windows.

By leveraging a 100% **AWS Serverless** ecosystem (including *Amazon CloudFront, AWS WAF v2, AWS Shield, Amazon Cognito, Amazon API Gateway, AWS Lambda, AWS Step Functions, Amazon DynamoDB, Amazon S3, Amazon EventBridge, Amazon SQS, Amazon SES, AWS KMS, and AWS Secrets Manager*), the platform eliminates server administration overhead, minimizes operational expenditure with a pay-as-you-go model (near $0 cost during idle hours), and guarantees high availability (**99.99% SLA**).

---

### 2. Problem Statement

#### What’s the Problem?

* **Manual Timekeeping & Peak Traffic Bottlenecks:** Traditional companies rely on physical fingerprint/card readers or manual spreadsheet logs. During rush hours (e.g., 7:45 AM - 8:15 AM), thousands of employees check in simultaneously, creating severe API bottlenecks, latency spikes, and system crashes.
* **High Infrastructure & Maintenance Costs:** Deploying timekeeping applications on legacy server models (EC2 / RDS / On-Premises) requires high upfront capital expenditure and ongoing 24/7 server maintenance costs—even during non-working hours when system usage drops to zero.
* **Multi-Tenancy Security & Data Leakage Risks:** Multi-tenant SaaS products face critical security risks regarding cross-tenant data leaks if data partition key isolation and strict token authorization mechanisms are not properly enforced at the database and API ingress levels.
* **Lack of Automated Reporting & Alerting:** Compiling monthly attendance summary sheets manually is time-consuming and prone to human errors, lacking automated integration with email delivery services and third-party webhooks.

#### The Proposed Solution

The **Smart Attendance SaaS Platform** addresses these challenges using an **AWS Serverless Optimized Pro Architecture**:

1. **Edge & API Protection Layer:** Uses **Amazon CloudFront** coupled with **AWS WAF v2** and **AWS Shield** to deliver the React SPA frontend, block unauthorized requests, rate-limit DDoS/Botnet attacks, and secure API origin requests via a custom verification token (`x-origin-verify`).
2. **Multi-tenant Identity Management:** **Amazon Cognito User Pool** manages authentication with built-in Custom Attributes (`tenantId`, `role`, `userId`), multi-factor authentication (TOTP MFA), and Advanced Security Mode.
3. **High-Performance Compute & Microservices:** Stateless **AWS Lambda** functions (Auth, Check-in, Check-out, Attendance History, Admin Management, Export Report API, Webhook, Subscriptions) scale automatically to handle peak traffic effortlessly.
4. **Single-Table Design Database:** **Amazon DynamoDB** stores all entity types (Attendance, Users, Tenants) in a single table (Single-Table Design) with `TENANT#<tenantId>` Partition Key isolation, ensuring sub-10ms query latency and ironclad tenant isolation.
5. **Asynchronous Reporting Engine:** Combines **AWS Step Functions Express Workflow** and **Amazon SQS** to decouple heavy report generation tasks (PDF/Excel/CSV), storing generated reports in **Amazon S3 (Intelligent-Tiering)** and emailing secure download links via **Amazon SES**.

#### Benefits and Return on Investment (ROI)

* **Over 90% Infrastructure Cost Savings:** The serverless pay-as-you-go model ensures costs scale directly with actual requests. Baseline monthly infrastructure costs for 100 Tenants (5,000 active employees) come out to **~$9.93 USD/month**, offering massive savings compared to $120–$150 USD/month for traditional EC2/RDS setups.
* **Elastic Scalability:** Smoothly scales from tens to hundreds of thousands of concurrent clock-in requests per minute during morning peaks without manual provisioning.
* **Time Savings & Fast ROI:** Reduces HR monthly attendance processing time by 95%. SaaS vendors achieve full investment recovery within 2-3 months of commercial operation.

---

### 3. Solution Architecture

The platform implements a comprehensive **AWS Serverless Multi-Layered Architecture**:

![Smart Attendance SaaS Architecture](/images/2-Proposal/platform_architecture.png)

#### AWS Services Used

| Architectural Layer | AWS Service | Core Role & Responsibilities |
| :--- | :--- | :--- |
| **Global Edge Layer** | Amazon Route 53 | Global DNS resolution and domain routing. |
| | AWS WAF v2 | Protects Web & APIs against DDoS, enforces Rate Limiting (1000 req/IP), blocks Bots & OWASP Top 10. |
| | AWS Shield | Managed Layer 3/4 DDoS protection. |
| | Amazon CloudFront | Global CDN delivering React SPA assets and serving as an encrypted proxy to API Gateway with Custom Header Verification. |
| **Auth & Ingress Layer** | Amazon Cognito | Identity provider, issues JWTs with embedded claims `{tenantId, role, userId}`, enforces TOTP MFA. |
| | Amazon API Gateway | HTTP API v2 with Cognito JWT Authorizer and custom header verification from CloudFront ingress. |
| | AWS Secrets Manager | Stores and auto-rotates Webhook API Keys & credentials for external integrations. |
| **Compute Layer** | AWS Lambda | Executes microservice functions (Auth, Check-in/out, History, Admin, Export Report API, Billing, Webhook). |
| | AWS Step Functions | Orchestrates complex multi-step Express Workflows for batch report generation. |
| **Data & Storage Layer** | Amazon DynamoDB | NoSQL Single-Table Design with KMS CMK encryption and DynamoDB Streams (CDC enabled). |
| | Amazon S3 | Hosts React SPA frontend and stores generated report files (PDF/Excel/CSV) with Intelligent-Tiering and Force SSL policy. |
| **Event & Messaging** | Amazon EventBridge | EventBus & EventBridge Pipe routing CDC events from DynamoDB Streams (`AttendanceCreated`, `ReportGenerated`). |
| | Amazon SQS | Buffers email notifications & alerts with Dead Letter Queue (DLQ) guarantee against message loss. |
| | Amazon SES | Delivers automated transactional emails containing reports, check-in alerts, and invoices. |
| **Operations & Security** | AWS KMS | Customer Managed Keys (CMK) data-at-rest encryption across DynamoDB, S3, and SQS. |
| | Amazon CloudWatch | Centralized logs, metrics, dashboards, and automated alarm notifications for API/Lambda runtime errors. |
| | AWS X-Ray | End-to-end distributed tracing for monitoring system performance and latency. |
| | AWS Security Hub & Inspector | Security posture management, vulnerability assessment, and GuardDuty threat detection. |
| | CodePipeline & CodeBuild | CI/CD pipeline automating testing, artifact building, and deployment via AWS SAM/CloudFormation. |

#### Process Flow & Data Architecture (16-Step Process Flow)

Based on the architecture diagram (`platform_architecture.drawio`), the system operates through a 16-step end-to-end flow:

1. **DNS Resolution (`1`):** Client sends DNS request via **Amazon Route 53**.
2. **HTTPS Ingress (`2`):** HTTPS request hits **Amazon CloudFront**, protected by **AWS WAF v2** & **AWS Shield**.
3. **Static Content (`3`):** Web App (React SPA) assets are delivered directly from **Amazon S3** via CloudFront CDN.
4. **Authentication (`4`):** Web/Mobile app authenticates with **Amazon Cognito**, receiving a JWT token containing `{tenantId, role, userId}` context.
5. **API Proxy Path (`4a` & `5`):** API calls carrying the JWT token and `x-origin-verify` custom header pass through CloudFront to **API Gateway**.
6. **API Gateway Execution (`6`):** API Gateway validates JWT & custom headers, triggering the targeted **AWS Lambda** microservice (Check-in, Check-out, History).
7. **Async Report Request (`7`):** When an admin requests a large monthly report, the request is offloaded to an **Amazon SQS Queue**, returning an instant UI response.
8. **CDC Capture (`8a` & `8b`):** **DynamoDB Streams** captures Change Data Capture (CDC) events and streams via **EventBridge Pipe** to **Amazon EventBridge**.
9. **Workflow Execution (`9`):** **AWS Step Functions Engine** consumes SQS tasks and coordinates Lambda functions to assemble report files.
10. **Transactional Data Ops (`10`):** Lambda performs CRUD operations on **Amazon DynamoDB** using Single-Table Design with `TENANT#<tenantId>` partition key isolation.
11. **Report Storage (`11`):** PDF/Excel/CSV files are written to an **Amazon S3 Bucket** configured with S3 Intelligent-Tiering for cost lifecycle management.
12. **Notification Events (`12` & `13`):** EventBridge routes notification triggers to the **SQS Email Queue**, where the **Lambda Email Worker** processes messages in batches.
13. **Secured Email Delivery (`14`):** Lambda Email Worker invokes **Amazon SES** to send emails containing secure report download links.
14. **Outbound Webhooks (`15`):** **Lambda Webhook** dispatches real-time attendance alerts to third-party endpoints (Slack, Teams, HR systems).
15. **B2B Billing Integration (`16` & `16a`):** **Lambda Subscription** interacts with Payment Gateways. Successful payment webhooks (`16a`) hit API Gateway to update tenant status automatically.

---

### 4. Technical Implementation

#### Implementation Phases

The project is structured across 4 standardized phases:

1. **Phase 1: Architecture & Data Modeling (Weeks 1–2)**
   * Design DynamoDB Single-Table schema (Access Patterns: Employee Check-in, Check-out, Monthly Summary, Tenant Admin Queries).
   * Configure Cognito User Pools, Custom Attributes (`tenantId`, `role`), and Security Policies.
   * Map end-to-end security ingress flow across CloudFront, WAF v2, and API Gateway.
2. **Phase 2: Core Serverless Backend Development with AWS SAM (Weeks 3–5)**
   * Package Infrastructure as Code (IaC) using **AWS SAM / CloudFormation** (`template.yaml`).
   * Develop Node.js 20.x Lambda microservices for Authentication, Check-in/out, History, Admin, Report Export API, Webhook.
   * Configure EventBridge Pipe, SQS Queues with DLQ, and Step Functions Express Workflows.
3. **Phase 3: React SPA Frontend & CloudFront Integration (Weeks 6–7)**
   * Build Admin Dashboard and Employee Web App interfaces using React + Vite + TailwindCSS.
   * Integrate Cognito SDK for Auth flows, Token refresh, and role-based access control (RBAC).
   * Deploy static site build to S3 Bucket with CloudFront CDN distribution and Secret Origin Verification Header.
4. **Phase 4: Testing, Security Audit, CI/CD & Production Go-Live (Week 8)**
   * Establish automated CI/CD pipeline using **AWS CodePipeline** and **AWS CodeBuild** (Inspector vulnerability scanning).
   * Conduct load testing simulating 10,000 concurrent clock-in requests per minute.
   * Audit security compliance via **AWS Security Hub**, enable **AWS X-Ray** tracing and **CloudWatch Alarms**.

#### Technical Stack & Requirements

* **Frontend:** React.js, Vite, TailwindCSS, AWS Amplify / Cognito JS SDK.
* **Backend:** Node.js 20.x (AWS Lambda runtime), AWS SAM (Serverless Application Model), AWS SDK v3.
* **Database:** Amazon DynamoDB (Single-Table Design, On-Demand Capacity Mode, DynamoDB Streams).
* **Storage & CDN:** Amazon S3 (Static Website Hosting & Report Files), Amazon CloudFront (Global CDN, TLS 1.3).
* **Security & Auth:** Amazon Cognito, AWS WAF v2, AWS KMS (CMK), AWS Secrets Manager.
* **Orchestration & Events:** AWS Step Functions, Amazon EventBridge, Amazon SQS.

---

### 5. Timeline & Milestones

```
+-----------------------------------------------------------------------------------+
| Month 1: Discovery & Planning    | Month 2: Backend & Data Implementation         |
| - Finalize requirements & Schema | - Build AWS SAM Template                       |
| - Design OpenAPI & Cognito Auth  | - Develop Lambda Microservices & DynamoDB      |
+---------------------------------+-------------------------------------------------+
| Month 3: Frontend & Integration  | Month 4: Testing, Security & Production Go-Live |
| - Develop React Admin Dashboard | - Peak Load Testing & Security Hub Audit        |
| - Connect API Gateway & SES     | - Set up CI/CD CodePipeline & Official Go-Live  |
+-----------------------------------------------------------------------------------+
```

* **Milestone 1 (End of Month 1):** Architecture blueprint finalized, SAM template initialized, Cognito User Pool configured.
* **Milestone 2 (End of Month 2):** Core Backend APIs (Check-in/out, History, Query, Webhooks) and DynamoDB Single-Table deployed.
* **Milestone 3 (End of Month 3):** Web Dashboard for Admins/HR and Employee App frontend completed.
* **Milestone 4 (End of Month 4):** Production Go-Live on AWS Cloud with complete operational documentation.

---

### 6. Budget Estimation

Estimated monthly cost based on the **AWS Pricing Calculator** for a baseline workload of **100 Tenants – 5,000 Active Employees (500,000 check-in transactions/month)**:

#### Monthly Infrastructure Cost Breakdown

| AWS Service | Estimated Monthly Usage | Monthly Cost (USD) |
| :--- | :--- | :--- |
| **AWS Lambda** | 2,000,000 requests/month (128MB - 512MB, avg 200ms) | $0.40 USD (Covered by Free Tier) |
| **Amazon DynamoDB** | On-Demand (500k writes, 1.5M reads, 5GB storage) | $1.25 USD |
| **Amazon API Gateway** | 2,500,000 HTTP API requests/month | $2.50 USD |
| **Amazon CloudFront** | 50 GB Data Transfer Out + 1,000,000 HTTP requests | $0.85 USD |
| **Amazon S3** | 10 GB Report & Static site storage + Intelligent-Tiering | $0.23 USD |
| **Amazon Cognito** | 5,000 MAUs (Monthly Active Users) | $0.00 USD (Free Tier up to 50k MAUs) |
| **Amazon EventBridge & SQS**| 1,000,000 events & queue messages/month | $0.40 USD |
| **Amazon SES** | 10,000 notification emails/month | $1.00 USD |
| **AWS KMS & Secrets Manager**| 1 Customer Master Key + 2 Secrets | $1.50 USD |
| **Amazon CloudWatch & X-Ray**| 5GB Log Ingestion, Alarms & Tracing | $1.80 USD |
| **Total Monthly Infra Cost** | **For 100 Tenants (5,000 Active Users)** | **~$9.93 USD / month** |

> **Cost Comparison:** Traditional server infrastructure running 2 EC2 instances (`t3.medium`) + RDS PostgreSQL (`db.t3.medium`) costs roughly **$120 – $150 USD/month**. The AWS Serverless architecture delivers over **90% cost savings**.

---

### 7. Risk Assessment

#### Risk Matrix & Mitigation Strategies

| Risk Item | Impact | Likelihood | Mitigation Strategy |
| :--- | :---: | :---: | :--- |
| **Lambda Cold Start Spikes** | Medium | Low | Enable Provisioned Concurrency for core Check-in/out functions during morning rush hours; optimize Lambda bundle sizes. |
| **DynamoDB Throttling & Quotas** | High | Low | Provision DynamoDB in On-Demand Capacity Mode; implement API Gateway and CloudFront caching layer. |
| **DDoS / Auth Brute Force Attacks** | High | Medium | Enforce **AWS WAF v2** Rate Limiting (1000 req/IP); activate Cognito Advanced Security Mode to block brute force attempts. |
| **Cross-Tenant Data Leakage** | Critical | Very Low | Enforce strict Partition Key isolation (`TENANT#<tenantId>`) on all database queries; validate JWT Claims at API Gateway. |
| **Email Delivery Bottlenecks** | Low | Medium | Buffer email events using **Amazon SQS Queues** with Dead Letter Queues (DLQ) for failed message retry mechanisms. |

#### Contingency Plans

* **Disaster Recovery (DR):** Enable DynamoDB Point-in-Time Recovery (PITR) allowing continuous microsecond-level data restores up to 35 days.
* **Infrastructure Rollback:** Infrastructure defined completely via AWS SAM, enabling full stack rollbacks within 5 minutes in case of deployment errors.

---

### 8. Expected Results

#### Technical Improvements

* **Processing Speed:** Check-in response time under **200ms**, attendance history query latency under **50ms**.
* **Reliability:** 99.99% system availability SLA with automatic failover and recovery.
* **100% Automation:** Automated report generation and email distribution eliminate manual HR tasks completely.
