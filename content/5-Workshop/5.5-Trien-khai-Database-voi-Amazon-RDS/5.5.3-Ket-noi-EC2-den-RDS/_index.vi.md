---
title: "Kết nối EC2 đến RDS"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.5.3. </b> "
---

### 5.5.3. Kết nối EC2 đến RDS

Trước khi kết nối, kiểm tra EC2 backend `RecruitPro-BE` và RDS dùng cùng một VPC. Vào **EC2 → Instances → RecruitPro-BE → Networking** để ghi lại **VPC ID** và Security Group của EC2. Sau đó vào **RDS → Databases → chọn database → Connectivity & security** và xác nhận VPC ID của RDS trùng với EC2.

Tại Security Group đang gắn với RDS, thêm inbound rule:

| Type | Protocol | Port | Source |
|---|---|---:|---|
| MySQL/Aurora | TCP | 3306 | Security Group của EC2 backend |

Không dùng `0.0.0.0/0` cho RDS. Security Group của EC2 có thể giữ outbound mặc định `All traffic → 0.0.0.0/0`; Security Group có tính stateful nên traffic phản hồi được tự động cho phép.

Trong **Connectivity & security** của RDS, copy **Endpoint** và **Port**. Chỉ sử dụng hostname, không thêm `http://` hoặc `https://`.

Kết nối vào EC2 bằng **Connect → Session Manager**. Với Amazon Linux 2023, cài MySQL command-line client:

```bash
sudo dnf update -y
sudo dnf install mariadb105 -y
mysql --version
```

Kiểm tra kết nối đến RDS:

```bash
mysql -h <RDS_ENDPOINT> -P 3306 -u admin -p
```

Nhập mật khẩu RDS khi được yêu cầu. Nếu kết nối thành công, màn hình hiển thị dấu nhắc `mysql>`. Có thể kiểm tra database bằng:

```sql
SHOW DATABASES;
CREATE DATABASE IF NOT EXISTS recruitpro;
USE recruitpro;
SHOW TABLES;
EXIT;
```

Để Spring Boot sử dụng RDS, cấu hình file environment trên EC2:

```bash
sudo nano /etc/recruitpro.env
```

```dotenv
SPRING_DATASOURCE_URL=jdbc:mysql://<RDS_ENDPOINT>:3306/recruitpro
SPRING_DATASOURCE_USERNAME=admin
SPRING_DATASOURCE_PASSWORD=<RDS_PASSWORD>
```

Lưu file, khởi động lại service và kiểm tra log:

```bash
sudo systemctl restart recruitpro
sudo systemctl status recruitpro
sudo journalctl -u recruitpro -n 100 --no-pager
```

Các dấu hiệu kết nối thành công thường gồm `HikariPool`, `Hibernate` và thông báo ứng dụng đã `Started`. Nếu gặp `Connection timed out`, kiểm tra lại VPC, inbound rule TCP 3306, endpoint, route table và NACL. Nếu gặp `Access denied`, kiểm tra username/password; nếu gặp `Unknown database`, tạo database `recruitpro` trước khi khởi động ứng dụng.