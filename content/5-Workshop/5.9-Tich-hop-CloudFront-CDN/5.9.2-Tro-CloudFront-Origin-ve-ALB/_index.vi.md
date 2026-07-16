---
title: "Khai báo thông tin Distribution"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.9.2. </b> "
---

## 5.9.2. Khai báo thông tin Distribution

Ở bước **Get started**, nhập tên distribution là `cloudfront_recruit`. Tên này được AWS lưu dưới dạng thẻ (tag) để nhận diện tài nguyên và có thể thay đổi sau khi tạo.

![Khai báo thông tin CloudFront Distribution](</images/5-Workshop/5.9-Tich-hop-CloudFront-CDN/5.9.2-Tro-CloudFront-Origin-ve-ALB/cloudfront%202.png>)

Mục **Distribution type** được đặt là **Single website or app**, phù hợp vì RecruitBox là một ứng dụng có cấu hình CloudFront riêng. Trường **Route 53 managed domain** được để trống do chưa gắn tên miền tùy chỉnh; sau khi tạo, hệ thống sẽ sử dụng tên miền mặc định do CloudFront cấp. Nhấn **Next** để chuyển sang bước chọn origin.
