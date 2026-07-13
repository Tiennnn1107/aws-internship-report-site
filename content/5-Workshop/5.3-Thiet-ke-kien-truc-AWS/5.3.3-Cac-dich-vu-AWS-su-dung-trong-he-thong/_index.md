---
title: "AWS services used in the system"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.3.3. </b> "
---

### 5.3.3. AWS services used in the system

RecruitPro uses AWS services to deploy the application, store data, deliver content, and monitor operations.

```text
Route 53
    ↓ DNS
CloudFront ─────── S3 (frontend, CVs and static files)
    ↓ origin
Application Load Balancer
    ↓
EC2 (Spring Boot backend)
    ↓
RDS MySQL

CloudWatch ── monitors EC2, ALB and RDS
SNS ───────── sends alerts
IAM ───────── controls AWS permissions
VPC ───────── private network, subnets and Security Groups
```

#### Service overview

| Service | Role in the system |
|---|---|
| Amazon VPC | Provides the private network, including public and private subnets. |
| Public/Private Subnets | The ALB is placed in public subnets; the backend EC2 and RDS are placed in private subnets. |
| Security Groups | Control traffic between CloudFront/ALB, EC2 and RDS. |
| Amazon Route 53 | Provides DNS and routes the domain to CloudFront. |
| Amazon CloudFront | Delivers frontend, images and static files from edge locations; forwards API requests to the ALB. |
| Amazon S3 | Stores frontend artifacts, CVs, images and user uploads. |
| Application Load Balancer | Receives requests from CloudFront and routes them to healthy EC2 targets. |
| Amazon EC2 | Runs the Spring Boot backend application. |
| Amazon RDS for MySQL | Stores users, companies, job postings, applications, interviews and blogs. |
| AWS IAM | Manages users, roles and policies; grants EC2 the minimum S3 access required. |
| Amazon CloudWatch | Collects logs and metrics and creates alarms for EC2, ALB and RDS. |
| Amazon SNS | Sends email notifications when CloudWatch detects threshold violations. |

#### 1. Network and security layer

Amazon VPC is the system's main network layer. An Internet Gateway allows public components such as the ALB to receive external requests. A NAT Gateway allows private EC2 instances to download packages or artifacts without exposing them directly to the Internet.

Security Groups follow the least-open-port principle:

- ALB: accepts HTTPS/HTTP from users.
- EC2: accepts application traffic only from the ALB Security Group.
- RDS: accepts MySQL port `3306` only from the EC2 Security Group.
- SSH: is restricted to approved administration addresses, or Session Manager can be used where appropriate.

#### 2. Application and data layer

EC2 runs the Spring Boot backend and processes authentication, recruitment, applications and interviews. The ALB performs health checks and sends traffic only to healthy instances.

RDS for MySQL provides a managed database with backups and high availability options. The database is not placed in a public subnet and is accessed only by the backend EC2.

S3 stores files that should not be stored directly in the database, such as CVs, avatars and deployment files. MySQL stores the corresponding URL or object key.

#### 3. Content delivery layer

CloudFront reduces latency for frontend files, JavaScript, CSS, images and other static resources. Dynamic APIs are forwarded to the ALB and private or authenticated responses are not cached.

Route 53 lets users access the system through a friendly domain instead of an IP address or technical endpoint.

#### 4. IAM and permissions

An IAM Role is attached to EC2 so the backend can access only the required S3 bucket. Permanent access keys must not be stored in source code or public files.

Policies should follow least privilege. For example, grant `s3:GetObject` and `s3:PutObject` only on the RecruitPro bucket instead of granting full access to every bucket.

#### 5. Monitoring and alerting

CloudWatch monitors CPU, network traffic, ALB target health, RDS CPU and storage, and application logs. SNS receives CloudWatch notifications and sends email alerts when an incident occurs.

Typical alarms include:

- High EC2 CPU utilization.
- Unhealthy ALB targets or many 5XX errors.
- High RDS CPU or low remaining storage.
- A high number of application errors in logs.

Together, these services separate networking, application processing, database, storage and monitoring, making the system easier to scale and operate cost-effectively.
