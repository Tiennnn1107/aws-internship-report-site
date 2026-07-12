---
title: "Create an S3 Gateway Endpoint"
date: 2026-07-12
weight: 6
chapter: false
pre: " <b> 5.4.6. </b> "
---

## Goal

Allow private EC2 instances to reach Amazon S3 over the AWS network without using a NAT or Internet Gateway. S3 Gateway Endpoints have no hourly charge.

## Prerequisites

- `RecruitVPC` and its private application subnets exist.
- `Recruit-private-app-rt` is associated with both private application subnets.
- Your identity can create and modify VPC endpoints.

## Detailed steps

1. Open **Amazon VPC Console** in the deployment Region.
2. Select **Endpoints → Create endpoint**.
3. Enter `s3-gwe`; for **Service category**, select **AWS services**.
4. Search for `s3`, then select `com.amazonaws.ap-southeast-1.s3` with **Type = Gateway**.
5. Select `RecruitVPC`.
6. Select `Recruit-private-app-rt`; do not select the public or database route table.
7. Keep **Full access** for the initial test and choose **Create endpoint**.

## Validation

The endpoint must be `Available`. The application route table must contain an S3 prefix-list route (`pl-...`) targeting the endpoint (`vpce-...`). From EC2, run:

```bash
aws s3 ls
aws s3 ls s3://<cv-bucket-name>
```

## Security, cost, and clean-up

Replace Full access with a least-privilege endpoint policy after testing. IAM and bucket policies still apply. To remove the endpoint, use **VPC → Endpoints → s3-gwe → Delete VPC endpoints**.
