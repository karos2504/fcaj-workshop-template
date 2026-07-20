---
title: "Week 4 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives

* Understand Amazon RDS (Relational Database Service) fundamentals and supported database engines (MySQL, PostgreSQL).
* Study High Availability features with Multi-AZ deployments and read scaling with Read Replicas.
* Learn NoSQL Database essentials with Amazon DynamoDB (Tables, Primary Key, Sort Key, Capacity Modes, Indexing).

### Tasks to be carried out this week

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | - Learn Amazon RDS Core: <br>&emsp; + Database Engines (MySQL, PostgreSQL, Aurora) <br>&emsp; + Instance Classes, Storage Types (gp3, io2) & Subnet Groups <br>&emsp; + Automated Backups, Snapshots & Parameter Groups | 25/05/2026 | 25/05/2026 | <https://000005.awsstudygroup.com> |
| 3 | - Learn RDS High Availability Architecture: <br>&emsp; + Multi-AZ deployment (Synchronous replication & Failover) <br>&emsp; + Read Replicas (Asynchronous replication for read scaling) | 26/05/2026 | 26/05/2026 | <https://000005.awsstudygroup.com> |
| 4 | - **Practice:** <br>&emsp; + Provision an Amazon RDS MySQL Multi-AZ instance inside Private Subnets <br>&emsp; + Restrict Security Group access strictly to Web EC2 instances <br>&emsp; + Test DB connection from app instance and trigger manual failover | 27/05/2026 | 27/05/2026 | <https://000005.awsstudygroup.com> |
| 5 | - Learn Amazon DynamoDB NoSQL: <br>&emsp; + Partition Key, Sort Key & Composite Primary Keys <br>&emsp; + Read/Write Capacity Modes (On-Demand vs Provisioned) <br>&emsp; + Local Secondary Indexes (LSI) & Global Secondary Indexes (GSI) | 28/05/2026 | 28/05/2026 | <https://000060.awsstudygroup.com> |
| 6 | - **Practice:** <br>&emsp; + Create a DynamoDB table and perform CRUD operations via AWS CLI/SDK <br>&emsp; + Compare performance, cost, and design trade-offs between RDS and DynamoDB | 29/05/2026 | 29/05/2026 | <https://000060.awsstudygroup.com> |

### Week 4 Achievements

* Successfully provisioned, secured, and connected Amazon RDS instances within private subnets.
* Understood automated backup retention and RDS Multi-AZ disaster recovery failover.
* Mastered DynamoDB NoSQL schema design, primary keys, and secondary indexing.
* Developed clear architectural criteria for choosing Relational vs NoSQL databases.
