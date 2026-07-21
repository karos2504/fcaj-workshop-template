---
title: "Week 5 Worklog"
date: 2026-06-01
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives

* Master High Availability (HA) and Scalability system architecture design principles on AWS.
* Configure Elastic Load Balancing (Application Load Balancer - ALB) to distribute multi-AZ application traffic.
* Configure EC2 Auto Scaling Groups, Amazon Route 53 DNS Routing Policies, and inter-VPC connectivity via VPC Peering.

### Tasks to be carried out this week

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | - **Elastic Load Balancing (ELB Essentials):** <br>&emsp; + Compare ALB (Layer 7) vs NLB (Layer 4) <br>&emsp; + Target Groups, Health Checks & Listener Rules <br>&emsp; + SSL/TLS Termination using AWS Certificate Manager (ACM) certificates | 01/06/2026 | 01/06/2026 | <https://000006.awsstudygroup.com> |
| 3 | - **EC2 Auto Scaling Groups (ASG):** <br>&emsp; + Launch Templates vs Launch Configurations <br>&emsp; + Scaling Policies: Target Tracking, Step Scaling & Scheduled Scaling <br>&emsp; + Dynamic Scaling based on CPU utilization / ALB Request count | 02/06/2026 | 02/06/2026 | <https://000006.awsstudygroup.com> |
| 4 | - **Hands-on:** <br>&emsp; + Create a Launch Template for EC2 Web Servers <br>&emsp; + Provision an ALB across 2 Public Subnets and attach Target Groups <br>&emsp; + Create an Auto Scaling Group spanning 2 Private Subnets integrated with ALB | 03/06/2026 | 03/06/2026 | <https://000006.awsstudygroup.com> |
| 5 | - **Amazon Route 53 & Hybrid DNS:** <br>&emsp; + Public vs Private Hosted Zones <br>&emsp; + Routing Policies: Simple, Weighted, Latency, Failover & Geolocation <br>&emsp; + Route 53 Health Checks & VPC Peering between isolated VPCs | 04/06/2026 | 04/06/2026 | <https://000010.awsstudygroup.com> <br> <https://000019.awsstudygroup.com/> |
| 6 | - **Building Highly Available Web Applications:** <br>&emsp; + Simulate heavy web traffic via Stress Testing on EC2 to evaluate Auto Scaling responses <br>&emsp; + Configure Route 53 Failover Routing to test automated DNS failover during outages | 05/06/2026 | 05/06/2026 | <https://000101.awsstudygroup.com> |

### Week 5 Achievements

* Successfully deployed an Application Load Balancer to distribute incoming traffic seamlessly across Availability Zones.
* Configured Auto Scaling Groups to dynamically scale EC2 capacity up or down based on real-time traffic demand.
* Mastered DNS routing strategies using Amazon Route 53 and implemented automated Disaster Recovery Failover.
* Connected two isolated VPC networks securely using VPC Peering.

