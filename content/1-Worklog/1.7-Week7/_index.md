---
title: "Week 7 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives

* Understand Infrastructure as Code (IaC) principles and cloud infrastructure automation benefits.
* Master AWS CloudFormation: Write YAML templates to automate VPC, Subnets, EC2, RDS & Security Groups deployment.
* Program infrastructure using modern high-level constructs with AWS Cloud Development Kit (AWS CDK v2) in TypeScript/Python.

### Tasks to be carried out this week

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | - Study AWS CloudFormation Core Concepts: <br>&emsp; + Template syntax (JSON/YAML): Parameters, Mappings, Conditions, Resources, Outputs <br>&emsp; + Stack lifecycle management (Create, Update, Drift Detection, Rollback & Delete) | 15/06/2026 | 15/06/2026 | <https://000037.awsstudygroup.com> |
| 3 | - **Practice:** <br>&emsp; + Write a CloudFormation Template provisioning complete VPC, Subnets, IGW & Security Groups <br>&emsp; + Deploy stack via AWS CLI & test Drift Detection after manual console edits | 16/06/2026 | 16/06/2026 | <https://000037.awsstudygroup.com> |
| 4 | - Study AWS Cloud Development Kit (AWS CDK) Essentials: <br>&emsp; + CDK Architecture: App, Stacks & Constructs (L1, L2, L3 constructs) <br>&emsp; + CDK CLI (cdk init, cdk synth, cdk diff, cdk deploy, cdk destroy) | 17/06/2026 | 17/06/2026 | <https://000038.awsstudygroup.com> |
| 5 | - Study AWS CDK Advanced: <br>&emsp; + Multi-stack architecture & Cross-stack references <br>&emsp; + Build reusable Custom Constructs for team standards <br>&emsp; + CDK Aspects & Unit Testing infrastructure code with Jest/PyTest | 18/06/2026 | 18/06/2026 | <https://000076.awsstudygroup.com> <br> <https://000102.awsstudygroup.com> |
| 6 | - **Practice:** <br>&emsp; + Build an AWS CDK TypeScript/Python project for a 3-Tier Web App (VPC + ALB + EC2 ASG + RDS) <br>&emsp; + Execute `cdk synth` to generate template and `cdk deploy` for automated provisioning | 19/06/2026 | 19/06/2026 | <https://000076.awsstudygroup.com> |

### Week 7 Achievements

* Mastered CloudFormation YAML template formatting for consistent infrastructure packaging.
* Understood drift detection mechanisms and stack failure rollback scenarios.
* Gained proficiency in AWS CDK v2 object-oriented infrastructure modeling using L2 Constructs.
* Fully automated 3-tier enterprise infrastructure provisioning via CLI commands.
