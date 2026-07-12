---
title: "Kiểm tra truy cập hệ thống qua CloudFront"
date: 2026-07-10
weight: 5
chapter: false
pre: " <b> 5.9.5. </b> "
---

1. Truy cập `https://<distribution-domain>/`, đăng nhập và thực hiện các API chính.
2. Dùng DevTools xác nhận không có mixed content/CORS error và mọi request đi qua CloudFront.
3. Chạy `curl -I` hai lần với static asset để quan sát `X-Cache`; kiểm thử API không trả dữ liệu cache của người dùng khác.

![Kiểm tra hệ thống qua CloudFront](</images/5-Workshop/5.9-Tich-hop-CloudFront-CDN/5.9.5-Kiem-tra-truy-cap-he-thong-qua-CloudFront/cloudfront%205.png>)

Theo dõi `Requests`, `4xxErrorRate`, `5xxErrorRate`, `CacheHitRate`. Khi clean-up, disable distribution, chờ Deployed rồi mới delete.
