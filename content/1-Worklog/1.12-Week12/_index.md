---
title: "Week 12 Worklog"
date: 2026-07-03
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

{{% notice warning %}}
 **Note:** The following content records the learning and implementation activities completed during the week and is intended for the personal worklog report.
{{% /notice %}}

### Week 12 Objectives:

- Test RecruitPro end to end across application and AWS infrastructure layers.
- Resolve remaining issues and complete the bilingual Proposal, Workshop, and Worklog.
- Summarize the architecture, risks, cost, future direction, and cleanup activities.

### Tasks carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 07/03/2026 – 07/04/2026 | Tested registration, login, candidate/recruiter/admin authorization, job listing, profile updates, and CV uploads. | 07/03/2026 | 07/04/2026 | RecruitPro test results |
| 07/05/2026 | Cross-checked RDS data, S3 CV objects, and application access through ALB and CloudFront. | 07/05/2026 | 07/05/2026 | RDS, S3, ALB, and CloudFront checks |
| 07/06/2026 | Resolved Base64 JWT-secret handling, CloudFront CORS, S3 IAM `AccessDenied`, RDS connection, CloudFront 403, and systemd issues without recording secrets. | 07/06/2026 | 07/06/2026 | Application and infrastructure logs |
| 07/07/2026 | Finalized and numbered the architecture flow and captured screenshots of deployed AWS services. | 07/07/2026 | 07/07/2026 | Architecture diagram and deployment screenshots |
| 07/08/2026 – 07/09/2026 | Completed the bilingual RecruitBox Proposal, Workshop, and Worklog and summarized VPC, EC2, RDS, S3, IAM, ALB, CloudFront, CloudWatch, SNS, and Systems Manager. | 07/08/2026 | 07/09/2026 | Report content in the repository |
| 07/10/2026 | Documented risks, cost, and future work, clearly marking Route 53/ACM, Auto Scaling, CI/CD, Cognito, and the CV-processing pipeline as not implemented.<br>&emsp;Removed unneeded test resources to avoid charges. | 07/10/2026 | 07/10/2026 | Cost table and cleanup checklist |

### Week 12 Achievements:

- Completed functional, authorization, RDS, S3, ALB, and CloudFront testing.
- Resolved JWT, CORS, IAM, RDS, CloudFront, and systemd issues without exposing sensitive data.
- Completed the architecture diagram and bilingual Proposal, Workshop, and Worklog.
- Accurately summarized the deployed services: VPC, EC2, RDS, S3, IAM, ALB, CloudFront, CloudWatch, SNS, and Systems Manager.
- Marked Route 53/ACM, Auto Scaling, CI/CD, Cognito, and the CV-processing pipeline as future work that was not implemented.
- Cleaned up unneeded test resources to limit ongoing cost.
