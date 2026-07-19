---
title: "Install Java and the Spring Boot Runtime"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.6.3. </b> "
---

### 5.6.3. Install Java and the Spring Boot Runtime

Sau khi kết nối đến EC2 bằng **AWS Systems Manager Session Manager**, cập nhật hệ điều hành và cài đặt Java 17 cùng MySQL client:

```bash
sudo dnf update -y
sudo dnf install -y java-17-amazon-corretto mysql
java -version
mysql --version
```

Create the application directory and assign ownership to the `ec2-user` user:

```bash
sudo mkdir -p /opt/recruitpro
sudo chown ec2-user:ec2-user /opt/recruitpro
```

{{% notice note %}}
The commands above apply to Amazon Linux 2023. The EC2 instance requires outbound connectivity through a NAT Gateway or suitable VPC endpoints to download packages.
{{% /notice %}}
