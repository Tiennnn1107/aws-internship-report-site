---
title: "Configure Cache Behavior for the Dynamic Application"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.9.3. </b> "
---

### 5.9.3. Configure Cache Behavior for the Dynamic Application

In **Specify origin**, select **Elastic Load Balancer** and choose the RecruitBox ALB DNS name. Leave **Origin path** empty because the application is served from the ALB root path.

CloudFront will receive viewer requests and forward them to the ALB, which distributes them to the backend target group.

![Cấu hình cache behavior](</images/5-Workshop/5.9-Tich-hop-CloudFront-CDN/5.9.3-Cau-hinh-Cache-Behavior-cho-ung-dung-dong/cloudfront%203.png>)
