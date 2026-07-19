---
title: "Create the EC2 Backend in a Private Subnet"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.6.1. </b> "
---

### 5.6.1. Create the EC2 Backend in a Private Subnet

## Goal and prerequisites

Run Spring Boot on an EC2 instance without a public IP. Complete the VPC, NAT or SSM connectivity, RDS security group, and IAM role first.

1. Create `recruit-ec2-sg` in `RecruitVPC`. Allow TCP `8080` only from `recruit-alb-sg`; do not expose SSH to `0.0.0.0/0`.
2. Open **EC2 → Launch instance**, name it `recruit-backend-01`, select Amazon Linux 2023, and choose `t3.micro`.
3. Select `RecruitVPC`, subnet `private-app-1a`, disable public IPv4 assignment, and attach `recruit-ec2-sg`.
4. Attach the IAM instance profile from section 5.6.2, configure 8–10 GiB gp3 storage, and launch the instance.
5. Connect with **Systems Manager → Session Manager** instead of public SSH.

Confirm that the instance is `running`, has no public IPv4 address, and appears as an `Online` SSM managed node. Monitor `CPUUtilization`, `NetworkIn/Out`, and `StatusCheckFailed` in CloudWatch.

Terminate the workshop instance and remove unused EBS volumes during cleanup.

![Cấu hình Security Group EC2](</images/5-Workshop/5.6-Trien-khai-Backend-voi-EC2/5.6.1-Tao-EC2-Backend-trong-Private-Subnet/sg%20cho%20ec2.png>)
![Bắt đầu tạo EC2](</images/5-Workshop/5.6-Trien-khai-Backend-voi-EC2/5.6.1-Tao-EC2-Backend-trong-Private-Subnet/ec2.png>)
![Chọn AMI và instance type](</images/5-Workshop/5.6-Trien-khai-Backend-voi-EC2/5.6.1-Tao-EC2-Backend-trong-Private-Subnet/ec2%202.png>)
![Cấu hình network](</images/5-Workshop/5.6-Trien-khai-Backend-voi-EC2/5.6.1-Tao-EC2-Backend-trong-Private-Subnet/ec2%203.png>)
![EC2 đang chạy](</images/5-Workshop/5.6-Trien-khai-Backend-voi-EC2/5.6.1-Tao-EC2-Backend-trong-Private-Subnet/ec2%204.png>)
