---
title: "Future development"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.12.3. </b> "
---

### 5.12.3. Future development

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

| Resource group | Cost impact | Optimization guidance |
|---|---:|---|
| Multi-AZ EC2 and workers | High | Start small, monitor CPU/RAM, and scale based on demand |
| RDS Multi-AZ and read replicas | High | Enable Multi-AZ for production and right-size the database and gp3 storage |
| NAT Gateway | High with heavy data processing | Use an S3 Gateway Endpoint and minimize traffic through NAT |
| ElastiCache Redis | Medium to high | Add it only after metrics confirm a database or session bottleneck |
| CloudFront, WAF, and data transfer | Low to high depending on traffic | Improve cache hit ratio and keep WAF rules focused |
| CloudWatch, SNS, and SES | Low for a demo workload | Set log retention and create only actionable alarms |
| CI/CD, ECR, and S3 artifacts | Low to medium | Remove old images and artifacts with lifecycle policies |

{{% notice note %}}
Before production deployment, enter the expected `ap-southeast-1` resources and traffic into AWS Pricing Calculator. Create an AWS Budget and billing alerts to control monthly spending.
{{% /notice %}}

## Suggested roadmap

1. **Phase 1:** Standardize monitoring, backups, Secrets Manager, and CI/CD.
2. **Phase 2:** Deploy Multi-AZ EC2/RDS, Auto Scaling, and WAF for production.
3. **Phase 3:** Add Redis and SQS workers when monitoring confirms bottlenecks.
4. **Phase 4:** Optimize with Savings Plans, lifecycle policies, log retention, and right-sizing.
