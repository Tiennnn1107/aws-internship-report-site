---
title: "Tạo cảnh báo CPU cao cho Amazon RDS"
date: 2026-07-10
weight: 5
chapter: false
pre: " <b> 5.10.5. </b> "
---

### 5.10.5. Tạo cảnh báo CPU cao cho Amazon RDS

CloudWatch Alarm này theo dõi mức sử dụng CPU của RDS database. Khi CPU trung bình của `recruitpro-db` vượt 80%, hệ thống gửi cảnh báo qua SNS để người vận hành kiểm tra truy vấn, số kết nối và tải của database.

#### Bước 1: Chọn metric CPUUtilization của RDS

Truy cập **CloudWatch → Alarms → All alarms → Create alarm → Select metric**. Mở **RDS → DBInstanceIdentifier**, tìm `CPUUtilization` và chọn DB instance `recruitpro-db`.

![Chọn metric CPUUtilization của RDS recruitpro-db](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.5-Tao-CloudWatch-Alarm-cho-RDS-CPU/chon-metric-rds-cpu.jpg>)

Biểu đồ hiển thị phần trăm CPU của database theo thời gian; trong ảnh, mức sử dụng chỉ dao động khoảng 3–6%. Chọn metric theo DB instance giúp alarm chỉ giám sát đúng database của hệ thống. Chọn **Select metric** để tiếp tục.

#### Bước 2: Cấu hình chu kỳ và ngưỡng CPU

Cấu hình metric và điều kiện như sau:

- **Namespace:** `AWS/RDS`.
- **Metric name:** `CPUUtilization`.
- **DBInstanceIdentifier:** `recruitpro-db`.
- **Statistic:** `Average`.
- **Period:** `5 minutes`.
- **Threshold type:** `Static`.
- **Condition:** `Greater` với ngưỡng `80`.

![Cấu hình ngưỡng CPU cho RDS](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.5-Tao-CloudWatch-Alarm-cho-RDS-CPU/cau-hinh-nguong-rds-cpu.jpg>)

Alarm thỏa điều kiện khi CPU trung bình trong 5 phút lớn hơn 80%. Ngưỡng này giúp phát hiện tải CPU cao kéo dài thay vì các đỉnh ngắn. Nếu cảnh báo xảy ra thường xuyên, cần kiểm tra slow query, connection pool, index và kích thước DB instance.

#### Bước 3: Gửi cảnh báo đến SNS Topic

Tại **Configure actions**, chọn trạng thái **In alarm**, sau đó chọn **Select an existing SNS topic** và `recruitpro-alert-topic`.

![Chọn SNS Topic nhận cảnh báo CPU RDS](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.5-Tao-CloudWatch-Alarm-cho-RDS-CPU/chon-sns-topic.jpg>)

Email endpoint hiển thị bên dưới xác nhận topic đã có người nhận. Khi CPU vượt ngưỡng, CloudWatch gửi sự kiện đến SNS và SNS chuyển tiếp thông báo qua email. Không cần cấu hình các action khác trong workshop.

#### Bước 4: Đặt tên cho Alarm

Trong **Add alarm details**, nhập tên `RecruitPro-RDS-High-CPU`.

![Đặt tên CloudWatch Alarm CPU cao cho RDS](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.5-Tao-CloudWatch-Alarm-cho-RDS-CPU/dat-ten-alarm.jpg>)

Tên alarm thể hiện rõ hệ thống, loại tài nguyên và tình trạng cần cảnh báo. Có thể bổ sung description và tags trong production để ghi môi trường, mức độ ưu tiên và người chịu trách nhiệm xử lý.

#### Bước 5: Kiểm tra và tạo Alarm

Tại **Preview and create**, kiểm tra lại cấu hình rồi chọn **Create alarm**.

![Kiểm tra và tạo CloudWatch Alarm CPU RDS](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.5-Tao-CloudWatch-Alarm-cho-RDS-CPU/xem-lai-va-tao-alarm.jpg>)

Màn hình Review xác nhận metric `CPUUtilization` của `recruitpro-db`, thống kê `Average`, chu kỳ 5 phút, điều kiện CPU lớn hơn 80% và notification đến `recruitpro-alert-topic`. Alarm có thể tạm ở trạng thái **Insufficient data**, sau đó chuyển sang **OK** hoặc **In alarm** tùy dữ liệu CPU.
