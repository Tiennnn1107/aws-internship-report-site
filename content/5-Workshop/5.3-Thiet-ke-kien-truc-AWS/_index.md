---
title: "Design the AWS Architecture"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

## 5.3. Design the AWS Architecture

## Overall architecture

```mermaid
flowchart LR
  U[User] --> CF[CloudFront]
  CF --> ALB[Application Load Balancer]
  ALB --> EC2[EC2 Spring Boot\nPrivate App Subnet]
  EC2 --> RDS[(RDS MySQL\nPrivate DB Subnet)]
  EC2 --> CV[(S3 CV Storage)]
  S3A[(S3 Artifacts)] --> EC2
  CW[CloudWatch] -. Logs and metrics .-> EC2
  CW -. Metrics .-> ALB
  CW -. Metrics .-> RDS
  CW --> SNS[SNS Email]
```

## Services and rationale

| Service | Role | Rationale |
|---|---|---|
| VPC | Network isolation | Separates public, application, and database tiers |
| ALB | HTTP entry point | Provides health checks, load balancing, and EC2 scaling support |
| EC2 | Spring Boot runtime | Supports the existing JAR and operating-system control |
| RDS for MySQL | Relational database | Provides managed backups, patching, and monitoring |
| S3 | CV and artifact storage | Durable, cost-efficient storage integrated with IAM |
| CloudFront | CDN and public endpoint | Provides edge delivery and a default HTTPS domain |
| CloudWatch and SNS | Observability and alerts | Centralizes logs, metrics, alarms, and email notifications |

## Design principles

- Only the ALB and NAT Gateway are placed in public subnets; EC2 and RDS have no public IP addresses.
- RDS accepts TCP 3306 only from the EC2 security group.
- EC2 accepts the application port only from the ALB security group.
- S3 access uses an IAM role instead of access keys stored on the server.
