---
title: "Chuẩn bị tài khoản AWS và Region triển khai"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.2.3. </b> "
---

### 5.2.3. Chuẩn bị tài khoản AWS và Region triển khai

Sử dụng tài khoản AWS có quyền tạo các tài nguyên VPC, EC2, RDS, S3, Elastic Load Balancing, CloudFront, CloudWatch, SNS và IAM cần thiết cho workshop.

1. Đăng nhập AWS Management Console bằng danh tính quản trị dành cho workshop. Không sử dụng root user cho các thao tác triển khai hằng ngày.
2. Bật xác thực đa yếu tố và cấu hình AWS Budget hoặc cảnh báo chi phí trước khi tạo tài nguyên.
3. Chọn một Region và sử dụng nhất quán cho các dịch vụ theo Region. Workshop này sử dụng **Asia Pacific (Singapore) — `ap-southeast-1`**.
4. Kiểm tra Region ở góc trên bên phải AWS Management Console trước khi tạo bất kỳ tài nguyên nào.
5. Ghi lại Region, account ID và quy ước đặt tên tài nguyên để dùng nhất quán ở các bước sau.

CloudFront và IAM là dịch vụ global; VPC, EC2, RDS, ALB và phần lớn cấu hình S3 được tạo hoặc quản lý theo Region.

![Region của tài khoản AWS](/images/5-Workshop/5.2-Chuan-bi-moi-truong-trien-khai/5.2.3-Chuan-bi-tai-khoan-AWS-va-region-trien-khai/user%20region.png)
