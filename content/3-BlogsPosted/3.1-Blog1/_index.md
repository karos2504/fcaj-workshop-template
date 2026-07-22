---
title: "AWS ARCHITECTURE CASE STUDY – Samsung Achieves Real-Time Pricing with AWS Lambda Response Streaming"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# AWS ARCHITECTURE CASE STUDY – From Hourly Caching to Real-Time Pricing: How Samsung Solved Price Syncing with AWS Lambda Response Streaming

Hello everyone!

In e-commerce, product pricing is one of the most critical data points. If the price displayed on a product listing page differs from the checkout page, customer experience suffers severely, damaging brand trust and impacting conversion rates.

Today, I would like to share an architectural case study from the **AWS Architecture Blog** detailing how **Samsung** modernized its pricing engine on **Samsung.com** by leveraging **AWS Lambda Response Streaming** and **Amazon CloudFront**.

This case study is a textbook example of choosing the right architectural principles (prioritizing the Source of Truth) over blindly relying on multi-tier caching layers.

---

### 1. THE BUSINESS PROBLEM & OPERATIONAL CHALLENGES

**Samsung.com** is Samsung's Direct-to-Consumer (D2C) flagship portal, serving millions of global shoppers across diverse product lineups—smartphones, tablets, TVs, home appliances, and accessories.

During major shopping events such as **Black Friday** or **Flash Sales**:
* A single Product Listing Page (PLP) must render real-time prices for over **30 different SKUs** simultaneously.
* Each SKU contains multiple complex permutations: *Colors, storage capacities, time-sensitive promotional discounts, regional pricing, and carrier trade-in offers*.

Querying and rendering accurate prices across thousands of concurrent sessions in real time presents an immense technical challenge regarding both latency and infrastructure cost.

---

### 2. LEGACY ARCHITECTURE & CORE BOTTLENECK

In the legacy architecture, Samsung placed an intermediary **Data Aggregation Layer** between their core **Pricing Engine** and the **Amazon CloudFront CDN**.

An automated **Cron Job** executed hourly to:
1. Fetch all product master data from the Pricing Engine.
2. Pre-compute all potential price permutations.
3. Store pre-calculated pricing records into a cache tier to serve user requests.

While this approach provided fast read operations, it introduced two major operational flaws:

#### A. Permutation Explosion
As product lines and promotional rules grew, pre-computed price combinations expanded **exponentially**.
> *Example:* 30 products × multiple storage options × colors × regional promos created **tens of thousands of cached records**. The system wasted compute and storage resources processing price combinations that users never actually requested.

#### B. Synchronization Lag
This flaw directly harmed revenue. Because the Cron Job ran only **once every 60 minutes**, cached pricing data could lag behind live promotion updates by up to an hour.
> *Impact Scenario:* If a Flash Sale started at **10:05 AM**, customers visiting at **10:15 AM** would still see pre-sale pricing until the next scheduled Cron Job ran at **11:00 AM**.
> * **Consequence:** Mismatched prices, customer frustration during checkout, abandoned carts, and loss of brand credibility.

---

### 3. THE NEW SOLUTION WITH AWS LAMBDA RESPONSE STREAMING

Instead of attempting to further optimize the complex cache layer, Samsung made a bold architectural decision: **Completely eliminate the intermediary Data Aggregation Layer**.

The new architecture operates on a fundamental principle: **Always query prices directly from the Source of Truth at the exact moment a user issues a request.**

```
[User Browser] ➔ [Amazon CloudFront Edge] ➔ (Cache Miss) ➔ [AWS Lambda Function URL] 
                                                                    │
                                            ┌───────────────────────┴───────────────────────┐
                                            ▼                                               ▼
                              [Fan-out API Request 1]                         [Fan-out API Request 2]
                                            │                                               │
                                            └───────────────────────┬───────────────────────┘
                                                                    ▼
                                                         [Pricing Engine Service]
                                                                    │
                                                (Stream chunks via Response Streaming)
                                                                    ▼
                                                     [Stream Response back to Client]
```

#### Real-Time Execution Workflow:
1. A user accesses a product page on Samsung.com.
2. **Amazon CloudFront** checks Edge Location cache.
3. Upon a Cache Miss, CloudFront routes the request to an **AWS Lambda Function URL**.
4. The Lambda function executes a **Fan-out pattern**, sending parallel API requests to the Pricing Engine to fetch prices for 30+ SKUs concurrently.
5. As pricing data chunks for initial items return from the Pricing Engine, Lambda leverages **Response Streaming** to push HTTP payload chunks back to the browser immediately without waiting for all 30 SKUs to finish processing.
6. CloudFront applies short-lived edge caching to optimize subsequent duplicate requests.

---

### 4. WHY AWS LAMBDA RESPONSE STREAMING IS THE GAME CHANGER

Traditionally, AWS Lambda functions buffer the complete response in memory before returning the final JSON payload to the caller. When aggregating multiple backend services, latency accumulates.

With **AWS Lambda Response Streaming**:
* **Immediate Chunked Data Delivery:** Lambda streams HTTP response chunks to the browser as soon as the first backend service responds.
* **Drastically Lower Time To First Byte (TTFB):** The client browser begins rendering UI elements and displaying initial product prices without delay.
* **Simplified Infrastructure:** Removes the overhead of maintaining expensive Redis/ElastiCache clusters and complex cache synchronization scripts.

---

### 5. AWS SERVICES FEATURED IN THE ARCHITECTURE

| AWS Service | Architectural Role on Samsung.com |
| :--- | :--- |
| **Amazon CloudFront** | Edge CDN distribution layer providing short-lived caching and request security. |
| **AWS Lambda** | Serverless Compute Engine executing parallel fan-out pricing requests. |
| **Lambda Response Streaming** | Streamed HTTP payload delivery mechanism optimizing TTFB performance. |
| **Lambda Function URL** | Dedicated HTTPS endpoint invoking Lambda with minimal routing overhead. |
| **Provisioned Concurrency** | Keeps Lambda functions warm, completely eliminating Cold Start latency during peak traffic spikes. |

---

### 6. ARCHITECTURAL TAKEAWAYS & LESSONS LEARNED

The greatest insight from Samsung's case study goes beyond Lambda Response Streaming—it highlights **Architectural Mindset**:

1. **Caching is Not a Universal Cure:** Caching excels at speed, but in domains where **Data Accuracy** trumps raw retrieval velocity, caching can become a primary root cause of business errors.
2. **Prioritize the Source of Truth:** For financial, pricing, or inventory systems, always query live data from the primary authoritative source during transactions.
3. **The Power of Serverless Streaming:** Modern Serverless is no longer limited to short REST API calls; it excels at real-time stream processing and data aggregation at massive scale.
4. **Less is More:** A simplified architecture with fewer intermediary moving parts is easier to maintain, eliminates Single Points of Failure, and delivers superior reliability.

---

* Original Article on AWS Blog: [How Samsung achieved real-time pricing with AWS Lambda Response Streaming](https://aws.amazon.com/vi/blogs/architecture/how-samsung-achieved-real-time-pricing-with-aws-lambda-response-streaming/)

`#AWS` `#Serverless` `#AWSLambda` `#LambdaResponseStreaming` `#AmazonCloudFront` `#CloudArchitecture` `#SystemDesign` `#CaseStudy` `#DevOps`
