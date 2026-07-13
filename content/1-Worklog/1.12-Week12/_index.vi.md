---
title: "Worklog Tuần 12"
date: 2026-07-03
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

{{% notice warning %}}
 **Lưu ý:** Nội dung dưới đây ghi lại quá trình học tập và thực hành trong tuần. Thông tin được sử dụng cho mục đích báo cáo worklog cá nhân.
{{% /notice %}}

### Mục tiêu Tuần 12:

- Kiểm thử toàn bộ RecruitPro qua các lớp ứng dụng và hạ tầng AWS.
- Khắc phục các lỗi còn lại và hoàn thiện Proposal, Workshop, Worklog song ngữ.
- Tổng kết kiến trúc, rủi ro, chi phí, hướng phát triển và dọn tài nguyên thử nghiệm.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 03/07/2026 – 04/07/2026 | Kiểm thử đăng ký, đăng nhập, phân quyền candidate/recruiter/admin, danh sách việc làm, profile và upload CV. | 03/07/2026 | 04/07/2026 | Kết quả kiểm thử RecruitPro |
| 05/07/2026 | Đối chiếu dữ liệu RDS, object CV trên S3 và truy cập qua ALB/CloudFront. | 05/07/2026 | 05/07/2026 | RDS, S3, ALB and CloudFront checks |
| 06/07/2026 | Xử lý JWT secret Base64, CORS CloudFront, IAM S3 `AccessDenied`, kết nối RDS, CloudFront 403 và lỗi systemd service mà không ghi secret. | 06/07/2026 | 06/07/2026 | Application and infrastructure logs |
| 07/07/2026 | Hoàn thiện sơ đồ kiến trúc, đánh số và mô tả luồng; chụp màn hình các dịch vụ AWS đã triển khai. | 07/07/2026 | 07/07/2026 | Sơ đồ và ảnh chụp triển khai |
| 08/07/2026 – 09/07/2026 | Viết Proposal RecruitBox, Workshop và Worklog bằng tiếng Việt/Anh; tổng kết VPC, EC2, RDS, S3, IAM, ALB, CloudFront, CloudWatch, SNS và Systems Manager. | 08/07/2026 | 09/07/2026 | Nội dung báo cáo trong repository |
| 10/07/2026 | Viết rủi ro, chi phí và hướng tương lai; ghi rõ Route 53/ACM, Auto Scaling, CI/CD, Cognito và pipeline xử lý CV chưa triển khai.<br>&emsp;Dọn tài nguyên thử nghiệm để tránh chi phí. | 10/07/2026 | 10/07/2026 | Bảng chi phí và checklist dọn tài nguyên |

### Kết quả đạt được Tuần 12:

- Hoàn thành kiểm thử chức năng, phân quyền, RDS, S3, ALB và CloudFront.
- Khắc phục các lỗi JWT, CORS, IAM, RDS, CloudFront và systemd mà không lộ thông tin nhạy cảm.
- Hoàn thiện sơ đồ kiến trúc và báo cáo Proposal, Workshop, Worklog song ngữ.
- Tổng kết chính xác các dịch vụ đã triển khai: VPC, EC2, RDS, S3, IAM, ALB, CloudFront, CloudWatch, SNS và Systems Manager.
- Đánh dấu Route 53/ACM, Auto Scaling, CI/CD, Cognito và pipeline xử lý CV là hướng tương lai chưa triển khai.
- Dọn dẹp tài nguyên thử nghiệm không còn cần thiết để hạn chế phát sinh chi phí.
