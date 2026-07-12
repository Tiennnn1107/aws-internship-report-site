---
title: "Tạo Public Subnet và Private Subnet"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.4.2. </b> "
---

## Các bước chi tiết

1. Vào **VPC → Subnets → Create subnet**, chọn `RecruitVPC`.
2. Tạo subnet đầu tiên, chọn AZ `ap-southeast-1a`, nhập tên và CIDR không trùng nhau.

![Tạo public subnet đầu tiên](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.2-Tao-Public-Subnet-va-Private-Subnet/public%20subnet%201.png>)

3. Tạo đủ sáu subnet theo bảng:

| Tên | AZ | CIDR | Vai trò |
|---|---|---|---|
| `public-alb-1a` | 1a | `10.0.1.0/24` | ALB/NAT |
| `public-alb-1b` | 1b | `10.0.2.0/24` | ALB/NAT |
| `private-app-1a` | 1a | `10.0.11.0/24` | EC2 backend |
| `private-app-1b` | 1b | `10.0.12.0/24` | EC2 backend |
| `private-db-1a` | 1a | `10.0.21.0/24` | RDS |
| `private-db-1b` | 1b | `10.0.22.0/24` | RDS |

![Danh sách subnet](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.2-Tao-Public-Subnet-va-Private-Subnet/tuong%20tu%20tao%20them%206%20subnet.png>)

4. Với hai public subnet, bật **Auto-assign public IPv4 address**. Không bật tùy chọn này cho private subnet.

## Xác minh

Có sáu subnet thuộc đúng VPC, phân bố trên hai AZ và không có CIDR chồng lấn.
