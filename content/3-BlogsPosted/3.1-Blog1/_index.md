---
title: "From Hourly Caching to Real-Time Pricing: How Samsung Solved Price Syncing with AWS Lambda Response Streaming"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# From Hourly Caching to Real-Time Pricing: How Samsung Solved Price Syncing with AWS Lambda Response Streaming

In e-commerce, product pricing is one of the most critical data points. If the price displayed on a product listing page differs from the checkout price, customer trust and experience suffer immediately.

Recently, an insightful post on the AWS Architecture Blog highlighted how **Samsung** modernized the pricing system on Samsung.com using **AWS Lambda Response Streaming** and **Amazon CloudFront**.

This case study demonstrates how choosing the right architecture pattern outweighs merely tuning raw cache performance.

---

### THE PROBLEM

Samsung.com is Samsung's direct-to-consumer digital storefront, serving millions of shoppers for smartphones, TVs, home appliances, and accessories.

During major peak events like Black Friday, a single product catalog page may render prices for over 30 different SKUs simultaneously. Each product comes with multiple dynamic variables:

* Color variants & storage tiers
* Active promotional campaigns
* Regional and carrier-specific discounts

This complexity makes real-time price evaluation a formidable architectural challenge at scale.

---

### LEGACY ARCHITECTURE AND ISSUES

In the legacy architecture, Samsung used a Data Aggregation Layer positioned between the Pricing Engine and CloudFront. An hourly Cron Job executed to:

1. Fetch all product catalog data from the Pricing Engine.
2. Pre-calculate all potential pricing permutations.
3. Push pre-computed results into an intermediate cache layer.

While this improved read latencies, it introduced two major architectural bottlenecks:

#### 1. Permutation Explosion
As product SKUs and promotional rules expanded, pre-calculated pricing combinations grew exponentially.  
*Example:* 30 SKUs × multiple storage tiers × regional promos generated tens of thousands of records pre-computed hourly, wasting compute and storage resources on data shoppers never queried.

#### 2. Synchronization Lag
More critically, because the Cron Job ran hourly, cached prices lagged behind real-time pricing engines by up to 60 minutes.  
*If a Flash Sale launched at 10:05 AM, shoppers continued seeing pre-sale prices until the next Cron Job ran at 11:00 AM.*

**Impact:**
* Inaccurate pricing displays
* Price mismatch at checkout
* Loss of customer trust & cart abandonment
* Lost revenue opportunities

---

### NEW ARCHITECTURE WITH AWS LAMBDA RESPONSE STREAMING

Instead of optimizing an intermediate cache, Samsung eliminated the Data Aggregation layer entirely. The new architecture adheres to a core principle: **Always fetch pricing from the Source of Truth at request time.**

**Request Flow:**
1. User requests product list pricing.
2. Amazon CloudFront checks Edge Location cache.
3. On a cache miss, the request forwards to AWS Lambda.
4. Lambda performs fan-out calls in parallel to the underlying Pricing Engine.
5. Results are streamed back to the client immediately as data chunks arrive.
6. CloudFront caches the response for a short TTL to optimize performance.

---

### WHY AWS LAMBDA RESPONSE STREAMING IS THE RIGHT FIT

Traditionally, AWS Lambda waits for all internal requests to complete before returning a single payload, increasing Time To First Byte (TTFB).

With **Lambda Response Streaming**:
* Data chunks stream back to the client progressively as soon as available.
* Drastically reduces Time To First Byte (TTFB).
* End-users perceive faster page load performance.
* Eliminates the need for a complex intermediate caching infrastructure.

---

### AWS SERVICES FEATURED IN THE ARCHITECTURE

* **Amazon CloudFront:** Edge CDN providing intelligent caching.
* **AWS Lambda & Function URLs:** Serverless compute routing concurrent price evaluations.
* **Lambda Response Streaming:** Streams real-time payload chunks to clients.
* **Provisioned Concurrency:** Keeps execution environments warm, eliminating cold starts.

Though lightweight in service count, this pattern elegantly solves real-time data aggregation at global scale.

---

### KEY ARCHITECTURAL LESSONS

The most compelling takeaway is the architectural philosophy. Caching is frequently treated as a silver bullet for latency. However, when data accuracy trumps raw read speed, caching can become the root cause of business errors.

**Lessons from Samsung's case study:**
* Adding more cache layers is not always the right path.
* Source of Truth integrity must be prioritized for pricing applications.
* Serverless can handle heavy real-time data aggregation seamlessly.
* A simpler architecture often outperforms a multi-tiered cached system.

* Original Article: [AWS Architecture Blog - How Samsung achieved real-time pricing with AWS Lambda Response Streaming](https://aws.amazon.com/blogs/architecture/how-samsung-achieved-real-time-pricing-with-aws-lambda-response-streaming/)

`#AWS` `#AWSLambda` `#ResponseStreaming` `#AmazonCloudFront` `#Serverless` `#SystemArchitecture` `#ECommerce` `#CloudComputing`
