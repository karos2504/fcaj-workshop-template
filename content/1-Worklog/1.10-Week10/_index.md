---
title: "Week 10 Worklog"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Objectives

* Understand modern software delivery paradigms with CI/CD concepts (Continuous Integration / Continuous Delivery & Deployment).
* Gain hands-on mastery over AWS Developer Tools (CodeCommit, CodeBuild, CodeDeploy & CodePipeline).
* Automate end-to-end building, testing, and deployment pipelines for Serverless and Containerized applications.

### Tasks to be carried out this week

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | - Study DevOps Culture & CI/CD Fundamentals: <br>&emsp; + Differences between CI, CD & Continuous Deployment <br>&emsp; + Ecosystem of AWS Developer Tools <br>&emsp; + Source control management with AWS CodeCommit / GitHub integration | 06/07/2026 | 06/07/2026 | <https://000017.awsstudygroup.com> |
| 3 | - Study AWS CodeBuild: <br>&emsp; + `buildspec.yml` specification syntax (install, pre_build, build, post_build phases) <br>&emsp; + Environment Images, Build Artifacts & Environment Variables management | 07/07/2026 | 07/07/2026 | <https://000017.awsstudygroup.com> <br> <https://000051.awsstudygroup.com> |
| 4 | - Study AWS CodeDeploy & Deployment Strategies: <br>&emsp; + In-place deployment vs Blue/Green deployment <br>&emsp; + Deployment groups, AppSpec file (`appspec.yml`) & Automatic rollback triggers | 08/07/2026 | 08/07/2026 | <https://000023.awsstudygroup.com> |
| 5 | - Study AWS CodePipeline Orchestration: <br>&emsp; + Pipeline Stages (Source, Build, Test, Deploy, Manual Approval) <br>&emsp; + Webhook integration from GitHub / CodeCommit for automated git-push pipeline execution | 09/07/2026 | 09/07/2026 | <https://000023.awsstudygroup.com> <br> <https://000152.awsstudygroup.com> |
| 6 | - **Practice:** <br>&emsp; + Construct an end-to-end CI/CD pipeline that builds Docker images, pushes to ECR, and deploys to ECS Fargate upon code push <br>&emsp; + Configure pipeline status notifications via EventBridge & SNS | 10/07/2026 | 10/07/2026 | <https://000152.awsstudygroup.com> |

### Week 10 Achievements

* Mastered automated software release pipeline architecture on AWS.
* Proficiently wrote `buildspec.yml` and `appspec.yml` control files for automated build/deploy workflows.
* Built automated end-to-end CI/CD pipelines for ECS Container and Serverless services.
* Implemented Blue/Green deployment strategies ensuring zero downtime for web applications.
