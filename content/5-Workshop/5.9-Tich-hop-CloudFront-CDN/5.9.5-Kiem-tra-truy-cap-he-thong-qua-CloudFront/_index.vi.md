---
title: "Xác nhận CloudFront Distribution hoạt động"
date: 2026-07-10
weight: 5
chapter: false
pre: " <b> 5.9.5. </b> "
---

## 5.9.5. Xác nhận CloudFront Distribution hoạt động

Sau khi hoàn tất các bước cấu hình và tạo distribution, quay lại danh sách **CloudFront → Distributions** để kiểm tra kết quả.

![CloudFront Distribution đã được kích hoạt](</images/5-Workshop/5.9-Tich-hop-CloudFront-CDN/5.9.5-Kiem-tra-truy-cap-he-thong-qua-CloudFront/cloudfront%205.png>)

Trong hình, distribution có ID `E2QU9OGDR59GT0` đã ở trạng thái **Enabled**, loại **Standard**, sử dụng gói **Free** và origin là `recruit-alb-1002681411`. CloudFront cũng đã cấp một **Domain name** mặc định bắt đầu bằng `d32l...`; đây là địa chỉ dùng để gửi request qua mạng CDN đến ALB.

Trạng thái **Enabled** xác nhận distribution đã được kích hoạt. Bước kiểm thử truy cập thực tế cần mở domain CloudFront được cấp và xác nhận ứng dụng phản hồi bình thường; riêng ảnh này chỉ chứng minh distribution đã tồn tại và đang bật, không thể hiện kết quả đăng nhập, CORS hay cache hit.
