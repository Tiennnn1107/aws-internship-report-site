---
title: "Cấu hình Cache Behavior cho ứng dụng động"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.9.3. </b> "
---

1. Với `/api/*`, chọn allowed methods gồm API cần dùng, cache policy `CachingDisabled` và origin request policy chuyển các header/query/cookie cần thiết.
2. Với tài nguyên tĩnh, dùng managed policy `CachingOptimized`.
3. Không forward toàn bộ cookie/header nếu ứng dụng không cần vì làm giảm cache hit ratio.

![Cấu hình cache behavior](</images/5-Workshop/5.9-Tich-hop-CloudFront-CDN/5.9.3-Cau-hinh-Cache-Behavior-cho-ung-dung-dong/cloudfront%203.png>)

Kiểm tra `X-Cache`: API động thường `Miss from cloudfront`; static asset request lần sau nên `Hit from cloudfront`. Theo dõi `CacheHitRate` và `OriginLatency`.
