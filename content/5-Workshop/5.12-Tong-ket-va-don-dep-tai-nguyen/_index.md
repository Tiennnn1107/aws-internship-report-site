---
title: "Summary and Resource Cleanup"
date: 2026-07-10
weight: 12
chapter: false
pre: " <b> 5.12. </b> "
---

## 5.12. Summary and Resource Cleanup

## Cost optimization

- Use small EC2 and RDS sizes for the workshop and stop or delete them when not required.
- NAT Gateway and ALB charge by time; consider VPC endpoints, schedules, or serverless/container alternatives for small workloads.
- Configure S3 lifecycle rules and CloudWatch Logs retention, and remove obsolete snapshots and artifacts.
- Create an AWS Budget and Cost Anomaly Detection before deployment.

## Basic security

- Keep EC2 and RDS private and reference security groups instead of broad CIDR ranges.
- Apply least privilege with IAM roles; never commit access keys, database passwords, or tokens.
- Enable S3, RDS, and EBS encryption and use HTTPS with CloudFront, ALB, and ACM.
- Enable suitable RDS backups, CloudTrail, and logs without recording sensitive data.

## Safe cleanup order

1. Preserve required evidence, delete demonstration PII, and stop test workloads.
2. Disable and delete the CloudFront distribution.
3. Delete the ALB, listeners, and target group.
4. Terminate EC2 and remove unused EBS volumes and Elastic IPs.
5. Delete RDS and any unnecessary manual snapshots.
6. Empty all S3 object versions, then delete the buckets.
7. Delete the NAT Gateway, release its Elastic IP, and delete VPC endpoints.
8. Delete custom route tables, subnets, the Internet Gateway, security groups, and the VPC.
9. Delete CloudWatch alarms and log groups, SNS subscriptions and topics, and custom IAM policies and roles.
10. Review **Billing → Bills**, Cost Explorer, and Resource Explorer for remaining billable resources.

Cleanup is complete when no EC2, RDS, NAT Gateway, ALB, CloudFront distribution, Elastic IP, or S3 object continues to generate charges and no abnormal cost appears after billing data updates.
