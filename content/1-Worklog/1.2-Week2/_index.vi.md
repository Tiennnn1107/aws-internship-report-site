---
title: "Worklog Tuần 2"
date: 2026-04-24
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

{{% notice warning %}}
 **Lưu ý:** Nội dung dưới đây ghi lại quá trình học tập và thực hành trong tuần. Thông tin được sử dụng cho mục đích báo cáo worklog cá nhân.
{{% /notice %}}

### Mục tiêu Tuần 2:

- Hiểu thành phần và cách định tuyến trong Amazon VPC.
- Tạo VPC demo có public subnet, private subnet, Internet Gateway và route table.
- Phân biệt Security Group với Network ACL và kiểm tra kết nối EC2.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 24/04/2026 | Tìm hiểu Amazon VPC, CIDR và sự khác nhau giữa public subnet với private subnet. | 24/04/2026 | 24/04/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 25/04/2026 | Tạo `VPC-DEMO` với CIDR `10.10.0.0/16`; tạo public subnet và private subnet. | 25/04/2026 | 25/04/2026 | AWS Management Console |
| 26/04/2026 – 27/04/2026 | Tạo Internet Gateway, gắn vào VPC và cấu hình public route table có default route ra Internet. | 26/04/2026 | 27/04/2026 | AWS VPC configuration |
| 28/04/2026 | Tìm hiểu rule stateful của Security Group và rule stateless của Network ACL; rà soát inbound và outbound. | 28/04/2026 | 28/04/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 29/04/2026 – 30/04/2026 | Tạo EC2 trong `VPC-DEMO`; kiểm tra route, subnet, public IP và khả năng kết nối Internet. | 29/04/2026 | 30/04/2026 | EC2 and VPC verification results |

### Kết quả đạt được Tuần 2:

- Tạo được `VPC-DEMO` và phân chia public/private subnet theo CIDR.
- Cấu hình được Internet Gateway và route table cho public subnet.
- Giải thích được khác biệt giữa public subnet, private subnet, Security Group và Network ACL.
- Xác minh được đường đi kết nối của EC2 trong VPC.
