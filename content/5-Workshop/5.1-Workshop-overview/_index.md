---
title: "Workshop Overview"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1 </b> "
---

# Smart Attendance SaaS Platform Workshop Overview

### Introduction

In this lab, you will explore the end-to-end architecture and concepts behind building a multi-tenant timekeeping Software-as-a-Service (**SaaS**) platform running 100% on **AWS Serverless**.

### System Architecture Diagram

Below is the complete Serverless infrastructure architecture that you will construct and deploy throughout this workshop:

![Smart Attendance SaaS Architecture](/images/2-Proposal/platform_architecture.png)

### Key Objectives & Learning Outcomes

Upon completing this workshop series, you will gain hands-on expertise in:

1. **Infrastructure as Code (IaC):** Using **AWS SAM (Serverless Application Model)** to declaratively define and automate 18+ AWS resources in code (`template.yaml`).
2. **Multi-Tenant Authentication:** Configuring **Amazon Cognito User Pools** with custom tenant claims (`tenantId`, `role`) integrated with **Amazon API Gateway HTTP API v2** via JWT Authorizers.
3. **High-Performance NoSQL Modeling:** Implementing an **Amazon DynamoDB Single-Table Design**, encrypting data-at-rest via **AWS KMS CMK**, and capturing Change Data Capture (CDC) events with **DynamoDB Streams**.
4. **Asynchronous Event-Driven Workflows:** Orchestrating **EventBridge Pipes**, **AWS Step Functions Express Workflows**, **Amazon SQS Queues**, and **Amazon SES** to automatically generate and email monthly Excel/PDF attendance reports.
5. **Edge Security & SPA Distribution:** Deploying a modern React + Vite Single Page Application to **Amazon S3**, served globally through **Amazon CloudFront CDN** secured with Custom Origin Verification Headers (`x-origin-verify`).

### Estimated Duration

* **Estimated Time:** 60 - 90 minutes.
* **Level:** Intermediate to Advanced.
