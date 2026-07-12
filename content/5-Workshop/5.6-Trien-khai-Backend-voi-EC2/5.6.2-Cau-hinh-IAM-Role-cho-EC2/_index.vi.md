---
title: "Cấu hình IAM Role cho EC2"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.6.2. </b> "
---

## Các bước chi tiết

1. Vào **IAM → Roles → Create role**, trusted entity `AWS service`, use case `EC2`.
2. Gắn `AmazonSSMManagedInstanceCore` và policy S3 tối thiểu ở mục 5.7.3.
3. Đặt tên `RecruitBoxEC2Role`, tạo role.
4. Vào EC2 → chọn backend → **Actions → Security → Modify IAM role** → chọn role vừa tạo.

![Tạo IAM Role](</images/5-Workshop/5.6-Trien-khai-Backend-voi-EC2/5.6.2-Cau-hinh-IAM-Role-cho-EC2/role%20for%20ec2.png>)
![Gắn role vào EC2](</images/5-Workshop/5.6-Trien-khai-Backend-voi-EC2/5.6.2-Cau-hinh-IAM-Role-cho-EC2/role%20for%20ec2%202.png>)

## Xác minh bảo mật

Trên EC2 chạy `aws sts get-caller-identity`. Kết quả phải là assumed-role `RecruitBoxEC2Role`. Không tạo hoặc lưu IAM access key trên instance.
