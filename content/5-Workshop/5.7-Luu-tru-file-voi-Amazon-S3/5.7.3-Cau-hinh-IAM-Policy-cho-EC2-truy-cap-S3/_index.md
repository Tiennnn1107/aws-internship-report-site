---
title: "Configure an IAM Policy for EC2 Access to S3"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.7.3. </b> "
---

### 5.7.3. Configure an IAM Policy for EC2 Access to S3

1. Open **IAM → Policies → Create policy → JSON**.
2. Grant the artifact bucket `s3:GetObject`. Grant the CV bucket `GetObject`, `PutObject`, and `DeleteObject`; grant `ListBucket` only on the bucket ARN.
3. Restrict resources to the required buckets and prefixes, name the policy `RecruitBoxS3Access`, and attach it to `RecruitBoxEC2Role`.

From EC2, confirm that uploads and downloads under `cv/` succeed while access to an unrelated bucket returns `AccessDenied`. Enable CloudTrail data events when object-level auditing is required.

![Create the policy for EC2](</images/5-Workshop/5.7-Luu-tru-file-voi-Amazon-S3/5.7.3-Cau-hinh-IAM-Policy-cho-EC2-truy-cap-S3/policy%20role%20for%20ec2.png>)
