---
title: "Optimizing Amazon EBS Costs: Why You Should Migrate from gp2 to gp3"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# Optimizing Amazon EBS Costs: Why You Should Migrate from gp2 to gp3

Amazon EBS (Elastic Block Store) is the primary block storage service powering production Amazon EC2 instances across cloud environments. Over the years, many enterprises have continued running large numbers of **gp2 (General Purpose SSD)** volumes simply because gp2 was previously the default choice on AWS.

However, since AWS introduced **gp3**, migrating from gp2 has become an industry best practice. Not only does gp3 deliver an immediate **20% savings on storage costs**, but it also provides higher baseline performance and complete configuration decoupling.

This migration represents one of the highest ROI quick-win cost optimization initiatives available to Cloud Operations and FinOps teams.

---

### THE PROBLEM

In large-scale cloud footprints running hundreds or thousands of EC2 instances, Amazon EBS storage comprises a major portion of the monthly AWS bill.

Continuing to run legacy gp2 volumes exposes organizations to several key cost and architectural inefficiencies:

* **20% Higher Storage Unit Costs:** The per-GB monthly price of gp2 is roughly 20% higher than gp3 across all AWS Regions.
* **Tightly Coupled Capacity and IOPS:** To get higher IOPS for performance-sensitive applications, teams are forced to provision unneeded extra storage capacity (GB).
* **Wasted Resources:** Workloads requiring high IOPS but small data footprints (such as DB log volumes or cache nodes) end up paying for bloated storage capacity just to acquire baseline IOPS.

---

### LEGACY ARCHITECTURE (gp2) AND ISSUES

In the legacy gp2 architecture, volume performance scales at a fixed ratio of **3 IOPS per 1 GB of provisioned storage**.

This architectural model creates two significant technical limitations:

#### 1. Capacity Coupling Wastes Money for IOPS
*Example:* A database workload requires 3,000 IOPS for transaction processing. With gp2, the volume must be provisioned to at least **1,000 GB** (1,000 GB × 3 = 3,000 IOPS). If the database only stores 100 GB of real data, the enterprise pays for 900 GB of unused storage every month.

#### 2. Size-Dependent Throughput Limits
gp2 throughput is tied to volume size. Small volumes (under 170 GB) suffer restricted throughput baselines, making them vulnerable to I/O throttling during traffic spikes.

---

### NEW ARCHITECTURE WITH AMAZON EBS gp3

The next-generation **gp3** volume type completely decouples **Storage Capacity, IOPS, and Throughput**.

**Zero-Downtime Migration Workflow:**
1. Audit existing gp2 volumes using **AWS Cost Optimization Hub** or **AWS CLI** scripts.
2. Execute the `ModifyVolume` API to change the volume type from `gp2` to `gp3` on live running volumes.
3. Leveraging **Amazon EBS Elastic Volumes**, the migration occurs transparently in the background without rebooting EC2 instances or stopping application services.
4. Update Infrastructure as Code (IaC) source files (Terraform / CloudFormation / AWS CDK) to set `volume_type = "gp3"`.

---

### WHY AMAZON EBS gp3 IS THE RIGHT FIT

* **Immediate 20% Cost Savings:** The per-GB storage price of gp3 is 20% lower than gp2 in every AWS Region.
* **Free High Baseline Performance:** Every gp3 volume includes a free baseline of **3,000 IOPS** and **125 MB/s Throughput** regardless of size (even on a 10 GB volume).
* **Independent Performance Tuning:** When an application demands 10,000 IOPS, engineers can scale IOPS independently without purchasing extra storage capacity.

---

### AWS SERVICES FEATURED IN THE ARCHITECTURE

* **Amazon EBS (Elastic Block Store):** Next-generation gp3 block storage volumes.
* **Amazon EC2:** Compute instances attached to live EBS volumes.
* **AWS Cost Optimization Hub & Cost Explorer:** Auditing and cost projection tools.
* **AWS Systems Manager (SSM) & AWS Lambda:** Automated batch migration workflows.
* **Amazon CloudWatch:** I/O metric monitoring (`VolumeReadOps`, `VolumeWriteOps`, `VolumeThroughputPercentage`).

---

### KEY ARCHITECTURAL LESSONS

Migrating from gp2 to gp3 is a textbook example of Cloud FinOps optimization delivering instant financial savings with zero technical risk.

**Key Lessons:**
* Continuously modernize cloud resource generations to take advantage of lower unit costs and improved performance baselines.
* Decoupled performance architectures allow organizations to align cloud spend precisely with actual operational requirements.
* Leverage zero-downtime Elastic Volume features to continuously improve cloud infrastructure without risking service availability.

* Original Article: [AWS Storage Blog - Migrate your Amazon EBS volumes from gp2 to gp3 and save up to 20% on costs](https://aws.amazon.com/blogs/storage/migrate-your-amazon-ebs-volumes-from-gp2-to-gp3-and-save-up-to-20-on-costs/)

`#AWS` `#AmazonEBS` `#AWSStorage` `#CostOptimization` `#FinOps` `#AmazonEC2` `#CloudComputing` `#DevOps`
