---
title: "Week 3 Worklog"
date: 2026-05-01
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

{{% notice warning %}}
 **Note:** The following content records the learning and implementation activities completed during the week and is intended for the personal worklog report.
{{% /notice %}}

### Week 3 Objectives:

- Build separate Linux and Windows VPC environments across two Availability Zones.
- Practice EC2, EBS, AMI, and IAM administration and access instances without relying on public SSH.
- Install a web server and a test database while documenting configuration issues.

### Tasks carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 05/01/2026 | Designed Linux and Windows VPC environments across two AZs with public/private subnets, Internet Gateways, a NAT Gateway, and route tables. | 05/01/2026 | 05/01/2026 | AWS VPC configuration |
| 05/02/2026 | Created Security Groups and launched Linux and Windows EC2 instances.<br>&emsp;Tested EC2 Instance Connect Endpoint or Systems Manager Session Manager. | 05/02/2026 | 05/02/2026 | EC2 connection records |
| 05/03/2026 | Changed the instance type from `t3.micro` to `t3.medium` when required, created an EBS Snapshot, and produced a custom AMI. | 05/03/2026 | 05/03/2026 | EC2 and EBS console records |
| 05/04/2026 – 05/05/2026 | Created and attached an IAM Role; installed Apache, verified the `It works!` page, and configured `/var/www` permissions. | 05/04/2026 | 05/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 05/06/2026 | Installed MariaDB and phpMyAdmin and created the `awsuser` test database and table. | 05/06/2026 | 05/06/2026 | Web server implementation notes |
| 05/07/2026 | Created the `RegionRestrict` IAM Policy, tested region, instance-family, or IP restrictions, and documented routing, permission, and connection errors. | 05/07/2026 | 05/07/2026 | IAM policy and troubleshooting notes |

### Week 3 Achievements:

- Completed multi-AZ Linux and Windows VPC environments.
- Managed the EC2 lifecycle, resized an instance, and created an EBS Snapshot and custom AMI.
- Accessed instances through EC2 Instance Connect Endpoint or Session Manager and attached an appropriate IAM Role.
- Installed Apache, MariaDB, and phpMyAdmin and created the `awsuser` test data.
- Understood the effect of `RegionRestrict` and learned to diagnose route, Security Group, and IAM issues.
