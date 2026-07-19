---
title: "Integrate Amazon CloudFront CDN"
date: 2026-07-10
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---

## 5.9. Integrate Amazon CloudFront CDN

This section places Amazon CloudFront in front of the ALB. The distribution uses the ALB as its origin, disables caching for dynamic authenticated requests, forwards the required request data, and provides a CloudFront domain for application access.
