---
title: "Configure the IAM Role for EC2"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.6.2. </b> "
---

### 5.6.2. Configure the IAM Role for EC2

1. Open **IAM → Roles → Create role**, choose trusted entity `AWS service`, and select the `EC2` use case.
2. Attach `AmazonSSMManagedInstanceCore` and the minimum S3 policy described in section 5.7.3.
3. Name the role `RecruitBoxEC2Role` and create it.
4. Open the backend instance and choose **Actions → Security → Modify IAM role**, then attach the new role.

Run the following command on EC2:

```bash
aws sts get-caller-identity
```

The result must show an assumed role for `RecruitBoxEC2Role`. Never create or store IAM access keys on the instance.

![Tạo IAM Role](</images/5-Workshop/5.6-Trien-khai-Backend-voi-EC2/5.6.2-Cau-hinh-IAM-Role-cho-EC2/role%20for%20ec2.png>)
![Gắn role vào EC2](</images/5-Workshop/5.6-Trien-khai-Backend-voi-EC2/5.6.2-Cau-hinh-IAM-Role-cho-EC2/role%20for%20ec2%202.png>)
