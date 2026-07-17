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
| Hồ sơ ứng viên và CV | Cập nhật thông tin, tải PDF lên rồi mở/tải xuống CV | Thông tin được lưu; CV có thể xem và tải xuống | Trang hồ sơ + nội dung CV |
| Mất DB | Tạm chặn kết nối trong môi trường test | API trả lỗi kiểm soát, không lộ secret | 5xx metric + alarm email |
| Target unhealthy | Dừng service ngắn hạn | ALB đánh dấu unhealthy và alarm | Target health + SNS email |

## Đo lường

Chạy một lượng request có kiểm soát, ghi p50/p95 response time, error rate, CPU, DB connections và CloudFront cache hit rate. Sau test phải đưa cấu hình về trạng thái bình thường và xác nhận alarm trở lại `OK`.
