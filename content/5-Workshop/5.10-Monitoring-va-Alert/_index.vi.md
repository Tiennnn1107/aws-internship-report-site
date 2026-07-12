---
title: "Monitoring và Alert"
date: 2026-07-10
weight: 10
chapter: false
pre: " <b> 5.10. </b> "
---

## Log

1. Cài CloudWatch Agent trên EC2 và tạo log group `/recruitbox/application`.
2. Đẩy `/var/log/recruitbox/application.log` và journal của `recruitbox.service` lên CloudWatch Logs.
3. Đặt retention 14 hoặc 30 ngày; không ghi password, token, CV hoặc dữ liệu cá nhân vào log.
4. Bật ALB access logs vào S3 nếu cần audit request và CloudFront standard logs nếu cần phân tích edge traffic.

## Metric cần theo dõi

| Thành phần | Metric | Ngưỡng khởi đầu |
|---|---|---|
| EC2 | CPUUtilization | > 80% trong 10 phút |
| EC2 | StatusCheckFailed | >= 1 trong 5 phút |
| ALB | HTTPCode_Target_5XX_Count | >= 5 trong 5 phút |
| ALB | UnHealthyHostCount | >= 1 trong 2 chu kỳ |
| ALB | TargetResponseTime | p95 vượt SLO |
| RDS | CPUUtilization | > 80% trong 10 phút |
| RDS | FreeStorageSpace | < 5 GiB |
| CloudFront | 5xxErrorRate | vượt baseline |

## Alert

Tạo một SNS topic, subscribe email, sau đó nối các CloudWatch Alarm ở các mục con. Alarm phải có tên, mô tả tác động, ngưỡng, evaluation period và hành động khi `ALARM`/`OK`.

## Đo lường

Ghi baseline khi hệ thống nhàn rỗi và khi chạy kiểm thử tải. So sánh `RequestCount`, p50/p95 latency, 4xx/5xx, CPU và DB connections; điều chỉnh ngưỡng dựa trên dữ liệu thay vì giữ ngưỡng mặc định.
