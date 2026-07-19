---
title: "Handle CORS through CloudFront"
date: 2026-07-10
weight: 4
chapter: false
pre: " <b> 5.9.4. </b> "
---

### 5.9.4. Handle CORS through CloudFront

Use the recommended origin settings and customize the cache behavior for a dynamic web application:

- Allow the HTTP methods required by the application: `GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE`.
- Use `CachingDisabled` so authenticated and user-specific responses are not cached.
- Use an origin request policy that forwards the headers, cookies, and query strings required by authentication and CORS.
- Ensure the backend allows the CloudFront origin in its CORS configuration.

This configuration prioritizes API correctness. Production should redirect HTTP to HTTPS and forward only the request values the backend actually needs.

![Cấu hình CORS](</images/5-Workshop/5.9-Tich-hop-CloudFront-CDN/5.9.4-Xu-ly-CORS-khi-truy-cap-qua-CloudFront/cloudfront%204.png>)
