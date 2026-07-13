---
title: "Worklog Tuần 7"
date: 2026-05-29
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

{{% notice warning %}}
 **Lưu ý:** Nội dung dưới đây ghi lại quá trình học tập và thực hành trong tuần. Thông tin được sử dụng cho mục đích báo cáo worklog cá nhân.
{{% /notice %}}

### Mục tiêu Tuần 7:

- Xây dựng `RecruitVPC` tại `ap-southeast-1` với mô hình subnet đa AZ.
- Cấu hình đường ra Internet cho lớp public và private app nhưng giữ lớp database riêng tư.
- Thiết lập Security Group theo luồng ALB → EC2 → RDS.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 29/05/2026 | Tạo `RecruitVPC` CIDR `10.0.0.0/16` tại `ap-southeast-1`; chọn hai Availability Zone. | 29/05/2026 | 29/05/2026 | AWS VPC configuration |
| 30/05/2026 | Tạo public subnet AZ1 `10.0.1.0/24`, AZ2 `10.0.2.0/24`; private app AZ1 `10.0.11.0/24`, AZ2 `10.0.12.0/24`. | 30/05/2026 | 30/05/2026 | RecruitVPC subnet records |
| 31/05/2026 | Tạo private DB subnet AZ1 `10.0.21.0/24` và AZ2 `10.0.22.0/24`; kiểm tra CIDR không chồng lấn. | 31/05/2026 | 31/05/2026 | RecruitVPC subnet records |
| 01/06/2026 | Tạo Internet Gateway; tạo NAT Gateway trong public subnet và gán Elastic IP. | 01/06/2026 | 01/06/2026 | AWS VPC configuration |
| 02/06/2026 | Cấu hình public route table, private app route table đi qua NAT Gateway và private DB route table không có default Internet route. | 02/06/2026 | 02/06/2026 | Route table verification |
| 03/06/2026 – 04/06/2026 | Tạo Security Group cho ALB, EC2 backend và RDS; kiểm tra route và luồng kết nối giữa các lớp. | 03/06/2026 | 04/06/2026 | Security Group and connectivity checks |

### Kết quả đạt được Tuần 7:

- Hoàn thành `RecruitVPC` với sáu subnet phân bố trên hai AZ.
- Cấu hình Internet Gateway, NAT Gateway, Elastic IP và ba nhóm route table đúng vai trò.
- Tạo chuỗi Security Group giới hạn traffic từ ALB đến EC2 và từ EC2 đến RDS.
- Giải thích được EC2 và RDS nằm trong private subnet để giảm bề mặt truy cập trực tiếp; RDS không cần đường ra Internet.
