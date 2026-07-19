---
title: "Test Application Access through the ALB DNS Name"
date: 2026-07-10
weight: 4
chapter: false
pre: " <b> 5.8.4. </b> "
---

### 5.8.4. Test Application Access through the ALB DNS Name

1. Copy the ALB **DNS name** and open `http://<alb-dns>/`.
2. Run `curl -i http://<alb-dns>/actuator/health` and expect HTTP 200.
3. Send several requests and inspect ALB or CloudWatch metrics including `RequestCount`, `TargetResponseTime`, and `HTTPCode_Target_5XX_Count`.

For HTTP 503, check target health. For a timeout, inspect route tables, NACLs, and the ALB-to-EC2 security-group chain.

![Ứng dụng truy cập qua ALB](</images/5-Workshop/5.8-Public-ung-dung-voi-Application-Load-Balancer/5.8.4-Kiem-tra-truy-cap-ung-dung-qua-ALB-DNS/alb%205.png>)
