---
title: "Cấu hình IAM Policy cho EC2 truy cập S3"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.7.3. </b> "
---

## Các bước chi tiết

1. Vào **IAM → Policies → Create policy → JSON**.
2. Cho artifact bucket quyền `s3:GetObject`; CV bucket quyền `GetObject`, `PutObject`, `DeleteObject`; `ListBucket` chỉ trên ARN bucket.
3. Giới hạn Resource đúng bucket/prefix, đặt tên `RecruitBoxS3Access`, rồi gắn vào `RecruitBoxEC2Role`.

![Tạo policy cho EC2](</images/5-Workshop/5.7-Luu-tru-file-voi-Amazon-S3/5.7.3-Cau-hinh-IAM-Policy-cho-EC2-truy-cap-S3/policy%20role%20for%20ec2.png>)

## Kiểm thử

Từ EC2, upload/download trong `cv/` phải thành công; thử truy cập bucket ngoài danh sách phải nhận `AccessDenied`. Dùng CloudTrail Data Events nếu cần audit thao tác object.
