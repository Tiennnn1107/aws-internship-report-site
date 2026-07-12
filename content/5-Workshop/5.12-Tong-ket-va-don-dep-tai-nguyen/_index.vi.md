---
title: "Tối ưu và dọn dẹp tài nguyên"
date: 2026-07-10
weight: 12
chapter: false
pre: " <b> 5.12. </b> "
---

## Tối ưu chi phí

- Dùng EC2/RDS kích thước nhỏ cho workshop; dừng hoặc xóa khi không sử dụng.
- NAT Gateway và ALB tính phí theo giờ; cân nhắc VPC Endpoint, lịch chạy và kiến trúc serverless/container cho tải nhỏ.
- Đặt S3 lifecycle, CloudWatch Logs retention và xóa snapshot/artifact không còn cần.
- Tạo AWS Budget và Cost Anomaly Detection trước khi triển khai.

## Bảo mật cơ bản

- EC2/RDS không có public IP; Security Group tham chiếu Security Group thay cho CIDR rộng.
- IAM Role theo least privilege; không lưu access key, DB password hoặc token trong Git/source code.
- Bật mã hóa S3, RDS, EBS; dùng HTTPS CloudFront/ALB và ACM certificate.
- Bật backup RDS phù hợp, CloudTrail và log nhưng tránh ghi dữ liệu nhạy cảm.

## Thứ tự clean-up an toàn

1. Lưu bằng chứng cần thiết; xóa dữ liệu demo/PII và tắt workload test.
2. Disable rồi delete CloudFront distribution.
3. Delete ALB, listener và target group.
4. Stop/terminate EC2; xóa EBS volume và Elastic IP không dùng.
5. Delete RDS; chỉ tạo final snapshot khi thực sự cần, sau đó xóa manual snapshot không dùng.
6. Empty mọi version trong S3 rồi delete bucket.
7. Delete NAT Gateway, release Elastic IP, delete VPC Endpoint.
8. Delete route table tùy chỉnh, subnet, Internet Gateway, Security Group rồi VPC.
9. Delete CloudWatch alarms/log groups, SNS topic/subscription, IAM policy/role tùy chỉnh.
10. Kiểm tra **Billing → Bills**, Cost Explorer và Resource Explorer để bảo đảm không còn tài nguyên tính phí.

## Tiêu chí hoàn thành

Không còn EC2, RDS, NAT Gateway, ALB, CloudFront distribution, Elastic IP hoặc S3 object phát sinh phí; ngân sách không có chi phí bất thường sau 24–48 giờ cập nhật dữ liệu.
