---
title: "Week 10 Worklog"
date: 2026-07-06
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Objectives

* **Basic Security Configuration Implementation:** Implement defense-in-depth security controls protecting data at rest, data in transit, API endpoints, and service IAM roles for the project.
* **Continued CloudJourney Learning:** Master AWS security standards, AWS KMS CMK encryption, Secrets Manager, and AWS WAF v2 configuration on CloudJourney (`https://cloudjourney.awsstudygroup.com/`).
* Ensure enterprise-grade security compliance and prevent sensitive data leaks.

### Tasks to be carried out this week

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | - **AWS Security Architecture Research (06/07/2026 – 12/07/2026):** <br>&emsp; + Study data encryption and key management modules on CloudJourney <br>&emsp; + Analyze 3-tier security architecture: Edge (WAF), Auth (Cognito/IAM), and Storage (KMS) | 06/07/2026 | 06/07/2026 | <https://cloudjourney.awsstudygroup.com> <br> <https://000033.awsstudygroup.com> |
| 3 | - **Data-at-Rest Encryption with AWS KMS (CMK):** <br>&emsp; + Create Customer Managed Keys (CMK) encrypting DynamoDB Single-Table and S3 export buckets <br>&emsp; + Configure KMS Key Policies restricting access to authorized Lambda execution roles | 07/07/2026 | 07/07/2026 | <https://000033.awsstudygroup.com> |
| 4 | - **Secrets & Credentials Management with AWS Secrets Manager:** <br>&emsp; + Store API keys, DB connection strings, and sensitive credentials inside AWS Secrets Manager <br>&emsp; + Enable automatic secrets rotation and programmatic retrieval from Lambda functions | 08/07/2026 | 08/07/2026 | <https://000096.awsstudygroup.com> |
| 5 | - **Edge Security Enforcement with AWS WAF v2:** <br>&emsp; + Associate WAF Web ACLs with CloudFront distribution and API Gateway HTTP API v2 <br>&emsp; + Enforce AWS Managed Rules (SQLi, XSS protections) and rate-limiting rules against DDoS | 09/07/2026 | 09/07/2026 | <https://000026.awsstudygroup.com> |
| 6 | - **IAM Least Privilege Audit & Security Testing:** <br>&emsp; + Audit IAM Execution Roles enforcing strict Least Privilege access for all Lambda functions <br>&emsp; + Perform baseline security audit across all API Gateway endpoints | 10/07/2026 | 10/07/2026 | <https://000002.awsstudygroup.com> |

### Week 10 Achievements

* Successfully completed basic security configuration across all layers of the project infrastructure.
* Continued advancing cloud security skills through curated CloudJourney learning materials.
* Encrypted all sensitive data at rest via AWS KMS CMK and shielded API endpoints with AWS WAF v2.


