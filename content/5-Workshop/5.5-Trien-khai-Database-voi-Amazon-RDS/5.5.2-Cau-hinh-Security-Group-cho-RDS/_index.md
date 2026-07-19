---
title: "Configure the Security Group for RDS"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.5.2. </b> "
---

### 5.5.2. Configure the Security Group for RDS

1. Open **EC2 → Security Groups → Create security group**.
2. Create `recruit-rds-sg` in `RecruitVPC`.
3. Add one inbound rule: `MySQL/Aurora`, TCP `3306`, with the **EC2 backend security group** as its source.
4. Do not use `0.0.0.0/0` and do not enable public RDS access.

Validate that the backend EC2 instance can reach port 3306 while clients outside the VPC cannot connect to the RDS endpoint.

![Security group allowing MySQL access only from EC2](</images/5-Workshop/5.5-Trien-khai-Database-voi-Amazon-RDS/5.5.2-Cau-hinh-Security-Group-cho-RDS/Screenshots-20260712221530.png>)
