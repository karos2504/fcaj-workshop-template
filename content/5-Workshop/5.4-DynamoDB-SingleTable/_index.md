---
title: "DynamoDB Single-Table Design & Streams"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4 </b> "
---

# DynamoDB Single-Table Design & DynamoDB Streams CDC

In a Multi-Tenant SaaS platform, database architectural design directly dictates **infrastructure cost**, **query performance**, and **Tenant Data Isolation**.

In this module, you will examine the **Single-Table Design** pattern implemented in Amazon DynamoDB and explore real-time event streaming via **DynamoDB Streams (Change Data Capture)**.

---

### 1. Single-Table Schema Architecture

Rather than creating separate tables per tenant or per entity type, all application entities (Users, Attendance, Tenants, Subscriptions) reside within **1 single DynamoDB Table (`smart-attendance-database`)** using generic HASH (`PK`) and RANGE (`SK`) key attributes:

| Entity Type | Partition Key (`PK`) | Sort Key (`SK`) | Embedded Attributes |
| :--- | :--- | :--- | :--- |
| **Tenant Record** | `TENANT#<tenantId>` | `METADATA` | `tenantName`, `plan`, `status`, `createdAt` |
| **User Profile** | `TENANT#<tenantId>` | `USER#<userId>` | `email`, `fullName`, `role`, `department` |
| **Attendance Log** | `TENANT#<tenantId>` | `ATTENDANCE#<userId>#<timestamp>` | `checkInTime`, `checkOutTime`, `status`, `location` |
| **Subscription Billing**| `TENANT#<tenantId>` | `SUB#<billingId>` | `planTier`, `amount`, `paymentStatus`, `expiryDate` |

#### Ironclad Tenant Data Isolation
* Every DynamoDB Query executed by Lambda microservices **must** include the Partition Key formatted as `TENANT#<tenantId>`.
* This guarantees 100% data partition isolation, completely preventing cross-tenant data leaks.

---

### 2. Inspecting the DynamoDB Table on AWS Console

1. Open the [Amazon DynamoDB Console](https://console.aws.amazon.com/dynamodbv2/).
2. Select **Tables** -> Click `smart-attendance-database`.
3. Inspect the **Overview** tab:
   * **Read/Write capacity mode:** `On-Demand` (scales instantly with traffic).
   * **Encryption:** `KMS` (encrypted using Customer Managed Key `DataKMSKey`).
   * **Point-in-time recovery (PITR):** `ENABLED`.
   * **DynamoDB Streams:** `ENABLED (NEW_AND_OLD_IMAGES)`.

---

### 3. EventBridge Pipe Integration for CDC

To publish Change Data Capture (CDC) events without adding latency to the core Check-in Lambda, the system utilizes **AWS EventBridge Pipes**:

```yaml
DdbToEventBridgePipe:
  Type: AWS::Pipes::Pipe
  Properties:
    Name: smart-attendance-ddb-stream-pipe
    Source: !GetAtt SaaSAttendanceTable.StreamArn
    Target: !Sub 'arn:aws:events:${AWS::Region}:${AWS::AccountId}:event-bus/default'
```

* When a new attendance record is written, **DynamoDB Streams** emits a stream event containing the new record images.
* **EventBridge Pipe** automatically polls stream shards and dispatches `AttendanceCreated` events to the **EventBridge Event Bus**, triggering downstream email alerts and real-time webhooks.
