---
title: "Week 2 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives

* Master core concepts of Amazon VPC network infrastructure and network security on AWS.
* Design and deploy a custom VPC with Public Subnets, Private Subnets, Internet Gateway, and NAT Gateway.
* Gain deep knowledge of IAM permission management and network traffic monitoring using VPC Flow Logs.

### Tasks to be carried out this week

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | - Deep dive into IAM (Identity and Access Management): <br>&emsp; + IAM Users, Groups, Roles & Policies (Managed vs Inline) <br>&emsp; + Principle of Least Privilege & Enable MFA security | 11/05/2026 | 11/05/2026 | <https://000002.awsstudygroup.com> |
| 3 | - Learn Amazon VPC Core Components: <br>&emsp; + CIDR Blocks, Public Subnets & Private Subnets <br>&emsp; + Internet Gateway (IGW), NAT Gateway & Route Tables | 12/05/2026 | 12/05/2026 | <https://000003.awsstudygroup.com> <br> <https://000092.awsstudygroup.com> |
| 4 | - **Practice:** <br>&emsp; + Create a Custom VPC with 2 Public Subnets and 2 Private Subnets across 2 AZs <br>&emsp; + Configure Internet Gateway for Public Subnets & NAT Gateway for Private Subnets | 13/05/2026 | 13/05/2026 | <https://000003.awsstudygroup.com> |
| 5 | - Study network security mechanisms: Security Groups (Stateful) vs Network ACLs (Stateless) <br> - Learn VPC Peering and VPC Flow Logs for network monitoring | 14/05/2026 | 14/05/2026 | <https://000019.awsstudygroup.com/> <br> <https://000074.awsstudygroup.com> |
| 6 | - **Practice:** <br>&emsp; + Configure Security Groups & NACL rules for Web Server and Bastion Host <br>&emsp; + Enable VPC Flow Logs to deliver logs to CloudWatch Logs <br>&emsp; + Verify network connectivity between subnets and ensure Private Subnet isolation | 15/05/2026 | 15/05/2026 | <https://000074.awsstudygroup.com> |

### Week 2 Achievements

* Mastered IAM least-privilege principles and enforced MFA across accounts.
* Built a comprehensive multi-AZ custom VPC architecture from scratch.
* Differentiated stateful Security Groups and stateless Network ACLs effectively.
* Collected and analyzed real-time network traffic using VPC Flow Logs.
