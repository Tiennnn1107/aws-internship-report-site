---
title: "Monitoring and Alerting"
date: 2026-07-10
weight: 10
chapter: false
pre: " <b> 5.10. </b> "
---

## 5.10. Monitoring and Alerting

## Logs

1. Install the CloudWatch Agent on EC2 and create log group `/recruitbox/application`.
2. Send the application log and `recruitbox.service` journal output to CloudWatch Logs.
3. Set retention to 14 or 30 days. Never log passwords, tokens, CV contents, or personal data.
4. Enable ALB access logs in S3 or CloudFront standard logs when request auditing is required.

## Metrics to monitor

| Component | Metric | Initial threshold |
|---|---|---|
| EC2 | CPUUtilization | > 80% for 10 minutes |
| EC2 | StatusCheckFailed | >= 1 for 5 minutes |
| ALB | HTTPCode_Target_5XX_Count | >= 5 for 5 minutes |
| ALB | UnHealthyHostCount | >= 1 for two periods |
| ALB | TargetResponseTime | p95 exceeds the SLO |
| RDS | CPUUtilization | > 80% for 10 minutes |
| RDS | FreeStorageSpace | < 5 GiB |
| CloudFront | 5xxErrorRate | Exceeds the established baseline |

## Alerts and measurement

Create an SNS topic, confirm an email subscription, and connect it to the CloudWatch alarms in the following pages. Each alarm needs a meaningful name, impact description, threshold, evaluation period, and actions for both `ALARM` and `OK`.

Record an idle baseline and a controlled-load baseline. Compare request count, p50/p95 latency, 4xx/5xx responses, CPU, and database connections, then tune thresholds from observed data.
