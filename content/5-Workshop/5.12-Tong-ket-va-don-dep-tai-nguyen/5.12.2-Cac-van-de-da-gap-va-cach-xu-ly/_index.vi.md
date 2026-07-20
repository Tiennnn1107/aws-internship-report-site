---
title: "Các vấn đề đã gặp và cách xử lý"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.12.2. </b> "
---

### 5.12.2. Các vấn đề đã gặp và cách xử lý

Trong quá trình triển khai RecruitPro trên AWS, một số lỗi phát sinh ở các lớp mạng, ứng dụng, cơ sở dữ liệu và lưu trữ. Bảng dưới đây tổng hợp dấu hiệu nhận biết, nguyên nhân và cách xử lý đã áp dụng.

| Vấn đề | Nguyên nhân | Cách xử lý |
|---|---|---|
| EC2 private không tải được package hoặc artifact | Private subnet chưa có route đi qua NAT Gateway hoặc NAT Gateway chưa gắn Elastic IP | Kiểm tra route table của application subnet, bổ sung route `0.0.0.0/0` đến NAT Gateway và xác nhận NAT Gateway ở trạng thái `Available` |
| Backend không kết nối được RDS MySQL | Sai endpoint/thông tin đăng nhập hoặc Security Group của RDS chưa cho phép nguồn từ EC2 | Dùng đúng RDS endpoint và port `3306`; cấu hình inbound MySQL/Aurora trên RDS Security Group với source là EC2 Security Group, sau đó kiểm tra bằng MySQL client từ EC2 |
| Ứng dụng khởi động nhưng target của ALB ở trạng thái `unhealthy` | Sai health-check path/port, ứng dụng chỉ lắng nghe trên localhost hoặc EC2 Security Group chặn traffic từ ALB | Đặt health-check path trả về HTTP `200`, cho ứng dụng lắng nghe trên `0.0.0.0:8080` và chỉ mở port ứng dụng từ ALB Security Group |
| Upload CV lên S3 bị `AccessDenied` | IAM Role thiếu quyền object hoặc bucket name/prefix không khớp | Gắn IAM Role cho EC2, bổ sung quyền tối thiểu `s3:PutObject`, `s3:GetObject`, `s3:DeleteObject` trên đúng ARN của bucket/prefix và không lưu access key trong mã nguồn |
| CloudFront vẫn hiển thị nội dung cũ | Object đã được cache tại edge location | Tạo invalidation cho đường dẫn cần cập nhật, kiểm tra cache policy và dùng tên file có version cho các static asset thay đổi thường xuyên |
| Không nhận được email cảnh báo CloudWatch | SNS subscription chưa được xác nhận hoặc alarm chưa đúng metric/threshold | Xác nhận subscription trong email, kiểm tra topic gắn với alarm và thực hiện test để bảo đảm alarm chuyển từ `OK` sang `ALARM` |

Sau mỗi lần sửa, hệ thống được kiểm tra lại theo luồng hoàn chỉnh: người dùng gửi request qua CloudFront và ALB, backend truy cập RDS/S3, sau đó CloudWatch ghi nhận metric và log. Cách kiểm tra theo từng lớp giúp khoanh vùng lỗi nhanh hơn và tránh mở rộng Security Group không cần thiết.
