---
title: "Cấu hình Listener HTTP port 80"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.8.3. </b> "
---

## Các bước chi tiết

1. Mở ALB → tab **Listeners and rules → Add listener**.
2. Chọn HTTP port `80`; default action **Forward to `recruit-backend-tg`**.
3. Lưu listener và xác nhận rule mặc định có priority `default`.

![Thêm listener](</images/5-Workshop/5.8-Public-ung-dung-voi-Application-Load-Balancer/5.8.3-Cau-hinh-Listener-HTTP-port-80/alb%203.png>)
![Forward tới Target Group](</images/5-Workshop/5.8-Public-ung-dung-voi-Application-Load-Balancer/5.8.3-Cau-hinh-Listener-HTTP-port-80/alb%204.png>)

## Bảo mật production

Tạo certificate trong ACM, thêm listener HTTPS 443 và đổi HTTP 80 thành redirect sang HTTPS 443.
