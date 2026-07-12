---
title: "Tạo S3 bucket lưu trữ CV"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.7.1. </b> "
---

## Các bước chi tiết

1. Mở **S3 → Create bucket**, nhập tên duy nhất như `recruitbox-cv-<account-id>` và chọn cùng Region.
2. Giữ **Block all public access**; bật Bucket Versioning và default encryption SSE-S3 hoặc SSE-KMS.
3. Tạo bucket, sau đó tạo prefix `cv/`; cấu hình lifecycle chuyển/xóa phiên bản cũ theo chính sách lưu trữ.

![Nhập tên bucket CV](</images/5-Workshop/5.7-Luu-tru-file-voi-Amazon-S3/5.7.1-Tao-S3-bucket-luu-tru-CV/cv%20storage%201.png>)
![Cấu hình public access và versioning](</images/5-Workshop/5.7-Luu-tru-file-voi-Amazon-S3/5.7.1-Tao-S3-bucket-luu-tru-CV/cv%20storage%202.png>)
![Bucket CV đã tạo](</images/5-Workshop/5.7-Luu-tru-file-voi-Amazon-S3/5.7.1-Tao-S3-bucket-luu-tru-CV/cv%20storage%203.png>)

## Xác minh và bảo mật

Tab Permissions phải hiển thị `Block all public access: On`; upload thử một file và kiểm tra encryption. Không đưa CV thật có dữ liệu cá nhân vào môi trường demo.

## Clean-up

Xóa toàn bộ object và version trước khi xóa bucket.
