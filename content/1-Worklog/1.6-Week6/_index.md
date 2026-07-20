---
title: "Week 6 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives

* Understand High Availability and Scalability system architecture design principles on AWS.
* Configure Elastic Load Balancing (Application Load Balancer - ALB) for traffic distribution.
* Implement EC2 Auto Scaling Groups alongside Route 53 Health Checks & DNS Failover.

### Tasks to be carried out this week

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | - Study Elastic Load Balancing (ELB): <br>&emsp; + ALB (Layer 7) vs NLB (Layer 4) <br>&emsp; + Target Groups, Health Checks & Listener Rules <br>&emsp; + SSL/TLS Termination with AWS Certificate Manager (ACM) | 08/06/2026 | 08/06/2026 | <https://000006.awsstudygroup.com> |
| 3 | - Study EC2 Auto Scaling Groups (ASG): <br>&emsp; + Launch Templates vs Launch Configurations <br>&emsp; + Scaling Policies: Target Tracking, Step Scaling & Scheduled Scaling <br>&emsp; + Dynamic Scaling based on CPU utilization / ALB Request count | 09/06/2026 | 09/06/2026 | <https://000006.awsstudygroup.com> |
| 4 | - **Practice:** <br>&emsp; + Create Launch Template defining Web Server EC2 instances <br>&emsp; + Provision an ALB across 2 Public Subnets attached to Target Group <br>&emsp; + Create Auto Scaling Group across 2 Private Subnets integrated with ALB | 10/06/2026 | 10/06/2026 | <https://000006.awsstudygroup.com> |
| 5 | - Study Amazon Route 53 & Hybrid DNS: <br>&emsp; + Hosted Zones (Public vs Private) <br>&emsp; + Routing Policies: Simple, Weighted, Latency, Failover & Geolocation <br>&emsp; + Route 53 Health Checks for DNS Failover configuration | 11/06/2026 | 11/06/2026 | <https://000010.awsstudygroup.com> <br> <https://000101.awsstudygroup.com> |
| 6 | - **Practice:** <br>&emsp; + Simulate heavy load using CPU stress tool to test auto scale out/in behavior <br>&emsp; + Configure Route 53 Failover Routing to test traffic redirection during primary site failure | 12/06/2026 | 12/06/2026 | <https://000101.awsstudygroup.com> |

### Week 6 Achievements

* Successfully deployed an Application Load Balancer distributing web traffic across multi-AZ subnets.
* Configured Auto Scaling Groups to scale EC2 instances dynamically based on real-time traffic demand.
* Mastered Route 53 DNS routing policies and automated disaster recovery failover mechanisms.
