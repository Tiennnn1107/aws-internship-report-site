---
title: "Tạo SNS Topic gửi email cảnh báo"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.10.1. </b> "
---

### 5.10.1. Tạo SNS Topic gửi email cảnh báo

Amazon Simple Notification Service (SNS) được sử dụng làm kênh nhận thông báo từ các CloudWatch Alarm. Khi một chỉ số vượt ngưỡng cảnh báo, CloudWatch gửi thông báo đến SNS Topic và SNS tiếp tục chuyển thông báo đến địa chỉ email đã đăng ký.

## Bước 1: Tạo SNS Topic

Tại AWS Management Console, chọn Region **Asia Pacific (Singapore)** (`ap-southeast-1`), sau đó truy cập **Amazon SNS → Topics → Create topic**.

![Tạo SNS Standard Topic](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.1-Tao-SNS-Topic-gui-email-canh-bao/create1.jpg>)

Trong phần **Details**, cấu hình:

- **Type:** chọn `Standard` vì loại này hỗ trợ giao thức Email và phù hợp để gửi cảnh báo CloudWatch. Không chọn FIFO vì FIFO chủ yếu phục vụ các hệ thống cần bảo toàn thứ tự và chống trùng lặp thông điệp.
- **Name:** nhập `recruitpro-alert-topic` để nhận diện đây là topic cảnh báo của hệ thống RecruitPro.
- **Display name:** có thể để trống vì trường này chủ yếu được sử dụng cho SMS.

Các phần Encryption, Access policy, Delivery policy và Delivery status logging có thể giữ cấu hình mặc định trong phạm vi workshop. Sau đó cuộn xuống cuối trang và chọn **Create topic**.

## Bước 2: Tạo Email Subscription

Sau khi topic được tạo, mở topic `recruitpro-alert-topic`, chọn **Create subscription** và khai báo endpoint nhận cảnh báo.

![Tạo Email Subscription cho SNS Topic](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.1-Tao-SNS-Topic-gui-email-canh-bao/create2.jpg>)

Cấu hình subscription như sau:

- **Topic ARN:** chọn ARN của `recruitpro-alert-topic` tại Region `ap-southeast-1`.
- **Protocol:** chọn `Email`.
- **Endpoint:** nhập địa chỉ email sẽ nhận cảnh báo.

Không cần cấu hình **Subscription filter policy** hoặc **Redrive policy** cho trường hợp gửi cảnh báo email cơ bản. Chọn **Create subscription** để gửi yêu cầu xác nhận đến địa chỉ email vừa nhập.

## Bước 3: Xác nhận đăng ký trong email

SNS chưa gửi cảnh báo đến endpoint ngay sau khi tạo subscription. Người sở hữu email phải xác nhận đăng ký để tránh việc một địa chỉ bị thêm vào topic khi chưa đồng ý.

![Email xác nhận đăng ký Amazon SNS](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.1-Tao-SNS-Topic-gui-email-canh-bao/cfmail.jpg>)

Mở email có tiêu đề **AWS Notification - Subscription Confirmation** từ `no-reply@sns.amazonaws.com`, sau đó chọn liên kết **Confirm subscription**. Nếu không thấy email trong hộp thư đến, cần kiểm tra thêm thư mục Spam hoặc Thư rác như trong hình.

## Bước 4: Kiểm tra trạng thái Subscription

Quay lại trang chi tiết topic `recruitpro-alert-topic` và mở thẻ **Subscriptions** để xác minh kết quả.

![Email Subscription đã được xác nhận](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.1-Tao-SNS-Topic-gui-email-canh-bao/surbartion.jpg>)

Subscription trong hình sử dụng giao thức **EMAIL** và có trạng thái **Confirmed**. Trạng thái này xác nhận địa chỉ email đã đăng ký thành công và SNS có thể gửi thông báo đến endpoint. Topic này sẽ được chọn làm notification target khi cấu hình các CloudWatch Alarm ở những bước tiếp theo.
