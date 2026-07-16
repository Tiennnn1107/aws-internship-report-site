---
title: "Tạo CloudWatch Alarm cho EC2 CPU"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.10.2. </b> "
---

### 5.10.2. Tạo cảnh báo CPU cao cho EC2 Backend

CloudWatch Alarm được cấu hình để theo dõi mức sử dụng CPU của EC2 Backend. Khi CPU trung bình vượt ngưỡng quy định, alarm chuyển sang trạng thái **In alarm** và gửi thông báo qua SNS Topic đã tạo ở mục 5.10.1.

#### Bước 1: Chọn metric CPUUtilization của EC2

Truy cập **CloudWatch → Alarms → All alarms → Create alarm**, sau đó chọn **Select metric**. Trong cửa sổ chọn metric, mở **EC2 → Per-Instance Metrics**, tìm `CPUUtilization` và chọn instance có tên `RecruitPro-BE`.

![Chọn metric CPUUtilization của EC2 RecruitPro-BE](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.2-Tao-CloudWatch-Alarm-cho-EC2-CPU/chon-metric-ec2-cpu.jpg>)

Biểu đồ trong hình hiển thị tỷ lệ CPU của instance theo thời gian. Việc chọn metric theo từng instance giúp alarm chỉ theo dõi EC2 Backend của RecruitPro, không gộp dữ liệu từ các EC2 khác. Chọn **Select metric** để tiếp tục.

#### Bước 2: Cấu hình thống kê và ngưỡng cảnh báo

Trong phần **Metric**, đặt:

- **Statistic:** `Average`, sử dụng mức CPU trung bình trong mỗi chu kỳ.
- **Period:** `5 minutes`, đánh giá dữ liệu theo từng khoảng 5 phút.

Trong phần **Conditions**, chọn **Static**, điều kiện **Greater** và đặt ngưỡng CPU là `80`.

![Cấu hình điều kiện cảnh báo CPU](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.2-Tao-CloudWatch-Alarm-cho-EC2-CPU/cau-hinh-nguong-cpu.jpg>)

Với cấu hình hoàn chỉnh được xác nhận ở màn hình Review, alarm sẽ theo dõi điều kiện **CPUUtilization > 80%**. Giá trị `10000` đang xuất hiện trong ảnh nhập liệu là giá trị tạm thời trước khi được sửa thành `80`, không phải ngưỡng sử dụng cuối cùng. Ngưỡng 80% giúp phát hiện EC2 chịu tải CPU cao kéo dài mà không tạo cảnh báo từ các dao động nhỏ thông thường.

Sau khi kiểm tra điều kiện, chọn **Next**.

#### Bước 3: Gửi cảnh báo đến SNS Topic

Tại bước **Configure actions**, chọn trạng thái kích hoạt là **In alarm**. Điều này có nghĩa hành động gửi thông báo chỉ được thực hiện khi metric vượt ngưỡng đã cấu hình.

![Chọn SNS Topic nhận cảnh báo CPU](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.2-Tao-CloudWatch-Alarm-cho-EC2-CPU/chon-sns-topic.jpg>)

Chọn **Select an existing SNS topic**, sau đó chọn `recruitpro-alert-topic`. Giao diện hiển thị email endpoint đã đăng ký với topic, xác nhận thông báo từ alarm sẽ được chuyển đến địa chỉ email này. Không cần thêm Lambda action hoặc Auto Scaling action trong phạm vi workshop. Chọn **Next** để tiếp tục.

#### Bước 4: Đặt tên cho CloudWatch Alarm

Trong phần **Add alarm details**, nhập tên alarm là `RecruitPro-EC2-High-CPU`.

![Đặt tên CloudWatch Alarm cho EC2 CPU](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.2-Tao-CloudWatch-Alarm-cho-EC2-CPU/dat-ten-alarm.jpg>)

Tên này thể hiện đầy đủ hệ thống, tài nguyên và tình trạng cần cảnh báo, giúp dễ tìm kiếm khi có nhiều alarm. Trường mô tả và Tags là tùy chọn; có thể bổ sung thông tin vận hành trong môi trường production. Chọn **Next** để đến bước kiểm tra cuối cùng.

#### Bước 5: Kiểm tra và tạo Alarm

Tại trang **Preview and create**, kiểm tra lại toàn bộ cấu hình trước khi tạo.

![Kiểm tra cấu hình và tạo CloudWatch Alarm](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.2-Tao-CloudWatch-Alarm-cho-EC2-CPU/xem-lai-va-tao-alarm.jpg>)

Ảnh xác nhận các thông số cuối cùng:

- **Namespace:** `AWS/EC2`.
- **Metric:** `CPUUtilization` của instance `RecruitPro-BE`.
- **Statistic:** `Average`.
- **Period:** `5 minutes`.
- **Condition:** CPU lớn hơn `80%`.
- **Action:** khi alarm ở trạng thái **In alarm**, gửi thông báo đến `recruitpro-alert-topic`.
- **Alarm name:** `RecruitPro-EC2-High-CPU`.

Nếu các thông tin đã chính xác, chọn **Create alarm**. Sau khi tạo, CloudWatch cần một khoảng thời gian thu thập dữ liệu; alarm có thể tạm thời ở trạng thái **Insufficient data** trước khi chuyển sang **OK** hoặc **In alarm**.
