---
title: "Test System Access through CloudFront"
date: 2026-07-10
weight: 5
chapter: false
pre: " <b> 5.9.5. </b> "
---

### 5.9.5. Test System Access through CloudFront

After creating the distribution, return to **CloudFront → Distributions**. Confirm that the distribution is **Enabled**, uses the ALB origin, and has received a default CloudFront domain name.

Open that domain and verify that the application responds normally through the CDN. Test sign-in and API requests in the browser network panel to confirm that CORS succeeds and dynamic responses are not incorrectly cached. The enabled state proves that the distribution exists; application tests are still required to prove end-to-end access.

![Kiểm tra hệ thống qua CloudFront](</images/5-Workshop/5.9-Tich-hop-CloudFront-CDN/5.9.5-Kiem-tra-truy-cap-he-thong-qua-CloudFront/cloudfront%205.png>)
