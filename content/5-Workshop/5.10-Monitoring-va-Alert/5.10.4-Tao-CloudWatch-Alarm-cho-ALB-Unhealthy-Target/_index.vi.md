---
title: "Tạo cảnh báo ALB có Target không khỏe mạnh"
date: 2026-07-10
weight: 4
chapter: false
pre: " <b> 5.10.4. </b> "
---

### 5.10.4. Tạo cảnh báo ALB có Target không khỏe mạnh

CloudWatch Alarm này theo dõi số target không vượt qua health check trong Target Group của Application Load Balancer. Khi có ít nhất một target không khỏe mạnh, hệ thống gửi cảnh báo qua SNS để người vận hành kiểm tra backend.

#### Bước 1: Chọn metric UnHealthyHostCount

Truy cập **CloudWatch → Alarms → All alarms → Create alarm → Select metric**. Mở **ApplicationELB → Per AppELB, per TG Metrics**, tìm `UnHealthyHostCount`, sau đó chọn đúng cặp `recruit-alb` và Target Group `recruit-tg`.

![Chọn metric UnHealthyHostCount của ALB và Target Group](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.4-Tao-CloudWatch-Alarm-cho-ALB-Unhealthy-Target/chon-metric-unhealthy-host.jpg>)

Metric này biểu thị số target bị ALB đánh giá là unhealthy. Trong biểu đồ, giá trị hiện tại bằng 0, nghĩa là các target vẫn vượt qua health check. Chọn **Select metric** để tiếp tục.

#### Bước 2: Cấu hình chu kỳ và ngưỡng cảnh báo

Cấu hình metric và điều kiện như sau:

- **Namespace:** `AWS/ApplicationELB`.
- **Metric name:** `UnHealthyHostCount`.
- **Statistic:** `Average`.
- **Period:** `1 minute`.
- **Threshold type:** `Static`.
- **Condition:** `Greater/Equal` với ngưỡng `1`.

![Cấu hình ngưỡng UnHealthyHostCount](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.4-Tao-CloudWatch-Alarm-cho-ALB-Unhealthy-Target/cau-hinh-nguong-unhealthy-host.jpg>)

Alarm sẽ thỏa điều kiện khi số target unhealthy trung bình trong một phút lớn hơn hoặc bằng 1. Chu kỳ ngắn giúp phát hiện nhanh backend gặp lỗi, nhưng production có thể yêu cầu nhiều datapoint liên tiếp để tránh cảnh báo do target khởi động lại trong thời gian ngắn.

#### Bước 3: Gửi cảnh báo đến SNS Topic

Tại **Configure actions**, chọn **In alarm**, sau đó chọn **Select an existing SNS topic** và `recruitpro-alert-topic`.

![Chọn SNS Topic nhận cảnh báo unhealthy target](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.4-Tao-CloudWatch-Alarm-cho-ALB-Unhealthy-Target/chon-sns-topic.jpg>)

Email endpoint hiển thị bên dưới cho biết topic đã có người nhận. Khi alarm chuyển sang **In alarm**, CloudWatch gửi sự kiện đến SNS và SNS chuyển tiếp thông báo qua email. Các action khác không cần cấu hình trong workshop.

#### Bước 4: Đặt tên cho Alarm

Trong **Add alarm details**, nhập tên `RecruitPro-ALB-Unhealthy-Target`.

![Đặt tên alarm cho ALB unhealthy target](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.4-Tao-CloudWatch-Alarm-cho-ALB-Unhealthy-Target/dat-ten-alarm.jpg>)

Tên này thể hiện hệ thống, tài nguyên được giám sát và trạng thái cảnh báo. Có thể bổ sung description hoặc tags trong production để ghi rõ Target Group, môi trường và người chịu trách nhiệm xử lý.

#### Bước 5: Kiểm tra và tạo Alarm

Tại **Preview and create**, kiểm tra lại toàn bộ cấu hình trước khi chọn **Create alarm**.

![Kiểm tra và tạo alarm ALB unhealthy target](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.4-Tao-CloudWatch-Alarm-cho-ALB-Unhealthy-Target/xem-lai-va-tao-alarm.jpg>)

Màn hình Review xác nhận metric `UnHealthyHostCount`, thống kê `Average`, chu kỳ 1 phút, điều kiện lớn hơn hoặc bằng 1 và notification đến `recruitpro-alert-topic`. Alarm có thể tạm ở trạng thái **Insufficient data**, sau đó chuyển sang **OK** khi mọi target khỏe mạnh hoặc **In alarm** khi có target không vượt qua health check.
