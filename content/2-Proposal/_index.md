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

The project is structured into 4 standardized delivery phases:

1. **Phase 1: Architecture & Data Model Design (Weeks 1–2)**
   * Design Single-Table Design schema on DynamoDB (Access Patterns: Employee Check-in, Check-out, Monthly Summary, Tenant Admin Queries).
   * Configure Cognito User Pool, Custom Attributes (`tenantId`, `role`), and Security Policies.
   * Map end-to-end security ingress across CloudFront + WAF v2 + API Gateway.
2. **Phase 2: Core Serverless Backend with AWS SAM (Weeks 3–5)**
   * Package infrastructure as code (IaC) using **AWS SAM / CloudFormation** (`template.yaml`).
   * Develop Lambda microservices (Node.js 20) for Auth, Check-in/out, History, Admin, Report Export API, and Webhooks.
   * Set up EventBridge Pipe, SQS Queue, SQS Email DLQ, and Step Functions Express Workflows.
3. **Phase 3: Frontend React SPA & CloudFront Integration (Weeks 6–7)**
   * Build Admin Dashboard and Employee Web App using React + Vite + TailwindCSS.
   * Integrate Cognito JS SDK for sign-in/registration, token refresh, and role-based access control (RBAC).
   * Bundle static site assets and deploy to S3 Bucket + CloudFront Distribution with Secret Origin Verification Header.
4. **Phase 4: Testing, Security Audit, CI/CD & Go-Live (Week 8)**
   * Establish CI/CD pipelines via **AWS CodePipeline** and **AWS CodeBuild** (vulnerability scanning with Amazon Inspector).
   * Perform load testing simulating 10,000 concurrent check-in requests in 1 minute.
   * Audit security posture using **AWS Security Hub**, enabling distributed tracing via **AWS X-Ray** & **CloudWatch Alarms**.

#### Technical Stack & Requirements

* **Frontend:** React.js, Vite, TailwindCSS, AWS Amplify/Cognito JS SDK.
* **Backend:** Node.js 20.x (AWS Lambda Runtime), AWS SAM (Serverless Application Model), AWS SDK v3.
* **Database:** Amazon DynamoDB (Single-Table Design, On-Demand Capacity Mode, DynamoDB Streams).
* **Storage & CDN:** Amazon S3 (Static Web & Report Storage), Amazon CloudFront (Edge Network, TLS 1.3).
* **Security & Auth:** Amazon Cognito, AWS WAF v2, AWS KMS (CMK), AWS Secrets Manager.
* **Orchestration & Events:** AWS Step Functions, Amazon EventBridge, Amazon SQS.

---

### 5. Roadmap & Milestones

```
+-----------------------------------------------------------------------------------+
| Month 1: Planning & Design      | Month 2: Backend & Data Implementation          |
| - Requirements & Data Schema    | - Build AWS SAM Infrastructure Template         |
| - OpenAPI & Cognito Setup       | - Develop Lambda Microservices & DynamoDB Table |
+---------------------------------+-------------------------------------------------+
| Month 3: Frontend Integration   | Month 4: Testing, Security & Production Go-Live |
| - Develop React Dashboard UI    | - High-load testing, Audit AWS Security Hub     |
| - Connect API Gateway & SES     | - Setup CodePipeline CI/CD & Production Deploy  |
+-----------------------------------------------------------------------------------+
```

* **Milestone 1 (End of Month 1):** Architecture blueprint finalized, SAM template scaffolding complete, Cognito User Pool deployed.
* **Milestone 2 (End of Month 2):** Core Backend APIs complete (Check-in/out, History, Reports, Webhooks) with DynamoDB Single-Table.
* **Milestone 3 (End of Month 3):** Web Dashboard for Admin/HR and Employee App fully integrated.
* **Milestone 4 (End of Month 4):** Full system launched on AWS Cloud Production environment.

---

### 6. Detailed Cost Analysis & ROI (Strictly Mapped to 24 Diagram Resource Nodes)

Based on an exact node-by-node inventory of **24 resource instances** across **22 AWS services** present on the `platform_architecture.drawio` architecture blueprint, below is the itemized monthly operational cost breakdown:

#### Itemized Monthly Operational Cost Table (Standard Scale: 100 Tenants ~ 5,000 Staff, 3M Requests/Month)

| Item | AWS Service Node on Diagram | Node Count | Usage Metrics & Unit Pricing (Monthly) | Cost (USD/Month) |
| :---: | :--- | :---: | :--- | :--- |
| **1** | **Amazon Route 53** | 1 Node | 1 Hosted Zone ($0.50) + 3.0M DNS Queries ($1.20) | **$1.70** |
| **2** | **AWS WAF v2** | 1 Node | 1 Web ACL ($5.00) + 1 Managed Rule ($1.00) + 3M Req ($1.80) | **$7.80** |
| **3** | **AWS Shield** | 1 Node | Layer 3/4 DDoS Protection (Included Free with CloudFront) | **$0.00** |
| **4** | **Amazon CloudFront** | 1 Node | 50GB Data Transfer Out + 3M HTTPS Req (1TB Free Tier) | **$0.00** |
| **5** | **Amazon S3 (SPA Hosting)** | 1 Node | 1GB React Static Assets + 100k GET Requests | **$0.06** |
| **6** | **Amazon Cognito** | 1 Node | 5,000 MAUs User Auth (Free Tier covers up to 50,000 MAUs) | **$0.00** |
| **7** | **Amazon API Gateway** | 1 Node | HTTP API v2: 3,000,000 Requests ($1.00 / 1M Requests) | **$3.00** |
| **8** | **AWS Secrets Manager** | 1 Node | 1 Secret Key ($0.40) + API Calls ($0.50) | **$0.90** |
| **9** | **AWS Lambda (8 Functions)** | **8 Nodes** | Webhook, Check-in, Check-out, Attendance, Report, Admin, Subscription, Email Worker (3M invocations, avg 100ms) | **$0.63** |
| **10**| **AWS Step Functions Engine**| 1 Node | 10,000 Express Workflow Executions ($1.00 / 1M Executions) | **$0.02** |
| **11**| **Amazon SQS (Report Queue)** | 1 Node | 20,000 Report Queue Messages (Covered under 1M SQS Free Tier) | **$0.00** |
| **12**| **Amazon SQS (Email Queue)** | 1 Node | 20,000 Email Queue Messages (Covered under 1M SQS Free Tier) | **$0.00** |
| **13**| **Amazon DynamoDB** | 1 Node | Single-Table: 3M Writes ($3.75) + 6M Reads ($1.50) + 5GB ($1.25) | **$6.50** |
| **14**| **DynamoDB Streams** | 1 Node | CDC Event Streams (First 2.5M stream requests free) | **$0.00** |
| **15**| **AWS KMS CMK** | 1 Node | 1 Customer Managed Key ($1.00) + Request Encryption ($0.09) | **$1.09** |
| **16**| **Amazon S3 (Report Storage)**| 1 Node | 10GB Reports (Intelligent-Tiering Lifecycle) + PUT/GET | **$0.28** |
| **17**| **Amazon EventBridge** | 1 Node | EventBus: 1,000,000 Events routed ($1.00 / 1M Events) | **$1.00** |
| **18**| **Amazon SES** | 1 Node | 10,000 Transactional & Report Emails ($0.10 / 1,000 Emails) | **$1.00** |
| **19**| **Amazon CloudWatch** | 1 Node | Logs Ingestion 2GB ($1.00) + Basic Metrics & Alarms ($0.50) | **$1.50** |
| **20**| **AWS X-Ray** | 1 Node | 1,000,000 Distributed Traces Sampled ($5.00 / 1M Traces) | **$4.50** |
| **21**| **AWS CloudFormation** | 1 Node | Infrastructure as Code Resource Management (Free Service) | **$0.00** |
| **22**| **AWS CodePipeline** | 1 Node | 1 Active CI/CD Pipeline | **$1.00** |
| **23**| **AWS CodeBuild (Inspector)**| 1 Node | 100 Build Minutes ($0.50) + Container Vulnerability Scan ($0.50) | **$1.00** |
| **24**| **AWS Security Hub & GuardDuty**| 1 Node | Infrastructure Posture & Threat Detection Alerts | **$1.50** |
| **TOTAL INFRASTRUCTURE COST**| **24 Nodes** | **All 24 Diagram Service Nodes Included (Full Security & Tracing)** | **~$35.51 USD/month** |

> [!NOTE]
> **Bootstrapping Optimization (Basic Profile):** Disabling managed WAF rules and X-Ray sampling during early startup reduces baseline monthly infrastructure expenses down to **~$23.21 USD/month**.

---

#### Multi-Tier Scalability Comparison

```
+---------------------------------------------------------------------------------------------------+
| Growth Scale               | Usage Metrics                    | Serverless Cost   | Legacy EC2/RDS |
+----------------------------+----------------------------------+--------------------+----------------+
| Starter (10 Tenants)       | 500 Staff · 300K Requests/month  | ~$4.20 USD/month   | ~$85.00 USD    |
| Standard (100 Tenants)     | 5,000 Staff · 3M Requests/month  | ~$35.51 USD/month  | ~$165.00 USD   |
| Enterprise (1,000 Tenants) | 50,000 Staff · 30M Requests/month| ~$156.80 USD/month | ~$650.00 USD   |
+---------------------------------------------------------------------------------------------------+
```

> [!TIP]
> **Return on Investment (ROI):**
>
> * **78% to 95% Monthly Cost Reduction** compared to maintaining 24/7 dedicated EC2 application servers and RDS database instances.
> * **Zero Idle Cost:** During non-business hours (nights and weekends), compute and API expenses naturally scale down to **$0 USD**.
