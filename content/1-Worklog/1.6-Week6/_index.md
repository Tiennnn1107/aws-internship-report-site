---
title: "Week 6 Worklog"
date: 2026-05-22
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

{{% notice warning %}}
 **Note:** The following content records the learning and implementation activities completed during the week and is intended for the personal worklog report.
{{% /notice %}}

### Week 6 Objectives:

- Analyze the RecruitBox/RecruitPro codebase, features, and packaging model.
- Choose an AWS architecture that matches the project scope and budget.
- Complete the initial architecture diagram and clearly separate deployed scope from deferred ideas.

### Tasks carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 05/22/2026 | Reviewed the RecruitBox/RecruitPro source and identified Spring Boot, Thymeleaf, MySQL, and JAR packaging. | 05/22/2026 | 05/22/2026 | RecruitBox/RecruitPro source code |
| 05/23/2026 | Mapped registration, login, user management, job browsing, profile updates, CV uploads, and recruitment data management. | 05/23/2026 | 05/23/2026 | RecruitBox/RecruitPro source code |
| 05/24/2026 | Compared Fargate and EC2 for fit, operational control, and cost, then selected EC2 for the backend. | 05/24/2026 | 05/24/2026 | <https://aws.amazon.com/ec2/pricing/on-demand/> |
| 05/25/2026 | Designed the User → CloudFront or ALB → EC2 Spring Boot → RDS MySQL flow, with S3 for CV storage. | 05/25/2026 | 05/25/2026 | Project architecture diagram |
| 05/26/2026 | Identified VPC, IAM, Systems Manager, EC2, RDS, S3, ALB, CloudFront, CloudWatch, and SNS as deployment services. | 05/26/2026 | 05/26/2026 | Architecture design notes |
| 05/27/2026 – 05/28/2026 | Refined the diagram and prepared an initial cost estimate.<br>&emsp;Removed or deferred Cognito, Bedrock, SQS, the worker daemon, and ElastiCache. | 05/27/2026 | 05/28/2026 | <https://aws.amazon.com/vpc/pricing/>; <https://aws.amazon.com/rds/mysql/pricing/> |

### Week 6 Achievements:

- Understood the Spring Boot, Thymeleaf, and MySQL application structure and JAR deployment model.
- Mapped the core features and data that needed to move to AWS.
- Selected EC2 for the backend after comparing it with Fargate.
- Completed an initial ALB/CloudFront, EC2, RDS, and S3 architecture with a preliminary cost estimate.
- Documented Cognito, Bedrock, SQS, the worker daemon, and ElastiCache as removed or deferred rather than implemented.
