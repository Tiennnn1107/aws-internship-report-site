---
title: "Tạo cảnh báo lỗi HTTP 5XX từ ALB Target"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.10.3. </b> "
---

### 5.10.3. Tạo cảnh báo lỗi HTTP 5XX từ ALB Target

CloudWatch Alarm này theo dõi số phản hồi HTTP 5XX do các target phía sau Application Load Balancer trả về. Khi xuất hiện lỗi server từ backend, alarm chuyển sang trạng thái **In alarm** và gửi thông báo qua SNS Topic.

#### Bước 1: Chọn metric HTTPCode_Target_5XX_Count

Truy cập **CloudWatch → Alarms → All alarms → Create alarm → Select metric**. Mở **ApplicationELB → Per AppELB Metrics**, tìm `HTTPCode_Target_5XX_Count` và chọn load balancer `recruit-alb`.

![Chọn metric lỗi ALB Target 5XX](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.3-Tao-CloudWatch-Alarm-cho-ALB-Target-5XX/chon-metric-alb-target-5xx.jpg>)

Metric này đếm các phản hồi 5XX do target tạo ra, chẳng hạn lỗi từ ứng dụng backend. Nó khác với `HTTPCode_ELB_5XX_Count`, là lỗi do chính load balancer tạo ra. Chọn **Select metric** để tiếp tục.

#### Bước 2: Cấu hình thống kê và ngưỡng lỗi

Trong phần cấu hình metric, chọn:

- **Namespace:** `AWS/ApplicationELB`.
- **Metric name:** `HTTPCode_Target_5XX_Count`.
- **Statistic:** `Sum`, cộng tổng số lỗi trong mỗi chu kỳ.
- **Period:** `5 minutes`.
- **Threshold type:** `Static`.
- **Condition:** `Greater/Equal` với ngưỡng `1`.

![Cấu hình ngưỡng lỗi ALB Target 5XX](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.3-Tao-CloudWatch-Alarm-cho-ALB-Target-5XX/cau-hinh-nguong-target-5xx.jpg>)

Với cấu hình này, chỉ cần có ít nhất một phản hồi 5XX trong 5 phút là điều kiện cảnh báo được thỏa mãn. Ngưỡng nhạy này phù hợp cho workshop và hệ thống có lưu lượng thấp; production có thể tăng ngưỡng hoặc dùng tỷ lệ lỗi để giảm cảnh báo do lỗi đơn lẻ.

#### Bước 3: Gửi cảnh báo đến SNS Topic

Tại **Configure actions**, chọn trạng thái kích hoạt **In alarm**, sau đó chọn **Select an existing SNS topic** và topic `recruitpro-alert-topic`.

![Chọn SNS Topic nhận cảnh báo Target 5XX](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.3-Tao-CloudWatch-Alarm-cho-ALB-Target-5XX/chon-sns-topic.jpg>)

Email endpoint hiển thị bên dưới xác nhận topic đã có người nhận. Khi alarm vượt ngưỡng, CloudWatch gửi sự kiện đến SNS và SNS chuyển tiếp thông báo qua email. Các hành động Lambda, Auto Scaling, EC2 và Systems Manager không được sử dụng trong bước này.

#### Bước 4: Đặt tên cho Alarm

Trong **Add alarm details**, đặt tên mô tả tài nguyên và loại lỗi, ví dụ `RecruitPro-ALB-Target-5XX`.

![Đặt tên CloudWatch Alarm cho ALB Target 5XX](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.3-Tao-CloudWatch-Alarm-cho-ALB-Target-5XX/dat-ten-alarm.jpg>)

Ảnh hiển thị thông báo **The alarm name already exists**, nghĩa là tài khoản đã có alarm cùng tên. CloudWatch không cho tạo hai alarm trùng tên trong cùng Region. Nếu đang tạo mới, cần dùng tên duy nhất như `RecruitPro-ALB-Target-5XX-v2`; nếu alarm cũ đã đúng cấu hình thì quay lại danh sách alarm và chỉnh sửa alarm đó thay vì tạo bản trùng lặp.

#### Bước 5: Kiểm tra và tạo Alarm

Tại **Preview and create**, kiểm tra lại metric, điều kiện, hành động và tên alarm.

![Kiểm tra cấu hình CloudWatch Alarm Target 5XX](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.3-Tao-CloudWatch-Alarm-cho-ALB-Target-5XX/xem-lai-va-tao-alarm.jpg>)

Màn hình Review xác nhận alarm dùng `HTTPCode_Target_5XX_Count`, `Sum`, chu kỳ 5 phút, điều kiện lớn hơn hoặc bằng 1 và gửi thông báo đến `recruitpro-alert-topic`. Sau khi bảo đảm tên alarm không bị trùng, chọn **Create alarm**. Alarm có thể tạm ở trạng thái **Insufficient data**, sau đó chuyển sang **OK** nếu không có lỗi hoặc **In alarm** khi xuất hiện Target 5XX.
