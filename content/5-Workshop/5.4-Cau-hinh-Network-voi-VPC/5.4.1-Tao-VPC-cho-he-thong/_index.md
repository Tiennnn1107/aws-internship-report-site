---
title: "Create the System VPC"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.4.1. </b> "
---

### 5.4.1. Create the System VPC

## Goal

Create a dedicated VPC for RecruitBox in **Asia Pacific (Singapore) — `ap-southeast-1`**.

## Steps

1. Open **VPC Console → Your VPCs → Create VPC**.
2. Select **VPC only**, enter `RecruitVPC`, set IPv4 CIDR to `10.0.0.0/16`, and keep tenancy as `Default`.
3. Select **Create VPC** and wait until its state is `Available`.
4. Open the new VPC and enable both **DNS resolution** and **DNS hostnames** from **Actions → Edit VPC settings**.

## Validation

Confirm that the VPC uses CIDR `10.0.0.0/16`, is `Available`, and has both DNS options enabled.

![Nhập thông tin VPC](/images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.1-Tao-VPC-cho-he-thong/vpc1.png)
![Kiểm tra VPC đã tạo](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.1-Tao-VPC-cho-he-thong/vpc2.png>)
