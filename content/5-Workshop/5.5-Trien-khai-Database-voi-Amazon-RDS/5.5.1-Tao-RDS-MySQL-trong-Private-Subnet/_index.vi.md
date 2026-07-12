---
title: "Tạo RDS MySQL trong Private Subnet"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.5.1. </b> "
---

## Điều kiện đầu vào

Có hai private DB subnet ở hai AZ và Security Group RDS ở mục 5.5.2.

## Các bước chi tiết

1. Vào **RDS → Subnet groups**, tạo `recruit-db-subnet-group`, chọn `RecruitVPC` và hai DB subnet.
2. Chọn **Databases → Create database → Standard create → MySQL**.
3. Chọn template `Free tier` hoặc `Dev/Test`, DB identifier `recruit-db`, instance `db.t3.micro`/`db.t4g.micro`.
4. Nhập master username, lưu mật khẩu trong Secrets Manager hoặc password manager; không ghi vào source code.
5. Connectivity: chọn `RecruitVPC`, subnet group vừa tạo, **Public access: No**, chọn RDS Security Group.
6. Database name `recruitbox`, port `3306`, bật backup và Performance Insights nếu ngân sách cho phép.

![Bắt đầu tạo RDS](</images/5-Workshop/5.5-Trien-khai-Database-voi-Amazon-RDS/5.5.1-Tao-RDS-MySQL-trong-Private-Subnet/rds%201.png>)
![Chọn MySQL](</images/5-Workshop/5.5-Trien-khai-Database-voi-Amazon-RDS/5.5.1-Tao-RDS-MySQL-trong-Private-Subnet/rds%202.png>)
![Cấu hình identifier](</images/5-Workshop/5.5-Trien-khai-Database-voi-Amazon-RDS/5.5.1-Tao-RDS-MySQL-trong-Private-Subnet/rds%203.png>)
![Chọn instance class](</images/5-Workshop/5.5-Trien-khai-Database-voi-Amazon-RDS/5.5.1-Tao-RDS-MySQL-trong-Private-Subnet/rds%204.png>)
![Cấu hình storage](</images/5-Workshop/5.5-Trien-khai-Database-voi-Amazon-RDS/5.5.1-Tao-RDS-MySQL-trong-Private-Subnet/rds%205.png>)
![Cấu hình connectivity](</images/5-Workshop/5.5-Trien-khai-Database-voi-Amazon-RDS/5.5.1-Tao-RDS-MySQL-trong-Private-Subnet/rds%206.png>)
![Cấu hình database](</images/5-Workshop/5.5-Trien-khai-Database-voi-Amazon-RDS/5.5.1-Tao-RDS-MySQL-trong-Private-Subnet/rds%207.png>)
![RDS Available](</images/5-Workshop/5.5-Trien-khai-Database-voi-Amazon-RDS/5.5.1-Tao-RDS-MySQL-trong-Private-Subnet/rds%208.png>)

## Xác minh

Trạng thái `Available`, `Publicly accessible: No`; sao chép endpoint để dùng trong biến môi trường của Spring Boot.
