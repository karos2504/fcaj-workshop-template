---
title: "Blog 4"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 3.4. </b> "
---

# Blog 4: From Hourly Caching to Real-Time Pricing with AWS Lambda Response Streaming

Hello everyone!

In e-commerce, product pricing is one of the most critical data elements. A discrepancy between the price shown on a product page and the price at checkout can severely damage customer trust and experience.

Recently, I came across a fascinating case study on the AWS Architecture Blog regarding how **Samsung** modernized the pricing system for **Samsung.com** using **AWS Lambda Response Streaming** and **Amazon CloudFront**.

This is a compelling architectural case study demonstrating the value of choosing the right architecture pattern over blindly optimizing cache layers.

---

### 1. THE BUSINESS PROBLEM & CHALLENGE AT SAMSUNG.COM

Samsung.com serves as Samsung's direct-to-consumer sales channel, carrying diverse product lines including mobile devices, TVs, home appliances, and accessories.

During major promotional events like Black Friday, a single product catalog page might need to display live prices for over 30 distinct SKUs simultaneously. Each SKU carries multiple variations:

* Color variants & Memory storage capacity
* Active promotional discounts & Vouchers
* Region-specific pricing and localized offers

Evaluating real-time prices for complex variant combinations presents a major infrastructure and latency challenge.

---

### 2. LEGACY ARCHITECTURE & EMERGING BOTTLENECK

In the legacy architecture, Samsung placed a **Data Aggregation** layer between the Pricing Engine and Amazon CloudFront. An hourly Cron Job executed to:

1. Fetch all product master data from the Pricing Engine.
2. Pre-calculate all possible pricing permutations.
3. Store pre-computed results in a cache layer for user requests.

While this read-heavy model provided fast retrieval, it created two major operational flaws:

#### 1. Permutation Explosion
As product lines and promotional rules expanded, pre-calculated permutations grew exponentially. For instance, 30 products × multiple variants × regional promos produced tens of thousands of records pre-computed every hour—wasting massive compute and storage resources on data that users might never query.

#### 2. Synchronization Lag
A more critical issue was data staleness. Because the Cron Job ran hourly, cached prices could lag behind actual business pricing by up to 60 minutes. If a Flash Sale launched at 10:05 AM, customers still saw stale prices until the next cron run at 11:00 AM.

**Impact:**
* Inaccurate price displays
* Unexpected price changes at checkout
* Lost customer trust and negative revenue impact

---

### 3. MODERNIZED SOLUTION WITH AWS LAMBDA RESPONSE STREAMING

Instead of doubling down on caching, Samsung eliminated the Data Aggregation layer entirely. The new architecture operates on a fundamental principle: **Always fetch pricing from the Primary Source of Truth at request time.**

#### Request Execution Flow:
1. The user requests product price data.
2. **Amazon CloudFront** checks edge location cache.
3. On a cache miss, the request forwards to **AWS Lambda**.
4. Lambda fans out parallel requests to the **Pricing Engine**.
5. Pricing results stream back to the client immediately as chunks arrive.
6. CloudFront caches the response for a short TTL to optimize sub-second performance.

#### Why AWS Lambda Response Streaming?
Traditionally, AWS Lambda buffers the entire payload before returning a response, increasing wait times when aggregating data from multiple upstream calls.

With **Lambda Response Streaming**:
* Data chunks stream back to the client as soon as the first upstream call completes
* Significantly reduces **Time To First Byte (TTFB)**
* End users receive visible UI updates earlier
* Eliminates the need for a complex intermediate cache layer

---

### 4. AWS SERVICES FEATURED IN THE ARCHITECTURE

* **Amazon CloudFront:** Global edge distribution and short-TTL edge caching.
* **AWS Lambda:** Serverless compute executing pricing aggregation logic.
* **Lambda Response Streaming:** Streamed payload delivery reducing TTFB latency.
* **Lambda Function URL:** Direct HTTPS endpoint invoking Lambda from CloudFront.
* **Provisioned Concurrency:** Pre-warmed execution environments eliminating cold starts during peak traffic.

---

### CONCLUSION & ARCHITECTURAL TAKEAWAYS

The most insightful aspect of this architecture isn't just Lambda Response Streaming, but the underlying architectural mindset. Caching is frequently treated as the silver bullet for performance issues. However, when data accuracy outweighs raw retrieval speed, caching can become a source of business logic errors.

Samsung's case study highlights key principles:
* Adding cache layers isn't always the right architectural decision.
* **Source of Truth** must be prioritized in pricing and transaction systems.
* Serverless can effectively handle real-time data aggregation at massive scale.
* Simpler, decoupled architectures often outperform complex multi-tiered middleware.

* Reference Source: [AWS Architecture Blog - How Samsung achieved real-time pricing with AWS Lambda Response Streaming](https://aws.amazon.com/vi/blogs/architecture/how-samsung-achieved-real-time-pricing-with-aws-lambda-response-streaming/)

`#AWS` `#LambdaResponseStreaming` `#AmazonCloudFront` `#Serverless` `#RealTimePricing` `#SoftwareArchitecture` `#DevOps`
