---
title: "Kiểm tra upload CV lên S3"
date: 2026-07-10
weight: 4
chapter: false
pre: " <b> 5.7.4. </b> "
---

### 5.7.4. Kiểm tra upload CV lên S3

1. Đăng nhập bằng tài khoản ứng viên và mở trang hồ sơ.
2. Chọn file CV PDF hợp lệ, không vượt quá giới hạn dung lượng, rồi lưu hồ sơ.
3. Xác nhận ứng dụng thông báo upload thành công và một object đã mã hóa xuất hiện trong prefix của CV bucket.
4. Mở và tải CV thông qua ứng dụng để kiểm tra quyền đọc.
5. Thử file sai định dạng, file quá dung lượng và truy cập khi chưa đăng nhập. Hệ thống phải từ chối các yêu cầu này và không tạo object rác trên S3.

Bucket phải luôn ở trạng thái private. Backend truy cập S3 bằng IAM Role của EC2; không sử dụng public object URL.
