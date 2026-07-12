---
title: "Kiểm tra truy cập ứng dụng qua ALB DNS"
date: 2026-07-10
weight: 4
chapter: false
pre: " <b> 5.8.4. </b> "
---

## Kiểm thử

1. Sao chép **DNS name** của ALB và mở `http://<alb-dns>/`.
2. Chạy `curl -i http://<alb-dns>/actuator/health`; mong đợi HTTP 200.
3. Gửi nhiều request và kiểm tra ALB access log/CloudWatch `RequestCount`, `TargetResponseTime`, `HTTPCode_Target_5XX_Count`.

![Ứng dụng truy cập qua ALB](</images/5-Workshop/5.8-Public-ung-dung-voi-Application-Load-Balancer/5.8.4-Kiem-tra-truy-cap-ung-dung-qua-ALB-DNS/alb%205.png>)

Nếu nhận 503, kiểm tra target healthy; nếu timeout, kiểm tra route table, NACL và chuỗi Security Group ALB → EC2.
