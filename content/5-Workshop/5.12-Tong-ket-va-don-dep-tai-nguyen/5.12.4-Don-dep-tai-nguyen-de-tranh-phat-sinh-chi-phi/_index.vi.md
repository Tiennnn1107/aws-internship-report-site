---
title: "Dọn dẹp tài nguyên để tránh phát sinh chi phí"
date: 2026-07-10
weight: 4
chapter: false
pre: " <b> 5.12.4. </b> "
---

### 5.12.4. Dọn dẹp tài nguyên để tránh phát sinh chi phí

Hiện tại, các tài nguyên AWS vẫn được duy trì để phục vụ quá trình triển khai, kiểm thử, trình bày và đánh giá hệ thống. Vì vậy, các tài nguyên chính **chưa được xóa tại thời điểm viết báo cáo**. Việc dọn dẹp sẽ được thực hiện sau khi workshop và quá trình đánh giá hoàn tất.

#### Kiểm soát chi phí trong thời gian duy trì hệ thống

- Tạo AWS Budget và cấu hình cảnh báo khi chi phí thực tế hoặc chi phí dự báo vượt ngưỡng cho phép.
- Theo dõi thường xuyên **Billing**, **Cost Explorer** và email cảnh báo chi phí.
- Chỉ bật các tài nguyên phục vụ kiểm thử trong khoảng thời gian cần thiết.
- Dừng EC2 ngoài thời gian sử dụng nếu việc dừng máy không ảnh hưởng đến bài trình bày hoặc quá trình kiểm thử.
- Sử dụng kích thước EC2 và RDS phù hợp với tải của môi trường workshop.
- Cấu hình thời gian lưu cho CloudWatch Logs để tránh lưu log không cần thiết trong thời gian dài.
- Không tạo thêm NAT Gateway, Elastic IP, Load Balancer, snapshot hoặc tài nguyên thử nghiệm khi không cần thiết.

> **Lưu ý:** Việc dừng EC2 không đồng nghĩa với việc ngừng toàn bộ chi phí. EBS volume, Elastic IP, NAT Gateway, Application Load Balancer, RDS và các dịch vụ liên quan vẫn có thể tiếp tục phát sinh chi phí.

#### Kế hoạch dọn dẹp sau khi hoàn thành dự án

Sau khi hệ thống không còn cần thiết cho việc trình bày và đánh giá, tài nguyên sẽ được dọn dẹp theo thứ tự sau để hạn chế lỗi do phụ thuộc giữa các dịch vụ:

1. Disable và xóa CloudFront distribution.
2. Xóa Application Load Balancer, listener và target group.
3. Terminate các EC2 instance; kiểm tra và xóa EBS volume không còn sử dụng.
4. Xóa RDS database; chỉ tạo final snapshot khi thực sự cần lưu dữ liệu và xóa các manual snapshot không còn cần thiết.
5. Xóa object, object version và delete marker trong S3 trước khi xóa bucket không còn sử dụng.
6. Xóa NAT Gateway, release Elastic IP và xóa VPC Endpoint.
7. Xóa route table tùy chỉnh, subnet, Internet Gateway, Security Group và cuối cùng là VPC.
8. Xóa CloudWatch alarm, log group, SNS topic/subscription và IAM role/policy tùy chỉnh chỉ dùng cho workshop.
9. Kiểm tra lại **Billing**, **Cost Explorer** và **Resource Explorer** để bảo đảm không còn tài nguyên ngoài dự kiến.

#### Tiêu chí hoàn thành

Quá trình dọn dẹp được xem là hoàn tất khi không còn EC2, RDS, NAT Gateway, Application Load Balancer, CloudFront distribution, Elastic IP, EBS volume hoặc S3 object không cần thiết. Do dữ liệu chi phí có thể cập nhật chậm, tài khoản sẽ tiếp tục được theo dõi trong 24–48 giờ sau khi dọn dẹp.
