---
title: "Worklog Tuần 11"
date: 2026-06-26
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

{{% notice warning %}}
 **Lưu ý:** Nội dung dưới đây ghi lại quá trình học tập và thực hành trong tuần. Thông tin được sử dụng cho mục đích báo cáo worklog cá nhân.
{{% /notice %}}

### Mục tiêu Tuần 11:

- Thiết lập kênh cảnh báo email bằng SNS.
- Tạo CloudWatch Alarm cho EC2, ALB và RDS theo các metric vận hành chính.
- Kiểm tra trạng thái và luồng cảnh báo từ resource đến email quản trị.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 26/06/2026 | Tạo SNS topic `recruitpro-alert-topic`, tạo email subscription và xác nhận subscription trong email. | 26/06/2026 | 26/06/2026 | SNS topic and subscription records |
| 27/06/2026 | Tạo alarm `RecruitPro-EC2-High-CPU` và `RecruitPro-ALB-Target-5XX`; cấu hình alarm action gửi SNS. | 27/06/2026 | 27/06/2026 | CloudWatch Alarm records |
| 28/06/2026 | Tạo alarm `RecruitPro-ALB-Unhealthy-Target`; kiểm tra metric và target health liên quan. | 28/06/2026 | 28/06/2026 | CloudWatch and ALB metrics |
| 29/06/2026 | Tạo `RecruitPro-RDS-High-CPU` và `RecruitPro-RDS-Low-Storage`; gắn action đến SNS topic. | 29/06/2026 | 29/06/2026 | CloudWatch and RDS metrics |
| 30/06/2026 | Theo dõi các trạng thái `OK`, `In alarm`, `Insufficient data`; kiểm tra một lần alarm ALB 5XX đã được kích hoạt. | 30/06/2026 | 30/06/2026 | Alarm history and notification email |
| 01/07/2026 – 02/07/2026 | Chụp danh sách alarm và `Actions enabled`; mô tả luồng EC2/ALB/RDS → CloudWatch → SNS → Admin Email. | 01/07/2026 | 02/07/2026 | Monitoring screenshots and personal notes |

### Kết quả đạt được Tuần 11:

- Tạo và xác nhận email subscription cho `recruitpro-alert-topic`.
- Hoàn thành năm CloudWatch Alarm đúng tên cho EC2, ALB và RDS.
- Kết nối alarm action tới SNS và theo dõi được ba trạng thái alarm.
- Xác minh alarm ALB 5XX có thể chuyển sang `In alarm` và gửi thông báo.
- Hoàn thiện bằng chứng monitoring mà không sử dụng SES vì SES chưa được triển khai.
