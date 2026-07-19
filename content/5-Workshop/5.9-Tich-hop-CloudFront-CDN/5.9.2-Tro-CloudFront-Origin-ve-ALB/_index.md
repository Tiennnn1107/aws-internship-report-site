---
title: "Point the CloudFront Origin to the ALB"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.9.2. </b> "
---

### 5.9.2. Point the CloudFront Origin to the ALB

In **Get started**, enter the distribution name `cloudfront_recruit`. AWS stores this value as a tag and it can be changed later.

Select **Single website or app** because RecruitBox uses one dedicated CloudFront configuration. Leave **Route 53 managed domain** empty because the current system has no custom domain and will use the default CloudFront domain. Continue to the origin step.

![Cấu hình ALB origin](</images/5-Workshop/5.9-Tich-hop-CloudFront-CDN/5.9.2-Tro-CloudFront-Origin-ve-ALB/cloudfront%202.png>)
