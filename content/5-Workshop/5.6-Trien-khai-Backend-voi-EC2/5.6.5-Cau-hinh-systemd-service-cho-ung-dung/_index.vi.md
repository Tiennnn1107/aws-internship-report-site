---
title: "Cấu hình systemd service cho ứng dụng"
date: 2026-07-10
weight: 5
chapter: false
pre: " <b> 5.6.5. </b> "
---

### 5.6.5. Cấu hình systemd service cho ứng dụng

#### Bước 1: Tạo file biến môi trường

Trên EC2, tạo file `/etc/recruitpro.env`:

```bash
sudo nano /etc/recruitpro.env
```

Thêm cấu hình sau và thay các giá trị đặt trong dấu `<...>`:

```ini
SPRING_DATASOURCE_URL=jdbc:mysql://<RDS_ENDPOINT>:3306/recruitpro
SPRING_DATASOURCE_USERNAME=admin
SPRING_DATASOURCE_PASSWORD=<RDS_PASSWORD>

AWS_REGION=ap-southeast-1
S3_CV_BUCKET=recruitpro-cv-storage-tien

SERVER_FORWARD_HEADERS_STRATEGY=framework

APP_CORS_ALLOWED_ORIGINS=http://localhost:8080,http://localhost:3000,http://127.0.0.1:8080,http://127.0.0.1:3000,http://recruit-alb-1002681411.ap-southeast-1.elb.amazonaws.com,https://*.cloudfront.net,http://*.cloudfront.net
```

Nếu ứng dụng sử dụng JWT, thêm:

```ini
JWT_SECRET=<SECRET_BASE64_CUA_BAN>
```

Bảo vệ file vì file chứa thông tin đăng nhập database:

```bash
sudo chown root:root /etc/recruitpro.env
sudo chmod 600 /etc/recruitpro.env
```

#### Bước 2: Tạo systemd service

Tạo file service:

```bash
sudo nano /etc/systemd/system/recruitpro.service
```

Nội dung file:

```ini
[Unit]
Description=RecruitPro Spring Boot App
After=network.target

[Service]
User=ec2-user
WorkingDirectory=/opt/recruitpro
EnvironmentFile=/etc/recruitpro.env
ExecStart=/usr/bin/java -jar /opt/recruitpro/app.jar
SuccessExitStatus=143
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
```

Nạp lại systemd, bật tự khởi động và chạy ứng dụng:

```bash
sudo systemctl daemon-reload
sudo systemctl enable recruitpro
sudo systemctl start recruitpro
sudo systemctl status recruitpro
```

Kiểm tra ứng dụng trực tiếp trên EC2:

```bash
curl http://localhost:8080
```

Xem 100 dòng log gần nhất nếu service không khởi động thành công:

```bash
sudo journalctl -u recruitpro -n 100 --no-pager
```
