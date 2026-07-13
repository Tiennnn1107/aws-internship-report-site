---
title: "Week 9 Worklog"
date: 2026-06-12
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

{{% notice warning %}}
 **Note:** The following content records the learning and implementation activities completed during the week and is intended for the personal worklog report.
{{% /notice %}}

### Week 9 Objectives:

- Set up private S3 storage for CVs, deployment artifacts, and optional database backups.
- Grant least-privilege S3 access to the EC2 Role and deploy the JAR from S3.
- Integrate CV uploads with the AWS SDK for Java and resolve access errors.

### Tasks carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 06/12/2026 | Created `recruitpro-cv-storage-tien` and `recruitpro-deploy-artifacts-tien`, and recorded `recruitpro-db-backup-tien` for database backups. | 06/12/2026 | 06/12/2026 | S3 bucket records |
| 06/13/2026 | Enabled Block Public Access and encryption and confirmed that the CV bucket was not publicly accessible. | 06/13/2026 | 06/13/2026 | S3 security configuration |
| 06/14/2026 | Created a least-privilege IAM Policy with `s3:ListBucket`, `s3:GetObject`, `s3:PutObject`, and `s3:DeleteObject`, then attached it to the EC2 Role. | 06/14/2026 | 06/14/2026 | IAM policy records |
| 06/15/2026 | Uploaded the JAR to the artifact bucket and had EC2 download it from S3 before redeploying the service. | 06/15/2026 | 06/15/2026 | S3 and EC2 deployment logs |
| 06/16/2026 – 06/17/2026 | Configured Spring Boot with the AWS SDK for Java to upload CVs under `cv/` and provided a presigned URL or file-view API. | 06/16/2026 | 06/17/2026 | RecruitPro source and application logs |
| 06/18/2026 | Resolved HTTP 403 `HeadObject` and `AccessDenied` errors and verified that the CV object appeared in S3. | 06/18/2026 | 06/18/2026 | S3 object and error verification |

### Week 9 Achievements:

- Created the planned CV, deployment-artifact, and database-backup buckets.
- Kept the CV bucket private with Block Public Access and encryption.
- Applied least-privilege S3 permissions to the EC2 Role and deployed the JAR from the artifact bucket.
- Uploaded CVs under `cv/` and provided time-limited access through a presigned URL or API.
- Resolved `HeadObject` and `AccessDenied` issues by checking resource ARNs, actions, and the attached IAM Role.
