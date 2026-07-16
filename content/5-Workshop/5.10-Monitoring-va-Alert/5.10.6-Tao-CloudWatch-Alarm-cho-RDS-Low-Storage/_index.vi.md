---
title: "Tạo cảnh báo dung lượng lưu trữ RDS sắp hết"
date: 2026-07-10
weight: 6
chapter: false
pre: " <b> 5.10.6. </b> "
---

### 5.10.6. Tạo cảnh báo dung lượng lưu trữ RDS sắp hết

CloudWatch Alarm này theo dõi dung lượng lưu trữ còn trống của RDS. Khi `recruitpro-db` còn dưới 1 GB, hệ thống gửi cảnh báo qua SNS để người vận hành dọn dữ liệu, tăng storage hoặc kiểm tra tốc độ tăng trưởng database trước khi hết dung lượng.

#### Bước 1: Chọn metric FreeStorageSpace

Truy cập **CloudWatch → Alarms → All alarms → Create alarm → Select metric**. Mở **RDS → DBInstanceIdentifier**, tìm `FreeStorageSpace` và chọn DB instance `recruitpro-db`.

![Chọn metric FreeStorageSpace của RDS](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.6-Tao-CloudWatch-Alarm-cho-RDS-Low-Storage/chon-metric-free-storage-space.jpg>)

Metric này đo số byte lưu trữ còn trống. Biểu đồ trong ảnh cho thấy database còn khoảng 19,5 GB, cao hơn nhiều so với ngưỡng cảnh báo. Chọn **Select metric** để tiếp tục.

#### Bước 2: Cấu hình chu kỳ và ngưỡng dung lượng

Cấu hình metric và điều kiện như sau:

- **Namespace:** `AWS/RDS`.
- **Metric name:** `FreeStorageSpace`.
- **DBInstanceIdentifier:** `recruitpro-db`.
- **Statistic:** `Average`.
- **Period:** `5 minutes`.
- **Threshold type:** `Static`.
- **Condition:** `Lower` với ngưỡng `1000000000` bytes.

![Cấu hình ngưỡng dung lượng trống RDS](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.6-Tao-CloudWatch-Alarm-cho-RDS-Low-Storage/cau-hinh-nguong-low-storage.jpg>)

Giá trị `1,000,000,000` bytes tương đương 1 GB theo đơn vị thập phân, khoảng 0,93 GiB. Điều kiện phải là **Lower** vì dung lượng trống càng giảm thì rủi ro càng cao. Ngưỡng 1 GB phù hợp cho workshop; production nên chọn ngưỡng lớn hơn theo dung lượng cấp phát và tốc độ tăng dữ liệu.

#### Bước 3: Gửi cảnh báo đến SNS Topic

Tại **Configure actions**, chọn **In alarm**, sau đó chọn **Select an existing SNS topic** và `recruitpro-alert-topic`.

![Chọn SNS Topic nhận cảnh báo dung lượng RDS](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.6-Tao-CloudWatch-Alarm-cho-RDS-Low-Storage/chon-sns-topic.jpg>)

Email endpoint hiển thị bên dưới xác nhận topic đã có người nhận. Khi dung lượng trống thấp hơn ngưỡng, CloudWatch gửi sự kiện đến SNS và SNS chuyển tiếp cảnh báo qua email.

#### Bước 4: Đặt tên cho Alarm

Trong **Add alarm details**, nhập tên `RecruitPro-RDS-Low-Storage`.

![Đặt tên CloudWatch Alarm dung lượng RDS thấp](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.6-Tao-CloudWatch-Alarm-cho-RDS-Low-Storage/dat-ten-alarm.jpg>)

Tên này thể hiện rõ database và tình trạng cần cảnh báo. Trong production, có thể thêm description và tags để ghi ngưỡng, môi trường và quy trình xử lý khi storage sắp hết.

#### Bước 5: Kiểm tra và tạo Alarm

Tại **Preview and create**, kiểm tra lại cấu hình rồi chọn **Create alarm**.

![Kiểm tra và tạo CloudWatch Alarm dung lượng RDS](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.6-Tao-CloudWatch-Alarm-cho-RDS-Low-Storage/xem-lai-va-tao-alarm.jpg>)

Màn hình Review xác nhận metric `FreeStorageSpace` của `recruitpro-db`, thống kê `Average`, chu kỳ 5 phút, điều kiện thấp hơn `1,000,000,000` bytes và notification đến `recruitpro-alert-topic`. Alarm chuyển sang **OK** khi dung lượng còn đủ và **In alarm** khi dung lượng trống giảm dưới ngưỡng.
