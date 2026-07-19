---
title: "Tích hợp CloudFront CDN"
date: 2026-07-10
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---

## 5.9. Tích hợp CloudFront CDN

Phần này đặt Amazon CloudFront phía trước ALB. Distribution sử dụng ALB làm origin, tắt cache đối với request động có xác thực, chuyển tiếp dữ liệu request cần thiết và cung cấp CloudFront domain để truy cập ứng dụng.
