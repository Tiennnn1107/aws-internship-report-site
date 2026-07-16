---
title: "Chọn Application Load Balancer làm Origin"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.9.3. </b> "
---

## 5.9.3. Chọn Application Load Balancer làm Origin

Tại bước **Specify origin**, chọn loại origin là **Elastic Load Balancer** vì ứng dụng RecruitBox đang được phục vụ thông qua Application Load Balancer.

![Chọn Application Load Balancer làm origin](</images/5-Workshop/5.9-Tich-hop-CloudFront-CDN/5.9.3-Cau-hinh-Cache-Behavior-cho-ung-dung-dong/cloudfront%203.png>)

Trong trường **Elastic Load Balancing origin**, chọn ALB có DNS `recruit-alb-1002681411.ap-southeast-1.elb.amazonaws.com`. Trường **Origin path** không cần nhập vì ứng dụng được phục vụ từ đường dẫn gốc của ALB. Với cấu hình này, CloudFront tiếp nhận request từ người dùng rồi chuyển tiếp request về ALB để phân phối đến backend.
