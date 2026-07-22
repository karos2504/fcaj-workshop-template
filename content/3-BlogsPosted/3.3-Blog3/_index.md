---
title: "Blog 3"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# Blog 3: Why You Should Migrate from gp2 to gp3

Hello everyone!

Amazon EBS (Elastic Block Store) is the primary block storage service used alongside Amazon EC2 instances for production cloud workloads. Over the years, many organizations have continued running large numbers of legacy **gp2 (General Purpose SSD)** volumes simply because it was previously the default choice on AWS.

However, since the launch of **gp3**, AWS has strongly recommended migrating to this next-generation storage type. Not only does gp3 cost significantly less, but it also delivers baseline performance guarantees and independent scalability. According to the **AWS Cost Optimization Hub**, migrating from gp2 to gp3 can save organizations **up to 20% on EBS storage costs** while boosting performance with zero application changes or downtime.

---

### 1. ARCHITECTURE & PERFORMANCE COMPARISON: gp2 VS gp3

The core distinction between the two volume types lies in how performance is provisioned:

* **gp2 (Performance Tied to Volume Size):** Baseline performance is strictly bound to storage capacity (3 IOPS/GB). If your application requires higher IOPS, you are forced to over-provision volume capacity (e.g., provisioning 1,000 GB just to achieve 3,000 IOPS), incurring unnecessary storage costs.
* **gp3 (Decoupled Capacity & Performance):** Storage capacity, IOPS, and throughput can be configured independently. Every gp3 volume provides a free baseline of **3,000 IOPS** and **125 MB/s Throughput** regardless of size. When higher performance is required, IOPS or throughput can be scaled independently without expanding volume size.

#### Quick Feature Comparison

* **Storage Pricing:** gp3 is up to 20% cheaper per GB/month across all AWS Regions.
* **Default Baseline IOPS:** gp2 yields 3 IOPS/GB (max 16,000 IOPS), whereas gp3 provides a fixed 3,000 IOPS baseline (scalable up to 16,000 IOPS).
* **Default Throughput:** gp2 ranges from 128 MB/s to 250 MB/s based on size, while gp3 provides a fixed 125 MB/s baseline (scalable up to 1,000 MB/s).
* **Scaling Flexibility:** gp2 requires purchasing more storage GB to scale performance, while gp3 allows scaling GB, IOPS, and Throughput independently.

---

### 2. CORE BENEFITS & PRIORITY WORKLOADS

* **Immediate FinOps Savings:** gp3 storage is 20% cheaper per GB/month. Across fleets running hundreds or thousands of volumes, this migration delivers substantial recurring monthly savings.
* **Zero-Downtime Live Migration:** Thanks to Amazon EBS Elastic Volumes, modifying a volume from gp2 to gp3 is an online operation. EC2 instances remain active with zero reboot, data migration, or application impact.

#### Recommended Priority Workloads for Migration

* Web Applications & API Gateways
* Small-to-Medium Databases (MySQL, PostgreSQL, MongoDB, SQL Server)
* Bastion Hosts & Monitoring Servers (Prometheus, Zabbix)
* CI/CD Worker Nodes (Jenkins, GitLab Runners)
* File Servers & Storage Nodes

---

### 3. AUDIT, AUTOMATION & MONITORING WORKFLOW FOR DEVOPS

To safely execute fleet-wide migrations, DevOps teams should follow this 3-step workflow:

* **Step 1: Audit Legacy gp2 Volumes**  
  Use AWS Cost Optimization Hub, AWS Cost Explorer, or AWS CLI scripts to identify candidate gp2 volumes and calculate projected savings.

* **Step 2: Automate Migration (IaC & Automation)**  
  Rather than manually updating volumes via the console, leverage AWS Systems Manager (SSM) Automation or Lambda scripts calling the `ModifyVolume` API. For Infrastructure as Code (Terraform / CloudFormation / AWS CDK), update the resource property `volume_type = "gp3"` in source repositories to prevent IaC drifts.

* **Step 3: Monitor Post-Migration CloudWatch Metrics**  
  After migration, track key Amazon CloudWatch metrics for 7–14 days:
  * `VolumeReadOps` & `VolumeWriteOps`: Calculate actual IOPS utilization.
  * `VolumeThroughputPercentage`: Monitor bandwidth utilization.
  * `VolumeConsumedReadWriteOps`: Ensure workloads do not experience IOPS throttling beyond the 3,000 baseline. Scale IOPS independently if required.

---

### CONCLUSION

Migrating from gp2 to gp3 is one of the highest ROI quick-win cost optimization actions on AWS. Organizations immediately cut storage expenses by 20% while gaining independent performance scaling with zero operational downtime. If your cloud infrastructure still runs legacy gp2 volumes, now is the ideal time to automate this upgrade.

* Reference Source: [AWS Storage Blog - Migrate your Amazon EBS volumes from gp2 to gp3 and save up to 20% on costs](https://aws.amazon.com/blogs/storage/migrate-your-amazon-ebs-volumes-from-gp2-to-gp3-and-save-up-to-20-on-costs/)

`#AWS` `#AmazonEBS` `#AWSStorage` `#CostOptimization` `#FinOps` `#AmazonEC2` `#CloudComputing` `#DevOps`
