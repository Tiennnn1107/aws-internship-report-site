---
title: "Worklog Tuần 9"
date: 2026-06-12
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

{{% notice warning %}}
 **Lưu ý:** Nội dung dưới đây ghi lại quá trình học tập và thực hành trong tuần. Thông tin được sử dụng cho mục đích báo cáo worklog cá nhân.
{{% /notice %}}

### Mục tiêu Tuần 9:

- Thiết lập S3 riêng tư cho CV, artifact triển khai và bản sao lưu database khi cần.
- Cấp quyền S3 tối thiểu cho EC2 Role và triển khai JAR từ S3.
- Tích hợp upload CV bằng AWS SDK for Java và xử lý lỗi quyền truy cập.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 12/06/2026 | Tạo `recruitpro-cv-storage-tien`, `recruitpro-deploy-artifacts-tien` và ghi nhận `recruitpro-db-backup-tien` cho bản sao lưu database. | 12/06/2026 | 12/06/2026 | S3 bucket records |
| 13/06/2026 | Bật Block Public Access và encryption; xác minh bucket CV không cho truy cập công khai. | 13/06/2026 | 13/06/2026 | S3 security configuration |
| 14/06/2026 | Tạo IAM Policy giới hạn `s3:ListBucket`, `s3:GetObject`, `s3:PutObject`, `s3:DeleteObject`; gắn vào EC2 Role. | 14/06/2026 | 14/06/2026 | IAM policy records |
| 15/06/2026 | Upload JAR vào bucket artifact; để EC2 tải JAR từ S3 và triển khai lại service. | 15/06/2026 | 15/06/2026 | S3 and EC2 deployment logs |
| 16/06/2026 – 17/06/2026 | Cấu hình Spring Boot dùng AWS SDK for Java để upload CV vào prefix `cv/`; tạo presigned URL hoặc API xem file. | 16/06/2026 | 17/06/2026 | RecruitPro source and application logs |
| 18/06/2026 | Xử lý lỗi 403 `HeadObject` và `AccessDenied`; kiểm tra object CV đã xuất hiện trong S3. | 18/06/2026 | 18/06/2026 | S3 object and error verification |

### Kết quả đạt được Tuần 9:

- Tạo đúng các bucket CV, deploy artifact và backup database theo kế hoạch.
- Giữ bucket CV riêng tư bằng Block Public Access và encryption.
- Áp dụng quyền S3 tối thiểu cho EC2 Role và triển khai JAR từ bucket artifact.
- Upload CV vào prefix `cv/` và cung cấp quyền xem có thời hạn qua presigned URL hoặc API.
- Khắc phục lỗi `HeadObject`/`AccessDenied` bằng cách rà soát resource ARN, action và IAM Role.
