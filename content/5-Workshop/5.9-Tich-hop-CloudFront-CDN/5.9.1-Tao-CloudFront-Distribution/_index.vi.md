---
title: "Tạo CloudFront Distribution"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.9.1. </b> "
---

## Các bước chi tiết

1. Vào **CloudFront → Create distribution**.
2. Chọn ALB làm origin, đặt tên `recruit-alb-origin`.
3. Viewer protocol policy: `Redirect HTTP to HTTPS`; allowed methods theo nhu cầu API.
4. Chọn price class phù hợp và tạo distribution.

![Tạo CloudFront Distribution](</images/5-Workshop/5.9-Tich-hop-CloudFront-CDN/5.9.1-Tao-CloudFront-Distribution/cloudfront.png>)

## Xác minh

Chờ Status `Deployed`; truy cập domain `d....cloudfront.net` phải tải được ứng dụng qua HTTPS.
