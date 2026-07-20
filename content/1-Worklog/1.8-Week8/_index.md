---
title: "Week 8 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives

* Master Serverless architecture and Event-Driven application design principles on AWS.
* Gain deep expertise in AWS Lambda (Runtimes, Execution Roles, Layers, Memory/Timeout & Event Triggers).
* Build Serverless APIs using Amazon API Gateway, orchestrate workflows with AWS Step Functions & AWS SAM.

### Tasks to be carried out this week

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | - Learn AWS Lambda Core: <br>&emsp; + Event-driven model, Execution environment & Concurrency limits <br>&emsp; + IAM Execution Roles & Resource-based policies <br>&emsp; + Reusable Lambda Layers for shared code libraries | 22/06/2026 | 22/06/2026 | <https://000022.awsstudygroup.com> |
| 3 | - Learn Amazon API Gateway: <br>&emsp; + REST API vs HTTP API vs WebSocket API <br>&emsp; + Lambda Proxy Integration, Request Validation & Transformation <br>&emsp; + Authentication: Cognito User Pools vs Custom Lambda Authorizers | 23/06/2026 | 23/06/2026 | <https://000066.awsstudygroup.com> <br> <https://000141.awsstudygroup.com> |
| 4 | - **Practice:** <br>&emsp; + Develop business logic Lambda functions using Node.js/Python <br>&emsp; + Create REST API on API Gateway defining CRUD endpoints connected to Lambda & DynamoDB <br>&emsp; + Configure CORS & API Keys / Test API invocation via Postman | 24/06/2026 | 24/06/2026 | <https://000066.awsstudygroup.com> <br> <https://000133.awsstudygroup.com/> |
| 5 | - Study AWS Step Functions & AWS SAM (Serverless Application Model): <br>&emsp; + State Machines (Standard vs Express Workflows), Choice States & Error Handling <br>&emsp; + AWS SAM template syntax (template.yaml) & SAM CLI (sam build, sam local, sam deploy) | 25/06/2026 | 25/06/2026 | <https://000047.awsstudygroup.com> <br> <https://000080.awsstudygroup.com/> |
| 6 | - **Practice:** <br>&emsp; + Build a multi-step order processing workflow with Step Functions orchestrating multiple Lambdas <br>&emsp; + Package and deploy the entire Serverless application using AWS SAM CLI | 26/06/2026 | 26/06/2026 | <https://000047.awsstudygroup.com> <br> <https://000080.awsstudygroup.com/> |

### Week 8 Achievements

* Mastered event-driven Lambda function execution, error handling, and performance tuning.
* Deployed production-ready Serverless REST APIs connecting API Gateway, Lambda, and DynamoDB.
* Orchestrated complex multi-step workflows using Step Functions with automated catch/retry logic.
* Standardized serverless development, local testing, and automated deployment using AWS SAM.
