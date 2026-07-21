---
title: "Week 9 Worklog"
date: 2026-06-29
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objectives

* **System Structure Diagram Editing & Architecture Design:** Review, refine, and edit the project structure diagram (`platform_architecture.drawio`), optimizing data flows across Edge, Auth, Compute, and Storage tiers.
* **Continued CloudJourney Learning:** Deepen knowledge of AWS Well-Architected architecture patterns and DynamoDB Single-Table Design on CloudJourney (`https://cloudjourney.awsstudygroup.com/`).
* Finalize architecture diagram blueprints and index definitions for project implementation.

### Tasks to be carried out this week

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | - **Project Structure Diagram Editing (29/06/2026 – 05/07/2026):** <br>&emsp; + Review and refine `platform_architecture.drawio` system architecture diagram for the SaaS Timekeeping Platform <br>&emsp; + Continue studying cloud architecture design modules on CloudJourney | 29/06/2026 | 29/06/2026 | <https://cloudjourney.awsstudygroup.com> |
| 3 | - **Data Flow Diagram Optimization:** <br>&emsp; + Update data transformation flows between API Gateway, Lambda functions, and DynamoDB Single-Table Design <br>&emsp; + Refine Partition Key (PK) and Sort Key (SK) isolation schemes by `tenantId` | 30/06/2026 | 30/06/2026 | <https://000060.awsstudygroup.com> <br> <https://000039.awsstudygroup.com> |
| 4 | - **Secondary Index (GSI) Diagram Refinement:** <br>&emsp; + Refine `GSI1-PK` / `GSI1-SK` layout for querying attendance history by department <br>&emsp; + Refine `GSI2-PK` / `GSI2-SK` layout for compiling tenant aggregate reports | 01/07/2026 | 01/07/2026 | <https://000060.awsstudygroup.com> |
| 5 | - **Authentication & Authorization Architecture Update:** <br>&emsp; + Update Amazon Cognito User Pool integration flow and Custom Claims (`{tenantId, role}`) <br>&emsp; + Study API security best practices on CloudJourney | 02/07/2026 | 02/07/2026 | <https://000141.awsstudygroup.com> |
| 6 | - **Architecture Finalization & API Specification:** <br>&emsp; + Finalize updated system architecture diagrams <br>&emsp; + Finalize OpenAPI/Swagger API specifications for API Gateway endpoints | 03/07/2026 | 03/07/2026 | <https://000066.awsstudygroup.com> |

### Week 9 Achievements

* Successfully edited and standardized system structure diagrams (`platform_architecture.drawio`) adhering to AWS Well-Architected principles.
* Continued learning and applied cloud design concepts from CloudJourney into project blueprints.
* Unified data flow diagrams, DynamoDB Single-Table schema, and API contracts across all microservices.
