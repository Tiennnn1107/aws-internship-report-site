---
title: "Week 10 Worklog"
date: 2026-06-19
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

{{% notice warning %}}
 **Note:** The following content records the learning and implementation activities completed during the week and is intended for the personal worklog report.
{{% /notice %}}

### Week 10 Objectives:

- Expose the backend through an Application Load Balancer with health checks.
- Place CloudFront in front of the ALB with settings suitable for a dynamic application.
- Resolve CORS and forwarded-header issues and test features through CloudFront.

### Tasks carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 06/19/2026 | Created `recruit-tg` with EC2 instance targets on port `8080`, configured health checks, and registered the backend. | 06/19/2026 | 06/19/2026 | Target Group health records |
| 06/20/2026 | Created `recruit-alb` in two public subnets and configured HTTP listener `80` to forward to `recruit-tg`. | 06/20/2026 | 06/20/2026 | ALB configuration |
| 06/21/2026 | Confirmed the target was `Healthy` and accessed the application through the ALB DNS name. | 06/21/2026 | 06/21/2026 | ALB access verification |
| 06/22/2026 | Created CloudFront in the separate AWS account being used, set the public ALB DNS as an `HTTP only` origin, and redirected viewers from HTTP to HTTPS. | 06/22/2026 | 06/22/2026 | CloudFront distribution records |
| 06/23/2026 | Allowed GET, HEAD, OPTIONS, PUT, POST, PATCH, and DELETE and selected `CachingDisabled` with origin request policy `AllViewer`. | 06/23/2026 | 06/23/2026 | CloudFront behavior configuration |
| 06/24/2026 – 06/25/2026 | Resolved CORS and login HTTP 403 `Invalid CORS request`, set `server.forward-headers-strategy=framework`, created invalidation `/*`, and tested features.<br>&emsp;Recorded the possible CloudFront Free Plan limitation on multipart uploads. | 06/24/2026 | 06/25/2026 | Application logs and CloudFront tests |

### Week 10 Achievements:

- Created `recruit-tg` and `recruit-alb` and confirmed that the backend target was `Healthy`.
- Accessed the application successfully through the ALB DNS name.
- Configured CloudFront in the account being used to forward requests to the public ALB.
- Set methods, cache policy, and origin request policy for dynamic application traffic.
- Resolved CORS and forwarded-header issues, invalidated the cache, and documented the multipart-plan limitation.
