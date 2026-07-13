---
title: "Worklog Tuần 8"
date: 2026-06-05
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

{{% notice warning %}}
 **Lưu ý:** Nội dung dưới đây ghi lại quá trình học tập và thực hành trong tuần. Thông tin được sử dụng cho mục đích báo cáo worklog cá nhân.
{{% /notice %}}

### Mục tiêu Tuần 8:

- Triển khai RDS MySQL riêng tư và EC2 backend trong private app subnet.
- Kết nối quản trị EC2 bằng Systems Manager, không gán public IP.
- Deploy RecruitPro bằng JAR và systemd, đồng thời xác minh kết nối RDS.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 05/06/2026 | Tạo DB subnet group từ hai private DB subnet; tạo RDS MySQL Single-AZ, private access, port `3306`, database `recruitpro`. | 05/06/2026 | 05/06/2026 | RDS configuration records |
| 06/06/2026 | Cho RDS Security Group nhận TCP `3306` từ EC2 Security Group; tạo EC2 `RecruitPro-BE` trong private app subnet, không có public IP. | 06/06/2026 | 06/06/2026 | EC2 and Security Group records |
| 07/06/2026 | Tạo IAM Role cho EC2, gắn `AmazonSSMManagedInstanceCore` và kết nối bằng Systems Manager Session Manager. | 07/06/2026 | 07/06/2026 | Systems Manager connection record |
| 08/06/2026 | Cài Java 17 và MySQL/MariaDB client; kiểm tra EC2 kết nối tới RDS qua port `3306`. | 08/06/2026 | 08/06/2026 | EC2 terminal verification |
| 09/06/2026 | Tạo database `recruitpro`, import file SQL và kiểm tra bảng/dữ liệu mà không ghi thông tin xác thực vào worklog. | 09/06/2026 | 09/06/2026 | Database import verification |
| 10/06/2026 – 11/06/2026 | Chuẩn bị `/etc/recruitpro.env`, deploy `/opt/recruitpro/app.jar`, tạo `recruitpro.service`.<br>&emsp;Kiểm tra bằng `systemctl status`, `journalctl` và `curl localhost:8080`. | 10/06/2026 | 11/06/2026 | systemd status and application logs |

### Kết quả đạt được Tuần 8:

- Triển khai RDS MySQL Single-AZ trong private DB subnet group với database `recruitpro`.
- Tạo `RecruitPro-BE` không có public IP và quản trị thành công qua Session Manager.
- Cài Java 17, database client và xác minh kết nối EC2–RDS.
- Import dữ liệu SQL, triển khai `app.jar` và vận hành ứng dụng bằng `recruitpro.service`.
- Xác minh trạng thái service, log và phản hồi local mà không đưa mật khẩu hoặc secret vào tài liệu.
