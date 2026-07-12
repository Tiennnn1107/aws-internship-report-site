---
title: "Kiểm thử hệ thống"
date: 2026-07-10
weight: 11
chapter: false
pre: " <b> 5.11. </b> "
---

## Điều kiện kiểm thử

CloudFront, ALB target, EC2 service và RDS đều healthy; dùng dữ liệu giả, không dùng CV hoặc thông tin cá nhân thật.

## Ma trận end-to-end

| Kịch bản | Thao tác | Kết quả mong đợi | Bằng chứng |
|---|---|---|---|
| Đăng ký/đăng nhập | Tạo tài khoản rồi đăng nhập | HTTP 2xx, token/session hợp lệ | Screenshot + application log |
| Danh sách việc làm | Gọi trang/API qua CloudFront | Dữ liệu đúng, không lỗi CORS | DevTools network + ALB metric |
| Cập nhật hồ sơ | Sửa trường hợp lệ/không hợp lệ | Lưu thành công hoặc 4xx rõ ràng | DB record + log correlation ID |
| Upload CV | Upload PDF hợp lệ và file sai loại | S3 object mã hóa; file sai bị chặn | S3 metadata + app log |
| Mất DB | Tạm chặn kết nối trong môi trường test | API trả lỗi kiểm soát, không lộ secret | 5xx metric + alarm email |
| Target unhealthy | Dừng service ngắn hạn | ALB đánh dấu unhealthy và alarm | Target health + SNS email |

## Đo lường

Chạy một lượng request có kiểm soát, ghi p50/p95 response time, error rate, CPU, DB connections và CloudFront cache hit rate. Sau test phải đưa cấu hình về trạng thái bình thường và xác nhận alarm trở lại `OK`.
