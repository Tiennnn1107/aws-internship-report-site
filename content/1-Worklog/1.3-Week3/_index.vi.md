---
title: "Worklog Tuần 3"
date: 2026-05-01
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

{{% notice warning %}}
 **Lưu ý:** Nội dung dưới đây ghi lại quá trình học tập và thực hành trong tuần. Thông tin được sử dụng cho mục đích báo cáo worklog cá nhân.
{{% /notice %}}

### Mục tiêu Tuần 3:

- Xây dựng mô hình Linux VPC và Windows VPC trên hai Availability Zone.
- Thực hành quản trị EC2, EBS, AMI, IAM và phương thức truy cập instance không phụ thuộc SSH công khai.
- Cài web server và database thử nghiệm, đồng thời ghi nhận lỗi cấu hình.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 01/05/2026 | Thiết kế Linux VPC và Windows VPC trên 2 AZ; tạo public/private subnet, Internet Gateway, NAT Gateway và route table. | 01/05/2026 | 01/05/2026 | AWS VPC configuration |
| 02/05/2026 | Tạo Security Group và khởi tạo EC2 Linux, EC2 Windows.<br>&emsp;Thử EC2 Instance Connect Endpoint hoặc Systems Manager Session Manager. | 02/05/2026 | 02/05/2026 | EC2 connection records |
| 03/05/2026 | Đổi instance type từ `t3.micro` sang `t3.medium` khi cần; tạo EBS Snapshot và custom AMI từ EC2. | 03/05/2026 | 03/05/2026 | EC2 and EBS console records |
| 04/05/2026 – 05/05/2026 | Tạo và gắn IAM Role; cài Apache, xác minh trang `It works!` và cấu hình quyền thư mục `/var/www`. | 04/05/2026 | 05/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 06/05/2026 | Cài MariaDB và phpMyAdmin; tạo database/table thử nghiệm `awsuser`. | 06/05/2026 | 06/05/2026 | Web server implementation notes |
| 07/05/2026 | Tạo IAM Policy `RegionRestrict`; thử giới hạn region, instance family hoặc IP và tổng hợp lỗi về route, quyền và kết nối. | 07/05/2026 | 07/05/2026 | IAM policy and troubleshooting notes |

### Kết quả đạt được Tuần 3:

- Hoàn thành hai mô hình VPC đa AZ cho môi trường Linux và Windows.
- Quản lý được vòng đời EC2, thay đổi instance type, tạo Snapshot và custom AMI.
- Truy cập instance bằng EC2 Instance Connect Endpoint hoặc Session Manager và gắn IAM Role phù hợp.
- Cài Apache, MariaDB, phpMyAdmin và tạo dữ liệu thử nghiệm `awsuser`.
- Hiểu cách policy `RegionRestrict` ảnh hưởng đến quyền thao tác và biết kiểm tra lỗi route, Security Group, IAM.
