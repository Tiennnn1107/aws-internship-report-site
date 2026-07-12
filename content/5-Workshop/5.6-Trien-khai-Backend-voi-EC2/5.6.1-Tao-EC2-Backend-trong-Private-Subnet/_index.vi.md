---
title: "Tạo EC2 Backend trong Private Subnet"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.6.1. </b> "
---

## Mục tiêu và điều kiện đầu vào

Chạy Spring Boot trên EC2 không có public IP. Cần hoàn tất VPC, NAT/SSM, RDS Security Group và IAM Role.

## Các bước chi tiết

1. Tạo `recruit-ec2-sg` trong `RecruitVPC`. Inbound chỉ cho TCP `8080` từ `recruit-alb-sg`; không mở SSH `0.0.0.0/0`.
2. Vào **EC2 → Launch instance**, đặt tên `recruit-backend-01`, chọn Amazon Linux 2023, loại `t3.micro`.
3. Network: `RecruitVPC`, `private-app-1a`, **Auto-assign public IP: Disable**, chọn `recruit-ec2-sg`.
4. Gắn IAM instance profile ở mục 5.6.2; storage gp3 8–10 GiB; launch instance.
5. Dùng **Systems Manager → Session Manager** để kết nối thay vì public SSH.

![Cấu hình Security Group EC2](</images/5-Workshop/5.6-Trien-khai-Backend-voi-EC2/5.6.1-Tao-EC2-Backend-trong-Private-Subnet/sg%20cho%20ec2.png>)
![Bắt đầu tạo EC2](</images/5-Workshop/5.6-Trien-khai-Backend-voi-EC2/5.6.1-Tao-EC2-Backend-trong-Private-Subnet/ec2.png>)
![Chọn AMI và instance type](</images/5-Workshop/5.6-Trien-khai-Backend-voi-EC2/5.6.1-Tao-EC2-Backend-trong-Private-Subnet/ec2%202.png>)
![Cấu hình network](</images/5-Workshop/5.6-Trien-khai-Backend-voi-EC2/5.6.1-Tao-EC2-Backend-trong-Private-Subnet/ec2%203.png>)
![EC2 đang chạy](</images/5-Workshop/5.6-Trien-khai-Backend-voi-EC2/5.6.1-Tao-EC2-Backend-trong-Private-Subnet/ec2%204.png>)

## Xác minh và metric

Instance ở trạng thái `running`, không có Public IPv4; SSM managed node phải `Online`. Theo dõi `CPUUtilization`, `NetworkIn/Out`, `StatusCheckFailed` trên CloudWatch.

## Clean-up

Terminate instance sau workshop; kiểm tra và xóa EBS volume không còn sử dụng.
