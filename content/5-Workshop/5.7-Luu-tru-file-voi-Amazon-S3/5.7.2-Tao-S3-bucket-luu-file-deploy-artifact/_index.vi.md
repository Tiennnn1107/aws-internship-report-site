---
title: "Tạo S3 bucket lưu file deploy artifact"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.7.2. </b> "
---

## Các bước chi tiết

1. Tạo bucket `recruitbox-artifacts-<account-id>` cùng Region.
2. Bật Block Public Access, Versioning và default encryption.
3. Upload file JAR đã build vào key `releases/recruitbox-<version>.jar` thay vì ghi đè `latest.jar`.

![Tạo artifact bucket](</images/5-Workshop/5.7-Luu-tru-file-voi-Amazon-S3/5.7.2-Tao-S3-bucket-luu-file-deploy-artifact/artifact%20s3.png>)
![Cấu hình bucket](</images/5-Workshop/5.7-Luu-tru-file-voi-Amazon-S3/5.7.2-Tao-S3-bucket-luu-file-deploy-artifact/artifact%20s3%202.png>)
![Upload artifact](</images/5-Workshop/5.7-Luu-tru-file-voi-Amazon-S3/5.7.2-Tao-S3-bucket-luu-file-deploy-artifact/artifact%20s3%203.png>)

## Xác minh

Chạy `aws s3 cp s3://<artifact-bucket>/releases/<file>.jar /tmp/app.jar` từ EC2 và so sánh SHA-256 với file build.

## Tối ưu chi phí

Đặt lifecycle xóa artifact cũ sau thời gian phù hợp; giữ lại các phiên bản đang chạy và phiên bản rollback gần nhất.
