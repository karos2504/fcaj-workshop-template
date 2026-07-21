---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Building a Multi-Tenant Smart Attendance SaaS Platform with AWS Serverless Architecture

#### Overview

In this hands-on workshop series, you will step-by-step construct and deploy a production-grade **Smart Attendance SaaS Platform** for multi-tenant organizations based on the **AWS Serverless Optimized Pro Architecture**.

You will define Infrastructure as Code (IaC) using **AWS SAM (Serverless Application Model)**, configure identity & access management with **Amazon Cognito User Pools**, implement an **Amazon DynamoDB Single-Table Design** enforcing strict tenant isolation (`tenantId`), orchestrate asynchronous report generation workflows using **AWS Step Functions**, **Amazon SQS**, and **Amazon SES**, and deploy a modern React SPA frontend delivered globally via **Amazon S3** and **Amazon CloudFront CDN**.

#### Workshop Labs Structure

1. [Workshop Overview](5.1-Workshop-overview/)
2. [Prerequisites & Environment Setup](5.2-Prerequiste/)
3. [Deploying Serverless Backend with AWS SAM](5.3-Deploy-Backend/)
4. [Configuring DynamoDB Single-Table & DynamoDB Streams](5.4-DynamoDB-SingleTable/)
5. [Building Asynchronous Reporting Workflow](5.5-Async-Reporting/)
6. [Deploying React SPA Frontend & CloudFront CDN](5.6-Frontend-CloudFront/)
7. [End-to-End Testing & Resource Cleanup](5.7-Testing-Cleanup/)
