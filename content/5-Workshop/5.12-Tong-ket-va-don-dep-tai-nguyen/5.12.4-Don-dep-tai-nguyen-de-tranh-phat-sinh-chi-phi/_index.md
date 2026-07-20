---
title: "Clean Up Resources to Avoid Additional Charges"
date: 2026-07-10
weight: 4
chapter: false
pre: " <b> 5.12.4. </b> "
---

### 5.12.4. Clean Up Resources to Avoid Additional Charges

The AWS resources are currently retained for deployment, testing, demonstration, and system evaluation. Therefore, the main resources **have not been deleted at the time of writing**. Cleanup will be performed after the workshop and evaluation process have been completed.

#### Cost controls while the system remains available

- Create an AWS Budget and configure alerts when actual or forecast costs exceed the permitted threshold.
- Review **Billing**, **Cost Explorer**, and cost alert emails regularly.
- Run testing resources only for the time required.
- Stop EC2 instances outside testing periods when doing so does not affect demonstrations or evaluation.
- Use EC2 and RDS sizes appropriate for a workshop workload.
- Configure CloudWatch Logs retention to prevent unnecessary long-term log storage.
- Avoid creating additional NAT Gateways, Elastic IP addresses, load balancers, snapshots, or temporary resources unless required.

> **Note:** Stopping an EC2 instance does not stop every associated charge. EBS volumes, Elastic IP addresses, NAT Gateways, Application Load Balancers, RDS, and related services may continue to incur charges.

#### Cleanup plan after project completion

After the system is no longer required for demonstration or evaluation, resources will be removed in the following order to reduce dependency errors:

1. Disable and delete the CloudFront distribution.
2. Delete the Application Load Balancer, listeners, and target groups.
3. Terminate the EC2 instances, then identify and delete unused EBS volumes.
4. Delete the RDS database. Create a final snapshot only when its data must be retained, and remove unneeded manual snapshots.
5. Remove S3 objects, object versions, and delete markers before deleting buckets that are no longer required.
6. Delete the NAT Gateway, release its Elastic IP address, and delete VPC Endpoints.
7. Delete custom route tables, subnets, the Internet Gateway, Security Groups, and finally the VPC.
8. Delete workshop-specific CloudWatch alarms and log groups, SNS topics and subscriptions, and custom IAM roles and policies.
9. Review **Billing**, **Cost Explorer**, and **Resource Explorer** to confirm that no unexpected resources remain.

#### Completion criteria

Cleanup is complete when no unnecessary EC2 instances, RDS databases, NAT Gateways, Application Load Balancers, CloudFront distributions, Elastic IP addresses, EBS volumes, or S3 objects remain. Because cost data may be delayed, the account will continue to be monitored for 24–48 hours after cleanup.
