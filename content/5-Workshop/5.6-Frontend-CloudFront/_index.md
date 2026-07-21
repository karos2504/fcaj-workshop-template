---
title: "Deploy Frontend & CloudFront CDN"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6 </b> "
---

# Deploy React SPA Frontend & CloudFront CDN

In this section, you will build the **React Single Page Application (SPA)** web frontend, upload static build artifacts to **Amazon S3**, and distribute the app globally over **Amazon CloudFront CDN** integrated with Custom Verification Headers (`x-origin-verify`).

---

### 1. Edge Protection Architecture

```
[User Browser] ➔ [Route 53] ➔ [Amazon CloudFront CDN (WAF + Shield)]
                                 ├──> [Amazon S3 Bucket (React Static Assets)]
                                 └──> [API Gateway (Header: x-origin-verify)]
```

* **Amazon S3 (`SpaBucket`):** Stores static `index.html`, `js`, `css`, and image assets for the React application. Direct public HTTP access to the bucket is blocked.
* **Amazon CloudFront:** Serves static content at low latency worldwide across edge locations.
* **Custom Verification Header (`x-origin-verify`):** CloudFront automatically injects a secret token header into all origin requests forwarded to API Gateway. API Gateway denies requests missing this secret header, protecting the API Gateway endpoint against direct bypass attacks.

---

### 2. Configure Environment Variables (`.env.production`)

Change directory into `frontend/` and populate the production environment configuration with your SAM deployment output values:

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

### 3. Build React Application

Install dependencies and compile the production bundle:

```bash
npm install
npm run build
```

The output build directory `dist/` is generated:

```text
dist/
├── assets/
│   ├── index-xxxx.js
│   └── index-xxxx.css
├── favicon.ico
└── index.html
```

---

### 4. Upload Assets to Amazon S3 Bucket

Use the AWS CLI to synchronize static assets from `dist/` to your S3 hosting bucket:

```bash
aws s3 sync dist/ s3://smart-attendance-spa-hosting-<AWS_ACCOUNT_ID> --delete
```

---

### 5. Verify & Invalidate CloudFront CDN Cache

1. Open the [Amazon CloudFront Console](https://console.aws.amazon.com/cloudfront/).
2. Select your distribution associated with `smart-attendance`.
3. Invalidate cached objects to immediately serve updated assets:
   ```bash
   aws cloudfront create-invalidation --distribution-id <DISTRIBUTION_ID> --paths "/*"
   ```
4. Access your CloudFront Domain URL (e.g., `https://dxxxxxxxxx.cloudfront.net`) in a web browser to verify the live application!
