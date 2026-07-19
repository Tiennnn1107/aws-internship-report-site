---
title: "Create an S3 Bucket for Deployment Artifacts"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.7.2. </b> "
---

### 5.7.2. Create an S3 Bucket for Deployment Artifacts

1. Create `recruitbox-artifacts-<account-id>` in the deployment Region.
2. Enable Block Public Access, versioning, and default encryption.
3. Upload versioned JAR files under keys such as `releases/recruitbox-<version>.jar` instead of overwriting `latest.jar`.

From EC2, download an artifact and compare its SHA-256 checksum with the local build:

```bash
aws s3 cp s3://<artifact-bucket>/releases/<file>.jar /tmp/app.jar
sha256sum /tmp/app.jar
```

Use a lifecycle rule to remove obsolete artifacts while retaining the current release and the most recent rollback version.

![Tạo artifact bucket](</images/5-Workshop/5.7-Luu-tru-file-voi-Amazon-S3/5.7.2-Tao-S3-bucket-luu-file-deploy-artifact/artifact%20s3.png>)
![Cấu hình bucket](</images/5-Workshop/5.7-Luu-tru-file-voi-Amazon-S3/5.7.2-Tao-S3-bucket-luu-file-deploy-artifact/artifact%20s3%202.png>)
![Upload artifact](</images/5-Workshop/5.7-Luu-tru-file-voi-Amazon-S3/5.7.2-Tao-S3-bucket-luu-file-deploy-artifact/artifact%20s3%203.png>)
