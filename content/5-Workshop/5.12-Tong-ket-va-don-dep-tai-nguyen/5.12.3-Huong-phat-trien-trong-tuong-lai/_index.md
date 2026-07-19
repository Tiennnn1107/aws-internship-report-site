---
title: "Future development"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.12.3. </b> "
---

### 5.12.3. Future development

> **Current status:** The system **does not currently implement CI/CD**. The application is still built and deployed manually. The GitHub, CodePipeline, CodeBuild, and CodeDeploy pipeline described below is only a proposal for a future development phase.

After completing the current version, RecruitPro can evolve toward the following architecture to improve availability, scalability, security, and deployment automation.

![Proposed future AWS architecture for RecruitPro](/images/5-Workshop/5.12-Tong-ket-va-don-dep-tai-nguyen/5.12.3-Huong-phat-trien-trong-tuong-lai/future.jpg)

*Figure 5.12.3: Proposed architecture for the next development phase of RecruitPro.*

## Development analysis

| Area | Proposal | Benefit | Trade-off |
|---|---|---|---|
| Availability | Run EC2 in at least two Availability Zones behind an ALB and use RDS Multi-AZ | Reduces disruption when an instance or AZ fails | More resources and higher operating cost |
| Performance | Add ElastiCache Redis for sessions and frequently accessed data | Reduces database load and response time | Requires cache invalidation and memory monitoring |
| Background jobs | Send heavy jobs to SQS and process them with a dedicated worker service | Keeps the API responsive and prevents job loss during traffic spikes | Introduces asynchronous processing, retries, and DLQ handling |
| Security | Use Cognito, AWS WAF, private subnets, IAM roles, and Secrets Manager | Protects credentials and filters malicious requests | Requires careful rules, token flows, and access control |
| Content delivery | Serve static content from S3 through CloudFront and route dynamic requests to the ALB | Reduces latency and direct backend load | Requires cache policy, CORS, and invalidation management |
| CI/CD | GitHub → CodePipeline → CodeBuild → ECR → CodeDeploy | Standardizes deployment and supports rollback | Adds pipeline resources and administration |
| Observability | Combine CloudWatch Logs, Metrics, and Alarms with SNS and SES | Detects failures early and sends automated notifications | Logging cost increases with volume and retention |

## Cost analysis

Actual cost depends on the region, instance sizes, storage, Internet traffic, and utilization. The main cost drivers are:

The estimate below assumes **730 hours/month**, the **Singapore Region (`ap-southeast-1`)**, a small-to-medium workload, **50–100 GB/month** of traffic, On-Demand pricing, and excludes taxes:

| Resource group | Assumed configuration | Estimated monthly cost |
|---|---|---:|
| EC2 backend and worker | 2 `t3.small`/`t3.medium` instances with gp3 EBS | **USD 45–90** |
| RDS MySQL Multi-AZ | `db.t3.small`/`db.t4g.small` with 20–50 GB gp3 | **USD 70–140** |
| Application Load Balancer | 1 ALB with low-to-medium traffic | **USD 20–35** |
| NAT Gateway | 2 NAT Gateways across 2 AZs plus data processing | **USD 75–110** |
| ElastiCache Redis | 2 small nodes for Multi-AZ resilience | **USD 30–60** |
| CloudFront, WAF, and transfer | 50–100 GB traffic with basic WAF rules | **USD 10–40** |
| S3, EBS, snapshots, and ECR | CVs, static assets, artifacts, images, and backups | **USD 8–25** |
| CloudWatch, SNS, and SES | 7–30 day log retention and light alert usage | **USD 5–25** |
| CI/CD | Low-frequency CodePipeline, CodeBuild, and CodeDeploy usage | **USD 5–20** |
| Cognito and SQS | Low user and message volume | **USD 0–15** |
| **Estimated total** | Production architecture shown above | **Approximately USD 270–560/month** |

A demo environment using **one EC2 instance, Single-AZ RDS, one NAT Gateway, and no Redis/WAF** may cost approximately **USD 90–180/month**. Turning off resources outside lab hours or replacing NAT traffic with suitable VPC endpoints can reduce it further.

{{% notice note %}}
These figures are planning ranges, not an AWS quotation. Before production deployment, enter the exact configuration into [AWS Pricing Calculator](https://calculator.aws/) and verify the official [Amazon EC2](https://aws.amazon.com/ec2/pricing/on-demand/), [Amazon RDS for MySQL](https://aws.amazon.com/rds/mysql/pricing/), and [Amazon VPC/NAT Gateway](https://aws.amazon.com/vpc/pricing/) pricing pages. Create an AWS Budget and billing alerts to control monthly spending.
{{% /notice %}}

## Suggested roadmap

1. **Phase 1:** Standardize monitoring, backups, Secrets Manager, and CI/CD.
2. **Phase 2:** Deploy Multi-AZ EC2/RDS, Auto Scaling, and WAF for production.
3. **Phase 3:** Add Redis and SQS workers when monitoring confirms bottlenecks.
4. **Phase 4:** Optimize with Savings Plans, lifecycle policies, log retention, and right-sizing.
