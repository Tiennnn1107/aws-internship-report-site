---
title: "Create a Target Group for the EC2 Backend"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.8.1. </b> "
---

### 5.8.1. Create a Target Group for the EC2 Backend

1. Open **EC2 → Target Groups → Create target group** and choose target type `Instances`.
2. Enter `recruit-backend-tg`, protocol HTTP, port `8080`, and VPC `RecruitVPC`.
3. Set the health check path to `/actuator/health`, or another public endpoint that returns HTTP 200, with success codes `200-399`.
4. Select the backend EC2 instance, choose **Include as pending below**, and create the target group.

The target must become `healthy`. If it does not, confirm that the application listens on `0.0.0.0:8080`, the EC2 security group accepts traffic from the ALB security group, and the health endpoint returns 200. Monitor `HealthyHostCount` and `UnHealthyHostCount`.

![Tạo Target Group](</images/5-Workshop/5.8-Public-ung-dung-voi-Application-Load-Balancer/5.8.1-Tao-Target-Group-cho-EC2-Backend/target%20group.png>)
![Cấu hình health check](</images/5-Workshop/5.8-Public-ung-dung-voi-Application-Load-Balancer/5.8.1-Tao-Target-Group-cho-EC2-Backend/target%20group%202.png>)
![Đăng ký EC2 target](</images/5-Workshop/5.8-Public-ung-dung-voi-Application-Load-Balancer/5.8.1-Tao-Target-Group-cho-EC2-Backend/target%20group%203.png>)
![Target healthy](</images/5-Workshop/5.8-Public-ung-dung-voi-Application-Load-Balancer/5.8.1-Tao-Target-Group-cho-EC2-Backend/target%201.1.png>)
