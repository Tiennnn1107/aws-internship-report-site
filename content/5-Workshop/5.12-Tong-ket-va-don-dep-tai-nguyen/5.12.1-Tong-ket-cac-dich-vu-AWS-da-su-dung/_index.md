---
title: "Summary of AWS Services Used"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.12.1. </b> "
---

### 5.12.1. Summary of AWS Services Used

The workshop deployed RecruitPro as a multi-layer architecture on AWS. Each service has a distinct role in networking, application hosting, data, file storage, content delivery, and monitoring. This separation makes the system easier to manage, secure, and scale than hosting every component on one public server.

#### Completed architecture

```text
User
  │
  ▼
Amazon CloudFront
  │
  ▼
Application Load Balancer (public subnet)
  │
  ▼
Amazon EC2 - Spring Boot (private subnet)
  ├────────► Amazon RDS for MySQL (private subnet)
  └────────► Amazon S3 (CVs and deployment artifacts)

Amazon CloudWatch ──► Amazon SNS ──► Email notifications
AWS IAM ────────────► grants EC2 access to S3
```

CloudFront uses the default AWS-provided domain. Route 53 and ACM were not configured in this workshop, so they are not included as deployed services.

#### Network and connectivity layer

| Component | Implemented role |
|---|---|
| Amazon VPC | Provides an isolated network for RecruitPro resources. |
| Public Subnet | Hosts the ALB, NAT Gateway, and components requiring direct Internet connectivity. |
| Private Subnet | Hosts the EC2 backend and RDS without direct Internet exposure. |
| Internet Gateway | Provides Internet connectivity to public subnets. |
| NAT Gateway | Allows private EC2 instances to download packages and artifacts without a public IP. |
| Route Table | Routes traffic between subnets, the Internet Gateway, NAT Gateway, and S3 endpoint. |
| Security Group | Restricts traffic between the ALB, EC2, and RDS. |
| S3 Gateway Endpoint | Enables private access to S3 over the AWS network without using the NAT Gateway. |

Users can reach only the ALB. EC2 accepts application traffic from the ALB Security Group, while RDS allows MySQL port `3306` only from the EC2 Security Group.

#### Application and data layer

| Service | Implemented role |
|---|---|
| Amazon EC2 | Runs the RecruitPro Spring Boot backend as a `systemd` service. |
| Application Load Balancer | Provides a public endpoint, performs health checks, and forwards requests to healthy EC2 targets. |
| Target Group | Registers the backend EC2 instance and defines its port, protocol, and health-check path. |
| Amazon RDS for MySQL | Stores users, employers, jobs, applications, and other business data. |
| Amazon S3 | Stores candidate CVs and the backend JAR deployment artifact. |

Separating files from the database allows RDS to focus on structured data. The application stores an S3 object key or URL instead of saving binary file contents in MySQL.

#### Content delivery and access security

| Service | Implemented role |
|---|---|
| Amazon CloudFront | Provides a CDN domain and forwards user requests to the ALB origin. |
| AWS IAM | Provides an IAM Role and policy that grant EC2 access to the required S3 buckets. |

CloudFront is configured for the dynamic application with the required HTTP methods, `CachingDisabled`, and an appropriate origin request policy. The IAM Role allows the application to access S3 without storing permanent access keys in source code or on EC2.

#### Monitoring and alerting

| Service | Implemented role |
|---|---|
| Amazon CloudWatch | Collects metrics and creates alarms for EC2, ALB, and RDS. |
| Amazon SNS | Receives CloudWatch Alarm events and sends them to a confirmed email endpoint. |

The configured alarms include:

- EC2 `CPUUtilization > 80%` over a five-minute period.
- ALB `HTTPCode_Target_5XX_Count >= 1` over a five-minute period.
- ALB `UnHealthyHostCount >= 1` over a one-minute period.
- RDS `CPUUtilization > 80%` over a five-minute period.
- RDS `FreeStorageSpace < 1,000,000,000 bytes` over a five-minute period.

#### Result

RecruitPro now has a complete request path from CloudFront through the ALB and EC2 to RDS. Files are stored separately in S3, backend resources are placed in private subnets, AWS access is granted through an IAM Role, and critical metrics are monitored by CloudWatch with email alerts delivered through SNS.

The architecture is suitable for learning and testing. A production deployment should add ACM-based HTTPS, a Route 53 custom domain, multiple EC2 instances across Availability Zones, RDS Multi-AZ, centralized secret management, AWS WAF, centralized logging, and an appropriate backup policy.
