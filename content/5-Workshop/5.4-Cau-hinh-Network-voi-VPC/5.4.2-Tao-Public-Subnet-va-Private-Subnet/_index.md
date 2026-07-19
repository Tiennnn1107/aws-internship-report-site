---
title: "Create Public and Private Subnets"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.4.2. </b> "
---

### 5.4.2. Create Public and Private Subnets

1. Open **VPC → Subnets → Create subnet** and select `RecruitVPC`.
2. Create six non-overlapping subnets across two Availability Zones:

| Name | AZ | CIDR | Role |
|---|---|---|---|
| `public-alb-1a` | 1a | `10.0.1.0/24` | ALB and NAT |
| `public-alb-1b` | 1b | `10.0.2.0/24` | ALB and NAT |
| `private-app-1a` | 1a | `10.0.11.0/24` | EC2 backend |
| `private-app-1b` | 1b | `10.0.12.0/24` | EC2 backend |
| `private-db-1a` | 1a | `10.0.21.0/24` | Amazon RDS |
| `private-db-1b` | 1b | `10.0.22.0/24` | Amazon RDS |

3. Enable **Auto-assign public IPv4 address** only for the two public subnets.

Verify that all six subnets belong to the correct VPC, span two AZs, and have no overlapping CIDR ranges.

![Tạo public subnet đầu tiên](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.2-Tao-Public-Subnet-va-Private-Subnet/public%20subnet%201.png>)
![Danh sách subnet](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.2-Tao-Public-Subnet-va-Private-Subnet/tuong%20tu%20tao%20them%206%20subnet.png>)
