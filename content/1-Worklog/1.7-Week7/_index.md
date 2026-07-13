---
title: "Week 7 Worklog"
date: 2026-05-29
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

{{% notice warning %}}
 **Note:** The following content records the learning and implementation activities completed during the week and is intended for the personal worklog report.
{{% /notice %}}

### Week 7 Objectives:

- Build `RecruitVPC` in `ap-southeast-1` with a multi-AZ subnet design.
- Provide Internet paths for the public and private application tiers while keeping the database tier private.
- Implement the ALB → EC2 → RDS Security Group flow.

### Tasks carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 05/29/2026 | Created `RecruitVPC` with CIDR `10.0.0.0/16` in `ap-southeast-1` and selected two Availability Zones. | 05/29/2026 | 05/29/2026 | AWS VPC configuration |
| 05/30/2026 | Created public subnets `10.0.1.0/24` and `10.0.2.0/24`, plus private app subnets `10.0.11.0/24` and `10.0.12.0/24`. | 05/30/2026 | 05/30/2026 | RecruitVPC subnet records |
| 05/31/2026 | Created private DB subnets `10.0.21.0/24` and `10.0.22.0/24` and verified that CIDR ranges did not overlap. | 05/31/2026 | 05/31/2026 | RecruitVPC subnet records |
| 06/01/2026 | Created an Internet Gateway and a NAT Gateway in a public subnet and associated an Elastic IP. | 06/01/2026 | 06/01/2026 | AWS VPC configuration |
| 06/02/2026 | Configured the public route table, the private app route through NAT, and the private DB route table without a default Internet route. | 06/02/2026 | 06/02/2026 | Route table verification |
| 06/03/2026 – 06/04/2026 | Created Security Groups for the ALB, EC2 backend, and RDS and verified routes and traffic flow between tiers. | 06/03/2026 | 06/04/2026 | Security Group and connectivity checks |

### Week 7 Achievements:

- Completed `RecruitVPC` with six subnets distributed across two AZs.
- Configured the Internet Gateway, NAT Gateway, Elastic IP, and three route-table groups for their intended roles.
- Built a Security Group chain that limits ALB-to-EC2 and EC2-to-RDS traffic.
- Explained that private subnets reduce direct exposure for EC2 and RDS and that RDS does not require an Internet route.
