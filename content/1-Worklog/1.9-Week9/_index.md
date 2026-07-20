---
title: "Week 9 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objectives

* Understand Containerization core principles using Docker (Dockerfile, Images, Containers, Multi-stage builds).
* Manage private container image registries with Amazon Elastic Container Registry (ECR).
* Orchestrate containers at scale on Amazon ECS (Elastic Container Service) with AWS Fargate & Explore Amazon EKS (Elastic Kubernetes Service).

### Tasks to be carried out this week

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | - Learn Docker Core Concepts: <br>&emsp; + Docker Architecture, Images, Containers & Registries <br>&emsp; + Standard Dockerfile syntax & Multi-stage builds for small image footprints <br>&emsp; + Docker Networking & Persistent Volumes | 29/06/2026 | 29/06/2026 | <https://000015.awsstudygroup.com> |
| 3 | - **Practice:** <br>&emsp; + Write optimized Dockerfile for Web App (Node.js/Python/Go) <br>&emsp; + Build, run & debug containers on local computer <br>&emsp; + Create Amazon ECR Private Repository, authenticate AWS CLI, and push image to ECR | 30/06/2026 | 30/06/2026 | <https://000015.awsstudygroup.com> <br> <https://000067.awsstudygroup.com> |
| 4 | - Learn Amazon ECS Architecture: <br>&emsp; + Task Definitions (CPU, Memory, Env vars, Logging) <br>&emsp; + ECS Services, Clusters & Launch Types (EC2 vs AWS Fargate) <br>&emsp; + ECS Service Auto Scaling & Application Load Balancer integration | 01/07/2026 | 01/07/2026 | <https://000016.awsstudygroup.com> <br> <https://000067.awsstudygroup.com> |
| 5 | - **Practice:** <br>&emsp; + Provision an ECS Cluster powered by Serverless AWS Fargate <br>&emsp; + Create Task Definition pulling image from ECR & Launch ECS Service behind ALB <br>&emsp; + Verify Service Auto Scaling and zero-downtime rolling update deployments | 02/07/2026 | 02/07/2026 | <https://000067.awsstudygroup.com> |
| 6 | - Study Amazon EKS (Elastic Kubernetes Service) & Container IaC: <br>&emsp; + Kubernetes Control Plane & Managed Worker Nodes architecture <br>&emsp; + Overview of EKS Blueprints for AWS CDK for automated cluster provisioning | 03/07/2026 | 03/07/2026 | <https://000126.awsstudygroup.com> <br> <https://000065.awsstudygroup.com> |

### Week 9 Achievements

* Successfully containerized web applications using optimized multi-stage Docker builds.
* Established secure container image lifecycle management using Amazon ECR.
* Deployed scalable containerized microservices in production using Serverless ECS Fargate.
* Acquired foundational knowledge of Kubernetes architecture and Amazon EKS cluster management.
