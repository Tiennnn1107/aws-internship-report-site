---
title: "Configure Route Tables"
date: 2026-07-10
weight: 5
chapter: false
pre: " <b> 5.4.5. </b> "
---

### 5.4.5. Configure Route Tables

1. Create `Recruit-public-rt`, add `0.0.0.0/0 → Internet Gateway`, and associate both public subnets.
2. Create `Recruit-private-app-rt`, add `0.0.0.0/0 → NAT Gateway`, and associate both private application subnets.
3. Create `Recruit-private-db-rt`, keep only the `local` route, and associate both private database subnets.

## Validation

- Private EC2 instances can download packages through the NAT Gateway but cannot receive direct Internet connections.
- Database subnets have no route to an Internet Gateway or NAT Gateway.

![Tạo route table](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.5-Cau-hinh-Route-Table/route%20table%201.png>)
![Chọn VPC](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.5-Cau-hinh-Route-Table/route%20table%202.png>)
![Mở tab Routes](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.5-Cau-hinh-Route-Table/route%20table%203.png>)
![Thêm default route](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.5-Cau-hinh-Route-Table/route%20table%204.png>)
![Chọn Internet Gateway](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.5-Cau-hinh-Route-Table/route%20table%205.png>)
![Associate subnet](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.5-Cau-hinh-Route-Table/route%20table%206.png>)
![Chọn private subnet](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.5-Cau-hinh-Route-Table/route%20table%207.png>)
![Kiểm tra route table](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.5-Cau-hinh-Route-Table/route%20table%208.png>)
