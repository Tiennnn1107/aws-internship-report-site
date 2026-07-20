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

![Chọn file CV PDF từ máy tính để upload](</images/5-Workshop/5.7-Luu-tru-file-voi-Amazon-S3/5.7.4-Kiem-tra-upload-CV-len-S3/chon-file-cv-pdf.jpg>)

3. Xác nhận ứng dụng thông báo upload thành công và một object đã mã hóa xuất hiện trong prefix của CV bucket.

![Các file CV đã được upload vào prefix cv trên Amazon S3](</images/5-Workshop/5.7-Luu-tru-file-voi-Amazon-S3/5.7.4-Kiem-tra-upload-CV-len-S3/kiem-tra-cv-tren-s3.jpg>)

4. Mở và tải CV thông qua ứng dụng để kiểm tra quyền đọc.

![CV được hiển thị thành công trong hồ sơ ứng viên](</images/5-Workshop/5.7-Luu-tru-file-voi-Amazon-S3/5.7.4-Kiem-tra-upload-CV-len-S3/hien-thi-cv-tren-ho-so.jpg>)

![Mở file CV từ Amazon S3 thông qua URL có chữ ký tạm thời](</images/5-Workshop/5.7-Luu-tru-file-voi-Amazon-S3/5.7.4-Kiem-tra-upload-CV-len-S3/mo-cv-tu-s3-qua-ung-dung.jpg>)

5. Thử file sai định dạng, file quá dung lượng và truy cập khi chưa đăng nhập. Hệ thống phải từ chối các yêu cầu này và không tạo object rác trên S3.

Bucket phải luôn ở trạng thái private. Backend truy cập S3 bằng IAM Role của EC2; không sử dụng public object URL.

![Amazon S3 từ chối truy cập CV trực tiếp bằng URL công khai](</images/5-Workshop/5.7-Luu-tru-file-voi-Amazon-S3/5.7.4-Kiem-tra-upload-CV-len-S3/tu-choi-truy-cap-cong-khai-cv-s3.jpg>)
