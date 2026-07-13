---
title: "Worklog Tuần 10"
date: 2026-06-19
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

{{% notice warning %}}
 **Lưu ý:** Nội dung dưới đây ghi lại quá trình học tập và thực hành trong tuần. Thông tin được sử dụng cho mục đích báo cáo worklog cá nhân.
{{% /notice %}}

### Mục tiêu Tuần 10:

- Đưa backend ra ngoài qua Application Load Balancer và health check.
- Đặt CloudFront phía trước ALB với cấu hình phù hợp cho ứng dụng động.
- Xử lý CORS, forwarded headers và kiểm tra chức năng qua CloudFront.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 19/06/2026 | Tạo Target Group `recruit-tg`, target type EC2, port `8080`; cấu hình health check và đăng ký backend. | 19/06/2026 | 19/06/2026 | Target Group health records |
| 20/06/2026 | Tạo `recruit-alb` trong hai public subnet; listener HTTP `80` forward đến `recruit-tg`. | 20/06/2026 | 20/06/2026 | ALB configuration |
| 21/06/2026 | Xác minh target `Healthy` và truy cập ứng dụng qua ALB DNS. | 21/06/2026 | 21/06/2026 | ALB access verification |
| 22/06/2026 | Tạo CloudFront ở AWS account được sử dụng riêng và trỏ origin đến public ALB DNS với `HTTP only`; redirect viewer HTTP sang HTTPS. | 22/06/2026 | 22/06/2026 | CloudFront distribution records |
| 23/06/2026 | Cho phép GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE; dùng `CachingDisabled` và origin request policy `AllViewer`. | 23/06/2026 | 23/06/2026 | CloudFront behavior configuration |
| 24/06/2026 – 25/06/2026 | Xử lý CORS và lỗi đăng nhập 403 `Invalid CORS request`; cấu hình `server.forward-headers-strategy=framework`, tạo invalidation `/*` và kiểm tra chức năng.<br>&emsp;Ghi nhận multipart upload có thể bị giới hạn bởi CloudFront Free Plan. | 24/06/2026 | 25/06/2026 | Application logs and CloudFront tests |

### Kết quả đạt được Tuần 10:

- Tạo `recruit-tg` và `recruit-alb`, xác minh backend ở trạng thái `Healthy`.
- Truy cập ứng dụng thành công qua ALB DNS.
- Cấu hình CloudFront ở account được sử dụng để phân phối request đến public ALB.
- Thiết lập method, cache policy và origin request policy cho ứng dụng động.
- Khắc phục CORS/forwarded-header, invalidation cache và ghi nhận giới hạn multipart của gói CloudFront.
