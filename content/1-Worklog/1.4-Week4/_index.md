---
title: "Week 4 Worklog"
date: 2026-05-08
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

{{% notice warning %}}
 **Note:** The following content records the learning and implementation activities completed during the week and is intended for the personal worklog report.
{{% /notice %}}

### Week 4 Objectives:

- Host a multi-file static website on Amazon S3.
- Practice Versioning, Cross-Region Replication, and object access management.
- Create a CloudFormation stack and study AWS Backup and SNS notifications.

### Tasks carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 05/08/2026 | Created `aws-first-cloud-journey-123456` in `ap-southeast-1` and uploaded `index.html`, `error.html`, and static assets. | 05/08/2026 | 05/08/2026 | AWS S3 console records |
| 05/09/2026 | Enabled Static Website Hosting, adjusted Block Public Access, reviewed Object Ownership and ACLs, and made the required objects public for testing. | 05/09/2026 | 05/09/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 05/10/2026 | Tested the website endpoint, investigated HTTP 403, validated `index.html` and `error.html`, and calculated total object size. | 05/10/2026 | 05/10/2026 | S3 website verification results |
| 05/11/2026 | Enabled S3 Versioning and configured Cross-Region Replication from `ap-southeast-1` to `us-east-1`. | 05/11/2026 | 05/11/2026 | S3 replication configuration |
| 05/12/2026 | Stored a CloudFormation template or artifact in S3 and created a CloudFormation stack. | 05/12/2026 | 05/12/2026 | CloudFormation stack events |
| 05/13/2026 – 05/14/2026 | Studied Backup vaults, Backup plans, and Backup rules; configured an SNS notification and confirmed the email subscription when prompted. | 05/13/2026 | 05/14/2026 | AWS Backup and SNS console records |

### Week 4 Achievements:

- Published and validated a multi-file static website on S3.
- Understood Block Public Access, Object Ownership, ACL behavior, and HTTP 403 troubleshooting.
- Enabled Versioning, reviewed object size, and configured Cross-Region Replication.
- Created a CloudFormation stack from a template or artifact stored in S3.
- Understood the workflow for Backup vaults, Backup plans, Backup rules, and SNS notifications.
