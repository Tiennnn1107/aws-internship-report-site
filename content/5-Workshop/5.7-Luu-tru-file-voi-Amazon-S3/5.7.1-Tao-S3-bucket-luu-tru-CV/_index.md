---
title: "Create an S3 Bucket for CV Storage"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.7.1. </b> "
---

### 5.7.1. Create an S3 Bucket for CV Storage

1. Open **S3 → Create bucket**, enter a globally unique name such as `recruitbox-cv-<account-id>`, and select the deployment Region.
2. Keep **Block all public access** enabled. Enable versioning and default SSE-S3 or SSE-KMS encryption.
3. Create a `cv/` prefix and configure lifecycle rules for old versions according to the retention policy.

In **Permissions**, confirm that public access blocking is on. Upload a test file and verify its encryption. Do not use real CVs or personal data in the demonstration environment.

Before deleting the bucket, remove every object and version.

![Nhập tên bucket CV](</images/5-Workshop/5.7-Luu-tru-file-voi-Amazon-S3/5.7.1-Tao-S3-bucket-luu-tru-CV/cv%20storage%201.png>)
![Cấu hình public access và versioning](</images/5-Workshop/5.7-Luu-tru-file-voi-Amazon-S3/5.7.1-Tao-S3-bucket-luu-tru-CV/cv%20storage%202.png>)
![Bucket CV đã tạo](</images/5-Workshop/5.7-Luu-tru-file-voi-Amazon-S3/5.7.1-Tao-S3-bucket-luu-tru-CV/cv%20storage%203.png>)
