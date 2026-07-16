---
title: "Cấu hình Cache Behavior cho ứng dụng động"
date: 2026-07-10
weight: 4
chapter: false
pre: " <b> 5.9.4. </b> "
---

## 5.9.4. Cấu hình Cache Behavior cho ứng dụng động

Trong phần **Settings**, giữ **Use recommended origin settings** và chọn **Customize cache settings** để cấu hình phù hợp với ứng dụng web động.

![Cấu hình cache behavior cho RecruitBox](</images/5-Workshop/5.9-Tich-hop-CloudFront-CDN/5.9.4-Xu-ly-CORS-khi-truy-cap-qua-CloudFront/cloudfront%204.png>)

Hình cho thấy các thiết lập sau:

- **Viewer protocol policy:** `HTTP and HTTPS`, cho phép người dùng truy cập bằng cả hai giao thức.
- **Allowed HTTP methods:** cho phép đầy đủ `GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE` để các chức năng đăng nhập, cập nhật hồ sơ và upload CV hoạt động qua CloudFront.
- **Cache HTTP methods:** không chọn cache `OPTIONS`; CloudFront chỉ áp dụng mặc định cho `GET` và `HEAD`.
- **Cache policy:** `CachingDisabled`, tránh lưu cache các phản hồi động hoặc dữ liệu riêng của người dùng.
- **Origin request policy:** `AllViewer`, chuyển các thông tin trong request của người dùng về ALB để backend xử lý.

Cấu hình này ưu tiên tính đúng đắn của API. Trong môi trường production, nên chuyển viewer protocol policy sang **Redirect HTTP to HTTPS** và chỉ chuyển tiếp các header, cookie, query string thật sự cần thiết.
