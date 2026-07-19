---
title: "Triển khai Backend với EC2"
date: 2026-07-10
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

## 5.6. Triển khai Backend với EC2

Phần này triển khai Spring Boot backend trên EC2 trong private subnet. Nội dung gồm cấu hình network theo least privilege, gắn IAM Role, cài Java, tải JAR artifact từ S3 và chạy ứng dụng dưới dạng `systemd` service.
