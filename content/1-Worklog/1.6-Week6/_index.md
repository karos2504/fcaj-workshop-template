---
title: "Week 6 Worklog"
date: 2026-06-08
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives

* Understand Serverless Computing philosophy and Event-Driven Architecture on AWS.
* Master AWS Lambda (Execution environments, Execution Roles, Layers & Event Triggers) and user authentication with Amazon Cognito.
* Build Serverless REST APIs with Amazon API Gateway, orchestrate complex workflows using AWS Step Functions, and automate deployments using AWS SAM CLI.

### Tasks to be carried out this week

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | - **Serverless Automation with AWS Lambda:** <br>&emsp; + Event-driven execution model, Execution Environments & Concurrency limits <br>&emsp; + IAM Execution Roles & Resource-based access policies <br>&emsp; + Utilize Lambda Layers to share reusable code and libraries | 08/06/2026 | 08/06/2026 | <https://000022.awsstudygroup.com> |
| 3 | - **Building Serverless APIs with Amazon API Gateway:** <br>&emsp; + REST API vs HTTP API vs WebSocket API comparison <br>&emsp; + Lambda Proxy Integration, Request Validation & CORS configuration <br>&emsp; + User authentication using Amazon Cognito User Pools | 09/06/2026 | 09/06/2026 | <https://000066.awsstudygroup.com> <br> <https://000141.awsstudygroup.com> |
| 4 | - **Hands-on:** <br>&emsp; + Write business logic inside AWS Lambda functions using Node.js/Python <br>&emsp; + Provision REST API endpoints on API Gateway backed by Lambda & DynamoDB <br>&emsp; + Test API endpoints via Postman and verify JWT token authorization | 10/06/2026 | 10/06/2026 | <https://000066.awsstudygroup.com> |
| 5 | - **Workflow Orchestration with AWS Step Functions:** <br>&emsp; + State Machine types (Standard vs Express Workflows) <br>&emsp; + Choice States, Parallel execution, and Error Handling (Catch/Retry) <br>&emsp; + Introduction to AWS SAM template specification (`template.yaml`) | 11/06/2026 | 11/06/2026 | <https://000047.awsstudygroup.com> <br> <https://000080.awsstudygroup.com/> |
| 6 | - **Hands-on Serverless Application Model (AWS SAM):** <br>&emsp; + Build a multi-step asynchronous workflow orchestrating multiple Lambda functions via Step Functions <br>&emsp; + Package, test locally (`sam local`), and deploy automatically using AWS SAM CLI | 12/06/2026 | 12/06/2026 | <https://000047.awsstudygroup.com> <br> <https://000080.awsstudygroup.com/> |

### Week 6 Achievements

* Mastered writing and optimizing AWS Lambda functions following Event-Driven architecture patterns.
* Built and deployed a production-ready Serverless REST API combining API Gateway, Lambda, Cognito, and DynamoDB.
* Orchestrated complex multi-step workflows using AWS Step Functions with automated error handling and retries.
* Standardized, tested locally, and deployed full Serverless applications using AWS SAM CLI.

