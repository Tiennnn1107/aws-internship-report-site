---
title: "Hướng phát triển trong tương lai"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.12.3. </b> "
---

### 5.12.3. Hướng phát triển trong tương lai

> **Trạng thái hiện tại:** Hệ thống **chưa triển khai CI/CD**. Quá trình build và triển khai ứng dụng vẫn được thực hiện thủ công. Pipeline sử dụng GitHub, CodePipeline, CodeBuild và CodeDeploy dưới đây chỉ là đề xuất cho giai đoạn phát triển tiếp theo.

Sau khi hoàn thiện phiên bản hiện tại, RecruitPro có thể được mở rộng theo kiến trúc bên dưới để tăng tính sẵn sàng, khả năng mở rộng, bảo mật và mức độ tự động hóa.

![Kiến trúc AWS đề xuất cho RecruitPro trong tương lai](/images/5-Workshop/5.12-Tong-ket-va-don-dep-tai-nguyen/5.12.3-Huong-phat-trien-trong-tuong-lai/future.jpg)

*Hình 5.12.3: Kiến trúc đề xuất cho giai đoạn phát triển tiếp theo của RecruitPro.*

## Phân tích hướng phát triển

| Hạng mục | Đề xuất | Giá trị mang lại | Đánh đổi |
|---|---|---|---|
| Tính sẵn sàng | Chạy EC2 ở ít nhất hai Availability Zone, đặt sau ALB; sử dụng RDS Multi-AZ | Giảm gián đoạn khi một instance hoặc một AZ gặp sự cố | Tăng số lượng tài nguyên và chi phí vận hành |
| Hiệu năng | Bổ sung ElastiCache Redis cho session và dữ liệu truy cập thường xuyên | Giảm tải database, cải thiện thời gian phản hồi | Cần thiết kế cache invalidation và giám sát bộ nhớ |
| Xử lý nền | Đưa tác vụ nặng vào SQS và xử lý bằng worker/Bastion hoặc worker service riêng | API phản hồi nhanh hơn, tránh mất job khi tải tăng | Hệ thống trở thành bất đồng bộ và cần cơ chế retry/DLQ |
| Bảo mật | Dùng Cognito, AWS WAF, private subnet, IAM Role và Secrets Manager | Giảm rủi ro lộ thông tin đăng nhập và chặn request độc hại | Cần cấu hình rule, token flow và phân quyền cẩn thận |
| Phân phối nội dung | CloudFront phân phối frontend/static content từ S3, route request động về ALB | Giảm độ trễ và tải trực tiếp lên backend | Cần quản lý cache policy, CORS và cache invalidation |
| CI/CD | GitHub → CodePipeline → CodeBuild → ECR → CodeDeploy | Chuẩn hóa build/deploy, giảm thao tác thủ công và hỗ trợ rollback | Phát sinh thêm pipeline, artifact và thời gian quản trị |
| Quan sát hệ thống | CloudWatch Logs/Metrics/Alarm kết hợp SNS và SES | Phát hiện lỗi sớm và gửi cảnh báo tự động | Chi phí log tăng nếu lưu quá nhiều hoặc retention quá dài |

## Phân tích chi phí

Chi phí thực tế phụ thuộc region, loại instance, dung lượng lưu trữ, lưu lượng Internet và mức sử dụng. Các nhóm chi phí chính của kiến trúc tương lai gồm:

Ước tính dưới đây sử dụng **730 giờ/tháng**, region **Singapore (`ap-southeast-1`)**, workload nhỏ–trung bình, khoảng **50–100 GB lưu lượng/tháng**, giá On-Demand và chưa bao gồm thuế:

| Nhóm tài nguyên | Cấu hình giả định | Chi phí ước tính/tháng |
|---|---|---:|
| EC2 backend và worker | 2 EC2 cỡ `t3.small`/`t3.medium`, EBS gp3 | **45–90 USD** |
| RDS MySQL Multi-AZ | `db.t3.small`/`db.t4g.small`, 20–50 GB gp3 | **70–140 USD** |
| Application Load Balancer | 1 ALB và lưu lượng thấp–trung bình | **20–35 USD** |
| NAT Gateway | 2 NAT Gateway cho 2 AZ và phí xử lý dữ liệu | **75–110 USD** |
| ElastiCache Redis | 2 node nhỏ để dự phòng Multi-AZ | **30–60 USD** |
| CloudFront, WAF và data transfer | Traffic 50–100 GB, số rule cơ bản | **10–40 USD** |
| S3, EBS, snapshot và ECR | CV, static asset, artifact, image và backup | **8–25 USD** |
| CloudWatch, SNS và SES | Log retention 7–30 ngày, alarm và email mức thấp | **5–25 USD** |
| CI/CD | CodePipeline, CodeBuild và CodeDeploy ở tần suất thấp | **5–20 USD** |
| Cognito và SQS | Lượng người dùng và message thấp | **0–15 USD** |
| **Tổng dự kiến** | Kiến trúc production trong hình | **Khoảng 270–560 USD/tháng** |

Với môi trường demo chỉ dùng **1 EC2, RDS Single-AZ, 1 NAT Gateway và chưa bật Redis/WAF**, chi phí có thể giảm còn khoảng **90–180 USD/tháng**. Nếu tắt tài nguyên ngoài giờ học hoặc thay NAT Gateway bằng thiết kế endpoint phù hợp, chi phí có thể thấp hơn nữa.

{{% notice note %}}
Các số liệu trên là khoảng ước tính để lập kế hoạch, không phải báo giá của AWS. Trước khi triển khai production, cần nhập đúng cấu hình vào [AWS Pricing Calculator](https://calculator.aws/) và kiểm tra các trang giá chính thức của [Amazon EC2](https://aws.amazon.com/ec2/pricing/on-demand/), [Amazon RDS for MySQL](https://aws.amazon.com/rds/mysql/pricing/) và [Amazon VPC/NAT Gateway](https://aws.amazon.com/vpc/pricing/). Nên tạo AWS Budget và cảnh báo chi phí để kiểm soát mức sử dụng hàng tháng.
{{% /notice %}}

## Lộ trình triển khai đề xuất

1. **Giai đoạn 1:** Chuẩn hóa monitoring, backup, Secrets Manager và CI/CD.
2. **Giai đoạn 2:** Triển khai EC2/RDS Multi-AZ, Auto Scaling và WAF cho production.
3. **Giai đoạn 3:** Bổ sung Redis và SQS worker khi số liệu monitoring xác nhận điểm nghẽn.
4. **Giai đoạn 4:** Tối ưu chi phí bằng Savings Plans, lifecycle policy, log retention và right-sizing.
