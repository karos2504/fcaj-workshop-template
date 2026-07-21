---
title: "Deploying Frontend & CloudFront CDN"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6 </b> "
---

# Deploying React SPA Frontend & CloudFront CDN

In this section, you will compile the user-facing **React Single Page Application (SPA)**, deploy static web artifacts to an **Amazon S3 Bucket**, and serve the application globally via **Amazon CloudFront CDN** integrated with Custom Verification Header security (`x-origin-verify`).

---

### 1. Edge Protection Architecture

```
[User Browser] ➔ [Route 53] ➔ [Amazon CloudFront CDN (WAF + Shield)]
                                 ├──> [Amazon S3 Bucket (React Static Assets)]
                                 └──> [API Gateway (Header: x-origin-verify)]
```

* **Amazon S3 (`SpaBucket`):** Stores static `index.html`, `js`, `css`, and asset files. Public internet access is completely blocked directly on the S3 bucket policy.
* **Amazon CloudFront:** Distributes static content to global Edge Locations with minimal latency.
* **Custom Verification Header (`x-origin-verify`):** CloudFront automatically injects a secret token header on all API requests routed to API Gateway. API Gateway denies any direct incoming traffic that lacks this secret header, protecting origin APIs from bypassing CloudFront/WAF safeguards.

---

### 2. Configure Environment Variables (`.env.production`)

Navigate to the `frontend/` directory and configure production variables with the API endpoints output from Lab 5.3:

```bash
cd ../frontend
```

Create `.env.production`:

```ini
VITE_API_BASE_URL=https://xxxxxxx.execute-api.us-east-1.amazonaws.com/prod
VITE_COGNITO_USER_POOL_ID=us-east-1_xxxxxxxxx
VITE_COGNITO_CLIENT_ID=xxxxxxxxxxxxxxxxxxxxxxxxxx
VITE_AWS_REGION=us-east-1
```

---

### 3. Build the React Application

Install frontend dependencies and build the static assets:

```bash
npm install
npm run build
```

The production bundle is compiled into the `dist/` directory:

```text
dist/
├── assets/
│   ├── index-xxxx.js
│   └── index-xxxx.css
├── favicon.ico
└── index.html
```

---

### 4. Upload Assets to Amazon S3

Sync the compiled `dist/` directory to your S3 SPA Hosting Bucket using AWS CLI:

```bash
aws s3 sync dist/ s3://smart-attendance-spa-hosting-<AWS_ACCOUNT_ID> --delete
```

---

### 5. Verify Site Distribution on CloudFront

1. Open the [Amazon CloudFront Console](https://console.aws.amazon.com/cloudfront/).
2. Select your `smart-attendance` distribution.
3. Issue a cache **Invalidation** to refresh CDN edge nodes:
   ```bash
   aws cloudfront create-invalidation --distribution-id <DISTRIBUTION_ID> --paths "/*"
   ```
4. Navigate to your CloudFront domain URL (e.g. `https://dxxxxxxxxx.cloudfront.net`) in your web browser to test the web interface!
