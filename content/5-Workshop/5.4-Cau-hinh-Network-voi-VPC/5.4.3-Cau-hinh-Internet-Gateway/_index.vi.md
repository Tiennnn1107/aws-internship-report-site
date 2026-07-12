---
title: "Cấu hình Internet Gateway"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.4.3. </b> "
---

## Các bước chi tiết

1. Vào **VPC → Internet gateways → Create internet gateway**.
2. Nhập tên `Recruit-igw`, chọn **Create**.

![Tạo Internet Gateway](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.3-Cau-hinh-Internet-Gateway/internet%20gateway.png>)

3. Chọn gateway → **Actions → Attach to a VPC**.

![Chọn thao tác attach](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.3-Cau-hinh-Internet-Gateway/igw%20attach%20vpc.png>)

4. Chọn `RecruitVPC` và xác nhận.

![Attach vào RecruitVPC](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.3-Cau-hinh-Internet-Gateway/igw%20attach%20vpc%202.png>)

## Xác minh

Trạng thái Internet Gateway phải là `Attached`, cột VPC ID trỏ đến `RecruitVPC`.
