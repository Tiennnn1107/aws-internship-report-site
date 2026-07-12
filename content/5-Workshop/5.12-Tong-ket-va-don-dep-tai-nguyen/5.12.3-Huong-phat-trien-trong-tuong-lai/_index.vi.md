---
title: "Hướng phát triển trong tương lai"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.12.3. </b> "
---

### 5.12.3. Hướng phát triển trong tương lai

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

| Nhóm tài nguyên | Mức ảnh hưởng chi phí | Gợi ý tối ưu |
|---|---:|---|
| EC2 chạy Multi-AZ và worker | Cao | Bắt đầu với instance nhỏ, theo dõi CPU/RAM và dùng Auto Scaling theo nhu cầu |
| RDS Multi-AZ và read replica | Cao | Chỉ bật Multi-AZ cho production; chọn đúng instance class và dung lượng gp3 |
| NAT Gateway | Cao khi có nhiều dữ liệu xử lý | Dùng S3 Gateway Endpoint, hạn chế traffic đi qua NAT và cân nhắc một NAT cho môi trường demo |
| ElastiCache Redis | Trung bình đến cao | Chỉ triển khai khi metric cho thấy database hoặc session là điểm nghẽn |
| CloudFront, WAF và truyền dữ liệu | Thấp đến cao tùy traffic | Tối ưu cache hit ratio, giới hạn WAF rule và theo dõi data transfer |
| CloudWatch Logs, SNS và SES | Thấp ở quy mô demo | Đặt log retention, lọc log không cần thiết và tạo alarm theo ngưỡng hữu ích |
| CI/CD, ECR và artifact S3 | Thấp đến trung bình | Xóa image/artifact cũ bằng lifecycle policy và chỉ chạy pipeline khi cần |

{{% notice note %}}
Trước khi triển khai production, cần nhập đúng region `ap-southeast-1`, cấu hình instance và lưu lượng dự kiến vào AWS Pricing Calculator. Nên tạo AWS Budget và cảnh báo chi phí để kiểm soát mức sử dụng hàng tháng.
{{% /notice %}}

## Lộ trình triển khai đề xuất

1. **Giai đoạn 1:** Chuẩn hóa monitoring, backup, Secrets Manager và CI/CD.
2. **Giai đoạn 2:** Triển khai EC2/RDS Multi-AZ, Auto Scaling và WAF cho production.
3. **Giai đoạn 3:** Bổ sung Redis và SQS worker khi số liệu monitoring xác nhận điểm nghẽn.
4. **Giai đoạn 4:** Tối ưu chi phí bằng Savings Plans, lifecycle policy, log retention và right-sizing.
