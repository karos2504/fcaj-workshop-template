---
title: "Week 13 Worklog"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.13. </b> "
---

### Week 13 Objectives

* Perform end-to-end integration testing, performance benchmark, and cost optimization for the **SaaS Timekeeping Platform** following all 16 process flows (`Process Flow 1 - 16a`) from `Demo.drawio`.
* Configure system observability: Enable **AWS X-Ray** for end-to-end distributed tracing, build **CloudWatch Dashboards**, audit security posture using **AWS Security Hub & GuardDuty**.
* Author comprehensive step-by-step Workshop documentation, publish technical blog post, produce product demonstration video, and deliver final internship presentation to AWS Mentors on **July 30, 2026**.

### Tasks to be carried out this week

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | - **Integration & Load Testing:** <br>&emsp; + Conduct end-to-end integration tests covering all 16 process flows (`Process Flow 1 - 16a`): Route 53 -> CloudFront -> WAF -> Cognito Auth -> API Gateway -> Lambda Functions -> DynamoDB Single-Table -> Step Functions -> SQS -> SES & Payment Webhooks <br>&emsp; + Run load testing tools on API Gateway & Lambda to validate auto-scaling behavior and rate limit thresholds | 27/07/2026 | 27/07/2026 | <https://cloudjourney.awsstudygroup.com> |
| 3 | - **Distributed Tracing, Security Audit & Cost Optimization:** <br>&emsp; + Enable **AWS X-Ray** end-to-end request tracing across API Gateway, Lambda, DynamoDB, and Step Functions to pinpoint latency bottlenecks <br>&emsp; + Audit security posture with **AWS Security Hub**, **AWS GuardDuty**, and verify automated credential rotation in **AWS Secrets Manager** <br>&emsp; + Optimize Amazon S3 Intelligent-Tiering storage costs and enforce strict budget alerts with AWS Budgets | 28/07/2026 | 28/07/2026 | <https://cloudjourney.awsstudygroup.com> |
| 4 | - **Workshop Documentation, Technical Blog & Demo Video Production:** <br>&emsp; + **Workshop Documentation:** Write step-by-step hands-on guide for building SaaS Timekeeping Platform complete with `Demo.drawio` architecture diagrams and resource cleanup instructions <br>&emsp; + **Technical Blog Post:** Publish article titled *"Building a Multi-Tenant SaaS Timekeeping Platform with AWS Serverless Architecture (Cognito, DynamoDB Single-Table, Step Functions & EventBridge)"* <br>&emsp; + Record and edit live product demonstration video | 29/07/2026 | 29/07/2026 | <https://cloudjourney.awsstudygroup.com> |
| 5 | - **Final Internship & Graduation (30/07/2026):** <br>&emsp; + Wrap up 13-week AWS Cloud Journey internship program (05/05/2026 - 30/07/2026) | 30/07/2026 | 30/07/2026 | <https://cloudjourney.awsstudygroup.com> |

### Week 13 Achievements

* Successfully verified and benchmarked all 16 business process flows of the SaaS Timekeeping Platform based on `Demo.drawio`.
* Mastered AWS X-Ray distributed tracing for observability and latency optimization across serverless microservices.
* Authored high-quality hands-on Workshop documentation and published a deep-dive technical blog post.
* Delivered an outstanding final Capstone Project presentation to AWS Mentors, concluding the internship program (05/05/2026 - 30/07/2026).
