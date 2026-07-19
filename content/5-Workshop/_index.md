---
title: "Workshop"
date: 2026-07-10
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# 5. Workshop

## Workshop outcomes

Deploy the Spring Boot RecruitBox application end to end on AWS using the flow CloudFront → ALB → EC2 → RDS, store CVs and deployment artifacts in S3, and monitor the system with CloudWatch and SNS.

## How to complete the workshop

Follow sections 5.1 through 5.12 in order. Each section covers objectives, prerequisites, AWS Console or CLI actions, expected results, testing, and cleanup.

## Completion criteria

- Explain the architecture, request flow, and reason for each AWS service.
- Run EC2 and RDS in private subnets; users access the application only through CloudFront and the ALB.
- Centralize application logs and send important metric alarms through SNS email.
- Test functional flows, failures, and basic access controls.
- Document estimated costs, least-privilege rules, and resource cleanup.

{{% notice warning %}}
NAT Gateway, ALB, RDS, EC2, and CloudFront can incur charges. Complete section 5.12 immediately after the workshop.
{{% /notice %}}
