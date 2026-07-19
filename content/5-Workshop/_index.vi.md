---
title: "Workshop"
date: 2026-07-10
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

## Kết quả sau workshop

Người học triển khai end-to-end ứng dụng Spring Boot RecruitBox trên AWS theo mô hình CloudFront → ALB → EC2 → RDS, lưu CV/artifact trên S3 và giám sát bằng CloudWatch/SNS.

## Cách thực hiện

Thực hiện tuần tự từ 5.1 đến 5.12. Mỗi phần gồm mục tiêu, điều kiện đầu vào, thao tác trên AWS Console/CLI, kết quả mong đợi, kiểm thử và clean-up.

## Tiêu chí hoàn thành

- Kiến trúc và luồng request được giải thích; mỗi dịch vụ có lý do lựa chọn.
- EC2/RDS chạy trong private subnet; người dùng chỉ truy cập qua CloudFront/ALB.
- Log ứng dụng được tập trung; metric và alarm quan trọng gửi email qua SNS.
- Các kịch bản chức năng, lỗi và bảo mật cơ bản được kiểm thử.
- Có ước tính chi phí, nguyên tắc least privilege và quy trình xóa tài nguyên.

{{% notice warning %}}
NAT Gateway, ALB, RDS, EC2 và CloudFront có thể phát sinh chi phí. Hoàn tất mục 5.12 ngay sau khi thực hành.
{{% /notice %}}
