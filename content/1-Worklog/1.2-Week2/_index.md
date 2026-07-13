---
title: "Week 2 Worklog"
date: 2026-04-24
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

{{% notice warning %}}
 **Note:** The following content records the learning and implementation activities completed during the week and is intended for the personal worklog report.
{{% /notice %}}

### Week 2 Objectives:

- Understand Amazon VPC components and routing behavior.
- Build a demo VPC with public and private subnets, an Internet Gateway, and route tables.
- Differentiate Security Groups from Network ACLs and validate EC2 connectivity.

### Tasks carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 04/24/2026 | Studied Amazon VPC, CIDR planning, and the difference between public and private subnets. | 04/24/2026 | 04/24/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 04/25/2026 | Created `VPC-DEMO` with CIDR `10.10.0.0/16`, then created one public and one private subnet. | 04/25/2026 | 04/25/2026 | AWS Management Console |
| 04/26/2026 – 04/27/2026 | Created and attached an Internet Gateway and configured a public route table with a default Internet route. | 04/26/2026 | 04/27/2026 | AWS VPC configuration |
| 04/28/2026 | Compared stateful Security Group rules with stateless Network ACL rules and reviewed inbound and outbound traffic. | 04/28/2026 | 04/28/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 04/29/2026 – 04/30/2026 | Launched EC2 in `VPC-DEMO` and checked routes, subnet placement, public IP assignment, and Internet access. | 04/29/2026 | 04/30/2026 | EC2 and VPC verification results |

### Week 2 Achievements:

- Built `VPC-DEMO` and divided its address space into public and private subnets.
- Configured an Internet Gateway and a route table for the public subnet.
- Explained the differences among public subnets, private subnets, Security Groups, and Network ACLs.
- Validated the network path used by an EC2 instance in the VPC.
