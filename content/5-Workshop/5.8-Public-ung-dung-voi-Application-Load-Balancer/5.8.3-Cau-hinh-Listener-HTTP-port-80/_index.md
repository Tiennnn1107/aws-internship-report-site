---
title: "Configure the HTTP Listener on Port 80"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.8.3. </b> "
---

### 5.8.3. Configure the HTTP Listener on Port 80

1. Open the ALB and select **Listeners and rules → Add listener**.
2. Choose HTTP port `80` and set the default action to **Forward to `recruit-backend-tg`**.
3. Save the listener and confirm that the forwarding rule has `default` priority.

For production, request a certificate in ACM, add an HTTPS 443 listener, and change HTTP 80 to redirect to HTTPS 443.

![Thêm listener](</images/5-Workshop/5.8-Public-ung-dung-voi-Application-Load-Balancer/5.8.3-Cau-hinh-Listener-HTTP-port-80/alb%203.png>)
![Forward tới Target Group](</images/5-Workshop/5.8-Public-ung-dung-voi-Application-Load-Balancer/5.8.3-Cau-hinh-Listener-HTTP-port-80/alb%204.png>)
