---
title: "Cấu hình Route Table"
date: 2026-07-10
weight: 5
chapter: false
pre: " <b> 5.4.5. </b> "
---

## Các bước chi tiết

1. Tạo `Recruit-public-rt`, thêm route `0.0.0.0/0 → Internet Gateway`, rồi associate hai public subnet.
2. Tạo `Recruit-private-app-rt`, thêm route `0.0.0.0/0 → NAT Gateway`, associate hai private app subnet.
3. Tạo `Recruit-private-db-rt`, chỉ giữ route `local`, associate hai private DB subnet.

![Tạo route table](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.5-Cau-hinh-Route-Table/route%20table%201.png>)
![Chọn VPC](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.5-Cau-hinh-Route-Table/route%20table%202.png>)
![Mở tab Routes](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.5-Cau-hinh-Route-Table/route%20table%203.png>)
![Thêm default route](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.5-Cau-hinh-Route-Table/route%20table%204.png>)
![Chọn Internet Gateway](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.5-Cau-hinh-Route-Table/route%20table%205.png>)
![Associate subnet](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.5-Cau-hinh-Route-Table/route%20table%206.png>)
![Chọn private subnet](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.5-Cau-hinh-Route-Table/route%20table%207.png>)
![Kiểm tra route table](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.5-Cau-hinh-Route-Table/route%20table%208.png>)

## Xác minh

- EC2 private có thể tải package qua NAT nhưng không nhận kết nối trực tiếp từ Internet.
- DB subnet không có route tới Internet Gateway hoặc NAT Gateway.
