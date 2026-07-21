---
title: "Week 11 Worklog"
date: 2026-07-13
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Week 11 Objectives

* **Updating Frontend UI and Backend Logic:** Refactor and upgrade user interface components (React/Vite) and core serverless backend execution logic (AWS Lambda) for the project.
* **Continued CloudJourney Learning:** Deepen skills in full-stack Serverless Web App integration and CI/CD automation pipelines on CloudJourney (`https://cloudjourney.awsstudygroup.com/`).
* Refine AWS CDK v2 stacks and finalize automated CodePipeline deployment workflows.

### Tasks to be carried out this week

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | - **Updating Frontend User Interface (13/07/2026 – 19/07/2026):** <br>&emsp; + Refactor React/Vite UI components: Optimize Dashboard layout, Admin panel, and GPS check-in screens <br>&emsp; + Study Web App frontend integration on CloudJourney | 13/07/2026 | 13/07/2026 | <https://cloudjourney.awsstudygroup.com> <br> <https://000141.awsstudygroup.com> |
| 3 | - **Updating Backend Handler Logic (AWS Lambda):** <br>&emsp; + Refactor Lambda functions logic: `CheckInFunction`, `CheckOutFunction`, `AttendanceSummary`, and `AdminFunction` <br>&emsp; + Standardize API response JSON schemas and error formatting | 14/07/2026 | 14/07/2026 | <https://000060.awsstudygroup.com> |
| 4 | - **Frontend & Backend API Gateway Integration:** <br>&emsp; + Wire frontend HTTP request clients to API Gateway HTTP API v2 endpoints <br>&emsp; + Inject Authorization Bearer JWT Tokens and implement session refresh handling | 15/07/2026 | 15/07/2026 | <https://000066.awsstudygroup.com> |
| 5 | - **AWS CDK v2 Infrastructure Code Updating:** <br>&emsp; + Refine infrastructure CDK stacks: `DatabaseStack`, `AuthStack`, `ApiStack`, and `FrontendStack` (S3 + CloudFront OAC) <br>&emsp; + Run `cdk synth` and `cdk diff` validation checks | 16/07/2026 | 16/07/2026 | <https://000076.awsstudygroup.com> |
| 6 | - **CI/CD Pipeline Refinement & End-to-End Testing:** <br>&emsp; + Update `buildspec.yml` script to automate React UI bundling, unit tests execution, and `cdk deploy` execution <br>&emsp; + Perform end-to-end integration testing between updated frontend and backend | 17/07/2026 | 17/07/2026 | <https://000152.awsstudygroup.com> |

### Week 11 Achievements

* Successfully updated and polished both Frontend UI and Backend serverless handlers.
* Continued applying full-stack serverless integration concepts learned on CloudJourney.
* Connected React Web UI to Serverless API Gateway backend seamlessly.

