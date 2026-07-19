---
title: "Thiết kế kiến trúc AWS"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

## Kiến trúc tổng thể

![Kiến trúc AWS tổng thể của RecruitPro](</images/5-Workshop/5.3-Thiet-ke-kien-truc-AWS/5.3.1-Tong-quan-kien-truc-he-thong/hientai.jpg>)

Luồng request chính là **Người dùng → CloudFront → Application Load Balancer → EC2 Spring Boot → RDS MySQL**. Backend lưu CV trên S3, tải deployment artifact từ một S3 bucket riêng và gửi dữ liệu vận hành đến CloudWatch cùng SNS.

## Dịch vụ và lý do lựa chọn

| Dịch vụ | Vai trò | Lý do lựa chọn |
|---|---|---|
| VPC | Cô lập mạng | Chia public, application và database tier rõ ràng |
| ALB | Điểm vào HTTP | Health check, cân bằng tải và hỗ trợ mở rộng nhiều EC2 |
| EC2 | Chạy Spring Boot | Phù hợp ứng dụng JAR hiện có và cho phép kiểm soát OS |
| RDS MySQL | Cơ sở dữ liệu | Tự động backup, patching và giám sát |
| S3 | Lưu CV/artifact | Bền vững, chi phí thấp, tích hợp IAM |
| CloudFront | CDN | HTTPS mặc định, edge cache và che giấu ALB khỏi người dùng |
| CloudWatch/SNS | Quan sát và cảnh báo | Tập trung log, metric, alarm và email |

## Nguyên tắc thiết kế

- Chỉ ALB/NAT nằm trong public subnet; EC2 và RDS không có public IP.
- RDS chỉ nhận TCP 3306 từ Security Group của EC2.
- EC2 chỉ nhận cổng ứng dụng từ Security Group của ALB.
- Quyền truy cập S3 được cấp qua IAM Role, không lưu access key trên máy chủ.

Tiếp tục theo thứ tự từ **5.4 đến 5.12** để triển khai, kiểm thử, giám sát và dọn dẹp.
