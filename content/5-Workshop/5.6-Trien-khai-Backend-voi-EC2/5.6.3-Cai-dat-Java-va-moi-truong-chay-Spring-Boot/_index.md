---
title: "Cài đặt Java và môi trường chạy Spring Boot"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.6.3. </b> "
---

### 5.6.3. Cài đặt Java và môi trường chạy Spring Boot

Sau khi kết nối đến EC2 bằng **AWS Systems Manager Session Manager**, cập nhật hệ điều hành và cài đặt Java 17 cùng MySQL client:

```bash
sudo dnf update -y
sudo dnf install -y java-17-amazon-corretto mysql
java -version
mysql --version
```

Tạo thư mục dùng để lưu ứng dụng và cấp quyền sở hữu cho người dùng `ec2-user`:

```bash
sudo mkdir -p /opt/recruitpro
sudo chown ec2-user:ec2-user /opt/recruitpro
```

{{% notice note %}}
Các lệnh trên áp dụng cho Amazon Linux 2023. EC2 cần có đường ra Internet thông qua NAT Gateway hoặc các VPC endpoint phù hợp để tải package.
{{% /notice %}}
