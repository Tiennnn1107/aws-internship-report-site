---
title: "Issues Encountered and Resolutions"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.12.2. </b> "
---

### 5.12.2. Issues Encountered and Resolutions

During the RecruitPro deployment on AWS, several issues appeared across the networking, application, database, and storage layers. The following table summarizes their symptoms, causes, and applied resolutions.

| Issue | Cause | Resolution |
|---|---|---|
| The private EC2 instance could not download packages or artifacts | The private subnet had no route through the NAT Gateway, or the NAT Gateway had no Elastic IP | Verify the application subnet route table, add a `0.0.0.0/0` route to the NAT Gateway, and confirm that the gateway is `Available` |
| The backend could not connect to RDS MySQL | The endpoint or credentials were incorrect, or the RDS Security Group did not allow the EC2 source | Use the correct RDS endpoint and port `3306`; allow MySQL/Aurora inbound traffic from the EC2 Security Group and test the connection from EC2 with a MySQL client |
| The application started, but the ALB target remained `unhealthy` | The health-check path or port was incorrect, the application listened only on localhost, or the EC2 Security Group blocked ALB traffic | Configure a health endpoint that returns HTTP `200`, listen on `0.0.0.0:8080`, and allow the application port only from the ALB Security Group |
| Uploading a CV to S3 returned `AccessDenied` | The IAM role lacked object permissions, or the configured bucket name/prefix did not match | Attach the IAM role to EC2, grant the minimum `s3:PutObject`, `s3:GetObject`, and `s3:DeleteObject` permissions for the correct bucket/prefix ARN, and keep access keys out of the source code |
| CloudFront continued to serve outdated content | The object was still cached at an edge location | Create an invalidation for the updated path, review the cache policy, and use versioned names for static assets that change frequently |
| CloudWatch alert emails were not received | The SNS subscription was unconfirmed, or the alarm used the wrong metric or threshold | Confirm the email subscription, verify the SNS topic attached to the alarm, and run a test that moves the alarm from `OK` to `ALARM` |

After each correction, the complete request path was tested again: the user request passed through CloudFront and the ALB, the backend accessed RDS and S3, and CloudWatch collected metrics and logs. Validating one layer at a time made faults easier to isolate without unnecessarily broadening Security Group rules.
