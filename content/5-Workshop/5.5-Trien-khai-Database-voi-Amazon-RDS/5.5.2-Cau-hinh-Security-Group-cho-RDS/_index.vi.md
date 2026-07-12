---
title: "Cấu hình Security Group cho RDS"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.5.2. </b> "
---

## Các bước chi tiết

1. Vào **EC2 → Security Groups → Create security group**.
2. Tạo `recruit-rds-sg` trong `RecruitVPC`.
3. Inbound: `MySQL/Aurora`, TCP `3306`, **Source = Security Group của EC2 backend**.
4. Không dùng nguồn `0.0.0.0/0` và không mở public access cho RDS.

![Security Group chỉ cho EC2 truy cập MySQL](</images/5-Workshop/5.5-Trien-khai-Database-voi-Amazon-RDS/5.5.2-Cau-hinh-Security-Group-cho-RDS/Screenshots-20260712221530.png>)

## Xác minh

Máy EC2 backend kết nối được port 3306; máy ngoài VPC không thể kết nối endpoint RDS.
