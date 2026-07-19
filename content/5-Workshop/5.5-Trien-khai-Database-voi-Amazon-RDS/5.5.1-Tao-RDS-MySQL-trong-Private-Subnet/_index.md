---
title: "Create RDS for MySQL in a Private Subnet"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.5.1. </b> "
---

### 5.5.1. Create RDS for MySQL in a Private Subnet

## Prerequisites

Prepare two private database subnets in different AZs and the RDS security group described in section 5.5.2.

## Steps

1. Open **RDS → Subnet groups** and create `recruit-db-subnet-group` using `RecruitVPC` and both database subnets.
2. Select **Databases → Create database → Standard create → MySQL**.
3. Choose `Free tier` or `Dev/Test`, identifier `recruit-db`, and an appropriate small instance class.
4. Set the master username and store its password securely; never commit it to source code.
5. Select `RecruitVPC`, the new subnet group, **Public access: No**, and the RDS security group.
6. Set the initial database name to `recruitbox`, port `3306`, and enable backups. Enable Performance Insights only when the budget permits.

Confirm that the database becomes `Available` and remains not publicly accessible. Copy its endpoint for the Spring Boot environment variables.

![Bắt đầu tạo RDS](</images/5-Workshop/5.5-Trien-khai-Database-voi-Amazon-RDS/5.5.1-Tao-RDS-MySQL-trong-Private-Subnet/rds%201.png>)
![Chọn MySQL](</images/5-Workshop/5.5-Trien-khai-Database-voi-Amazon-RDS/5.5.1-Tao-RDS-MySQL-trong-Private-Subnet/rds%202.png>)
![Cấu hình identifier](</images/5-Workshop/5.5-Trien-khai-Database-voi-Amazon-RDS/5.5.1-Tao-RDS-MySQL-trong-Private-Subnet/rds%203.png>)
![Chọn instance class](</images/5-Workshop/5.5-Trien-khai-Database-voi-Amazon-RDS/5.5.1-Tao-RDS-MySQL-trong-Private-Subnet/rds%204.png>)
![Cấu hình storage](</images/5-Workshop/5.5-Trien-khai-Database-voi-Amazon-RDS/5.5.1-Tao-RDS-MySQL-trong-Private-Subnet/rds%205.png>)
![Cấu hình connectivity](</images/5-Workshop/5.5-Trien-khai-Database-voi-Amazon-RDS/5.5.1-Tao-RDS-MySQL-trong-Private-Subnet/rds%206.png>)
![Cấu hình database](</images/5-Workshop/5.5-Trien-khai-Database-voi-Amazon-RDS/5.5.1-Tao-RDS-MySQL-trong-Private-Subnet/rds%207.png>)
![RDS Available](</images/5-Workshop/5.5-Trien-khai-Database-voi-Amazon-RDS/5.5.1-Tao-RDS-MySQL-trong-Private-Subnet/rds%208.png>)
