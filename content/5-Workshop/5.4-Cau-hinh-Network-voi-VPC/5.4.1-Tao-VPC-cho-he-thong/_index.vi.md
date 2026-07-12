---
title: "Tạo VPC cho hệ thống"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.4.1. </b> "
---

## Mục tiêu

Tạo VPC riêng cho RecruitBox tại Region **Asia Pacific (Singapore) – ap-southeast-1**.

## Các bước chi tiết

1. Mở **VPC Console → Your VPCs → Create VPC**.
2. Chọn **VPC only**, nhập `RecruitVPC`, IPv4 CIDR `10.0.0.0/16`, tenancy `Default`.
3. Chọn **Create VPC** và chờ trạng thái `Available`.

![Nhập thông tin VPC](/images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.1-Tao-VPC-cho-he-thong/vpc1.png)

4. Mở VPC vừa tạo, bật **DNS resolution** và **DNS hostnames** trong **Actions → Edit VPC settings**.

![Kiểm tra VPC đã tạo](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.1-Tao-VPC-cho-he-thong/vpc2.png>)

## Xác minh

VPC phải có CIDR `10.0.0.0/16`, trạng thái `Available` và cả hai thuộc tính DNS được bật.
