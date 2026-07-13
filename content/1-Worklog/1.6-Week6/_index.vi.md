---
title: "Worklog Tuần 6"
date: 2026-05-22
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

{{% notice warning %}}
 **Lưu ý:** Nội dung dưới đây ghi lại quá trình học tập và thực hành trong tuần. Thông tin được sử dụng cho mục đích báo cáo worklog cá nhân.
{{% /notice %}}

### Mục tiêu Tuần 6:

- Phân tích source code, chức năng và cách đóng gói của RecruitBox/RecruitPro.
- Lựa chọn kiến trúc AWS phù hợp với phạm vi và chi phí dự án.
- Hoàn thiện sơ đồ kiến trúc ban đầu và phân biệt rõ phần triển khai với phần hoãn.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 22/05/2026 | Đọc source code RecruitBox/RecruitPro; xác định Spring Boot, Thymeleaf, MySQL và quy trình đóng gói JAR. | 22/05/2026 | 22/05/2026 | Source code RecruitBox/RecruitPro |
| 23/05/2026 | Liệt kê luồng đăng ký/đăng nhập, quản lý user, xem việc làm, cập nhật hồ sơ, upload CV và quản lý dữ liệu tuyển dụng. | 23/05/2026 | 23/05/2026 | Source code RecruitBox/RecruitPro |
| 24/05/2026 | So sánh Fargate với EC2 theo mức độ phù hợp, khả năng quản trị và chi phí; chọn EC2 cho backend. | 24/05/2026 | 24/05/2026 | <https://aws.amazon.com/ec2/pricing/on-demand/> |
| 25/05/2026 | Thiết kế luồng User → CloudFront hoặc ALB → EC2 Spring Boot → RDS MySQL; S3 lưu CV. | 25/05/2026 | 25/05/2026 | Sơ đồ kiến trúc dự án |
| 26/05/2026 | Xác định VPC, IAM, Systems Manager, EC2, RDS, S3, ALB, CloudFront, CloudWatch và SNS cần cho triển khai. | 26/05/2026 | 26/05/2026 | Ghi chú thiết kế kiến trúc |
| 27/05/2026 – 28/05/2026 | Vẽ, chỉnh sơ đồ và ước tính chi phí sơ bộ.<br>&emsp;Loại bỏ hoặc hoãn Cognito, Bedrock, SQS, worker daemon và ElastiCache. | 27/05/2026 | 28/05/2026 | <https://aws.amazon.com/vpc/pricing/>; <https://aws.amazon.com/rds/mysql/pricing/> |

### Kết quả đạt được Tuần 6:

- Hiểu cấu trúc ứng dụng Spring Boot/Thymeleaf/MySQL và hình thức JAR deployment.
- Xác định đúng các chức năng chính và dữ liệu cần đưa lên AWS.
- Chọn EC2 cho backend sau khi so sánh với Fargate.
- Hoàn thiện kiến trúc ban đầu gồm ALB/CloudFront, EC2, RDS và S3 cùng ước tính chi phí sơ bộ.
- Ghi rõ Cognito, Bedrock, SQS, worker daemon và ElastiCache là các thành phần đã loại bỏ hoặc hoãn, chưa triển khai.
