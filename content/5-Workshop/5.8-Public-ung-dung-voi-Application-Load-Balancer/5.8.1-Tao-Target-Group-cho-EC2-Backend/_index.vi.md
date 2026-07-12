---
title: "Tạo Target Group cho EC2 Backend"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.8.1. </b> "
---

## Các bước chi tiết

1. Vào **EC2 → Target Groups → Create target group**, target type `Instances`.
2. Đặt tên `recruit-backend-tg`, protocol HTTP, port `8080`, VPC `RecruitVPC`.
3. Health check path `/actuator/health` (hoặc endpoint public trả HTTP 200), success codes `200-399`.
4. Chọn EC2 backend → **Include as pending below → Create target group**.

![Tạo Target Group](</images/5-Workshop/5.8-Public-ung-dung-voi-Application-Load-Balancer/5.8.1-Tao-Target-Group-cho-EC2-Backend/target%20group.png>)
![Cấu hình health check](</images/5-Workshop/5.8-Public-ung-dung-voi-Application-Load-Balancer/5.8.1-Tao-Target-Group-cho-EC2-Backend/target%20group%202.png>)
![Đăng ký EC2 target](</images/5-Workshop/5.8-Public-ung-dung-voi-Application-Load-Balancer/5.8.1-Tao-Target-Group-cho-EC2-Backend/target%20group%203.png>)
![Target healthy](</images/5-Workshop/5.8-Public-ung-dung-voi-Application-Load-Balancer/5.8.1-Tao-Target-Group-cho-EC2-Backend/target%201.1.png>)

## Xác minh và metric

Target phải `healthy`. Nếu lỗi, kiểm tra ứng dụng listen `0.0.0.0:8080`, EC2 SG cho phép từ ALB SG và health path trả 200. Theo dõi `HealthyHostCount`, `UnHealthyHostCount`.
