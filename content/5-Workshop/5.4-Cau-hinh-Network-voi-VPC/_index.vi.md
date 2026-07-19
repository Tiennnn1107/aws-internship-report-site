---
title: "Cấu hình Network với VPC"
date: 2026-07-10
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

## 5.4. Cấu hình Network với VPC

Phần này xây dựng mạng cô lập cho RecruitBox tại `ap-southeast-1`. Kiến trúc sử dụng public subnet cho ALB và NAT Gateway, private application subnet cho EC2 backend và private database subnet cho Amazon RDS. Các bước tiếp theo tạo VPC, subnet, gateway, route table và S3 Gateway Endpoint.
