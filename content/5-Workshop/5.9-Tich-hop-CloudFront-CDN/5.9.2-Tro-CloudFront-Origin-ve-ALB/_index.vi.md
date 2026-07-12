---
title: "Trỏ CloudFront Origin về ALB"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.9.2. </b> "
---

1. Origin domain chọn DNS của `recruit-alb`; protocol `HTTP only` cho demo hoặc `HTTPS only` khi ALB có certificate.
2. Không thêm slash ở cuối origin domain; đặt connection attempts/timeouts phù hợp.
3. Lưu và chờ distribution deploy.

![Cấu hình ALB origin](</images/5-Workshop/5.9-Tich-hop-CloudFront-CDN/5.9.2-Tro-CloudFront-Origin-ve-ALB/cloudfront%202.png>)

Kiểm tra header `Via`/`X-Cache` bằng `curl -I https://<cloudfront-domain>/`. Production nên thêm secret header và rule ALB để hạn chế bypass CloudFront.
