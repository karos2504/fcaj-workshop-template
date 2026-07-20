---
title: "Week 11 Worklog"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---

### Week 11 Objectives

* Master AWS data encryption, security governance, and compliance solutions (AWS KMS, Secrets Manager, WAF, GuardDuty).
* Understand database migration methodologies using AWS DMS & Schema Conversion Tool (SCT).
* Explore Data Lake fundamentals and serverless data analytics querying with Amazon Athena.

### Tasks to be carried out this week

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | - Study AWS KMS (Key Management Service) & AWS Secrets Manager: <br>&emsp; + Customer Managed Keys (CMK), Envelope Encryption & Key Policies <br>&emsp; + Manage and automate DB credential rotation in Secrets Manager | 13/07/2026 | 13/07/2026 | <https://000033.awsstudygroup.com> <br> <https://000096.awsstudygroup.com> |
| 3 | - Study AWS WAF (Web Application Firewall) & Threat Detection: <br>&emsp; + Managed Rule Groups (SQLi, XSS, OWASP Top 10) & Rate Limiting <br>&emsp; + Continuous threat detection with AWS GuardDuty & AWS Security Hub | 14/07/2026 | 14/07/2026 | <https://000026.awsstudygroup.com> <br> <https://000098.awsstudygroup.com> |
| 4 | - **Practice:** <br>&emsp; + Create KMS Key encrypting S3 Buckets & EBS Volumes <br>&emsp; + Configure AWS WAF Web ACL protecting Application Load Balancer <br>&emsp; + Store DB password in Secrets Manager and retrieve programmatically from Lambda | 15/07/2026 | 15/07/2026 | <https://000033.awsstudygroup.com> <br> <https://000026.awsstudygroup.com> |
| 5 | - Study Database Migration (AWS Migration): <br>&emsp; + AWS Schema Conversion Tool (SCT) converting heterogeneous schemas <br>&emsp; + AWS Database Migration Service (DMS) real-time CDC data replication | 16/07/2026 | 16/07/2026 | <https://000043.awsstudygroup.com> |
| 6 | - Study Data & Analytics on AWS: <br>&emsp; + Data Lake design pattern on Amazon S3 & AWS Glue Crawlers/Data Catalog <br>&emsp; + Execute serverless SQL queries directly on S3 data using Amazon Athena | 17/07/2026 | 17/07/2026 | <https://000035.awsstudygroup.com> <br> <https://000106.awsstudygroup.com> |

### Week 11 Achievements

* Implemented comprehensive Data-at-Rest and Data-in-Transit encryption strategies with AWS KMS.
* Secured web applications against web exploits (SQLi, XSS) using AWS WAF Web ACLs.
* Eliminated hardcoded secrets by integrating AWS Secrets Manager into application code.
* Mastered zero-downtime database migration strategies (DMS/SCT) and serverless analytics querying with Athena.
