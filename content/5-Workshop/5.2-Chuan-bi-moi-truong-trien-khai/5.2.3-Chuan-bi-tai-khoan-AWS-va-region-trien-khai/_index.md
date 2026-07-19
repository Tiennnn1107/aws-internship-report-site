---
title: "Prepare the AWS Account and Deployment Region"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.2.3. </b> "
---

### 5.2.3. Prepare the AWS Account and Deployment Region

Use an AWS account with permission to create the VPC, EC2, RDS, S3, Elastic Load Balancing, CloudFront, CloudWatch, SNS, and IAM resources required by the workshop.

1. Sign in to the AWS Management Console with an administrative identity prepared for the workshop. Avoid using the root user for daily deployment tasks.
2. Enable multi-factor authentication and configure a billing budget or cost alert before provisioning resources.
3. Select one AWS Region and use it consistently for regional services. This workshop uses **Asia Pacific (Singapore) — `ap-southeast-1`**.
4. Verify the selected Region in the upper-right corner of the AWS Management Console before creating any resource.
5. Record the Region, account ID, and resource naming convention so later steps use consistent values.

CloudFront and IAM are global services, while resources such as VPC, EC2, RDS, ALB, and most S3 configuration are created or managed with Region-specific context.

![user region](/images/5-Workshop/5.2-Chuan-bi-moi-truong-trien-khai/5.2.3-Chuan-bi-tai-khoan-AWS-va-region-trien-khai/user%20region.png)
