---
title: "Create an Application Load Balancer"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.8.2. </b> "
---

### 5.8.2. Create an Application Load Balancer

1. Create `recruit-alb-sg` with inbound HTTP port 80 from the Internet. A production configuration should add HTTPS 443 and redirect or restrict HTTP.
2. Open **EC2 → Load Balancers → Create ALB**, enter `recruit-alb`, select `Internet-facing`, and use IPv4.
3. Select `RecruitVPC`, two public subnets in different AZs, and `recruit-alb-sg`.
4. Configure HTTP port 80 to forward to `recruit-backend-tg`, then create the ALB.

Wait for the ALB to become `Active` and test its DNS name. ALB pricing includes hourly and LCU charges, so remove it when the workshop ends.

![Security group for the ALB](</images/5-Workshop/5.8-Public-ung-dung-voi-Application-Load-Balancer/5.8.2-Tao-Application-Load-Balancer/sg%20cho%20alb.png>)
![Bắt đầu tạo ALB](</images/5-Workshop/5.8-Public-ung-dung-voi-Application-Load-Balancer/5.8.2-Tao-Application-Load-Balancer/alb.png>)
![Chọn network và subnet](</images/5-Workshop/5.8-Public-ung-dung-voi-Application-Load-Balancer/5.8.2-Tao-Application-Load-Balancer/alb%202.png>)
