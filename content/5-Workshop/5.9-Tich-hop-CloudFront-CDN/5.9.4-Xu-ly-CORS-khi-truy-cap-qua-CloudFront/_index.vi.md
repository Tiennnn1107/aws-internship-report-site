---
title: "Xử lý CORS khi truy cập qua CloudFront"
date: 2026-07-10
weight: 4
chapter: false
pre: " <b> 5.9.4. </b> "
---

1. Cấu hình Spring Boot chỉ cho phép domain CloudFront/custom domain, các method và header thực sự dùng.
2. CloudFront phải forward header `Origin`, `Access-Control-Request-Method` và `Access-Control-Request-Headers` cho API.
3. Cho phép OPTIONS và không cache nhầm response giữa các Origin; thêm `Vary: Origin` khi cần.

![Cấu hình CORS](</images/5-Workshop/5.9-Tich-hop-CloudFront-CDN/5.9.4-Xu-ly-CORS-khi-truy-cap-qua-CloudFront/cloudfront%204.png>)

Kiểm thử preflight bằng `curl -i -X OPTIONS` với header Origin. Mong đợi HTTP 200/204 và `Access-Control-Allow-Origin` đúng domain, không dùng `*` khi gửi credential.
