---
title: "Configure Networking with Amazon VPC"
date: 2026-07-10
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

## 5.4. Configure Networking with Amazon VPC

This section builds an isolated network for RecruitBox in `ap-southeast-1`. The design uses public subnets for the ALB and NAT Gateway, private application subnets for the EC2 backend, and isolated database subnets for Amazon RDS. The following steps create the VPC, subnets, gateways, route tables, and an S3 Gateway Endpoint.
