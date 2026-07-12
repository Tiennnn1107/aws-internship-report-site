---
title: "Tạo Application Load Balancer"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.8.2. </b> "
---

## Các bước chi tiết

1. Tạo `recruit-alb-sg`: inbound HTTP 80 từ Internet; production nên thêm HTTPS 443 và giới hạn/redirect HTTP.
2. Vào **EC2 → Load Balancers → Create ALB**, tên `recruit-alb`, scheme `Internet-facing`, IP type IPv4.
3. Chọn `RecruitVPC` và hai public subnet ở hai AZ; chọn `recruit-alb-sg`.
4. Listener HTTP:80 forward tới `recruit-backend-tg`, sau đó tạo ALB.

![Security Group cho ALB](</images/5-Workshop/5.8-Public-ung-dung-voi-Application-Load-Balancer/5.8.2-Tao-Application-Load-Balancer/sg%20cho%20alb.png>)
![Bắt đầu tạo ALB](</images/5-Workshop/5.8-Public-ung-dung-voi-Application-Load-Balancer/5.8.2-Tao-Application-Load-Balancer/alb.png>)
![Chọn network và subnet](</images/5-Workshop/5.8-Public-ung-dung-voi-Application-Load-Balancer/5.8.2-Tao-Application-Load-Balancer/alb%202.png>)

## Xác minh và chi phí

Chờ trạng thái `Active`; DNS ALB phải trả ứng dụng. ALB tính phí theo giờ và LCU, vì vậy cần xóa khi kết thúc workshop.
