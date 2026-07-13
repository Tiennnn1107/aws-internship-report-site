---
title: "Worklog Tuần 4"
date: 2026-05-08
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

{{% notice warning %}}
 **Lưu ý:** Nội dung dưới đây ghi lại quá trình học tập và thực hành trong tuần. Thông tin được sử dụng cho mục đích báo cáo worklog cá nhân.
{{% /notice %}}

### Mục tiêu Tuần 4:

- Triển khai website tĩnh nhiều file trên Amazon S3.
- Thực hành Versioning, Cross-Region Replication và quản lý quyền truy cập object.
- Tạo CloudFormation stack và tìm hiểu quy trình AWS Backup, SNS notification.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 08/05/2026 | Tạo bucket `aws-first-cloud-journey-123456` tại `ap-southeast-1`; upload website gồm `index.html`, `error.html` và tài nguyên tĩnh. | 08/05/2026 | 08/05/2026 | AWS S3 console records |
| 09/05/2026 | Bật Static Website Hosting; điều chỉnh Block Public Access, tìm hiểu Object Ownership và ACL, rồi public object cần kiểm tra. | 09/05/2026 | 09/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 10/05/2026 | Kiểm tra website endpoint, phân tích lỗi 403 và xác minh `index.html`/`error.html`; tính tổng dung lượng object. | 10/05/2026 | 10/05/2026 | S3 website verification results |
| 11/05/2026 | Bật S3 Versioning và thực hành Cross-Region Replication từ `ap-southeast-1` sang `us-east-1`. | 11/05/2026 | 11/05/2026 | S3 replication configuration |
| 12/05/2026 | Lưu template hoặc artifact CloudFormation trên S3 và tạo CloudFormation stack. | 12/05/2026 | 12/05/2026 | CloudFormation stack events |
| 13/05/2026 – 14/05/2026 | Tìm hiểu Backup vault, Backup plan, Backup rule; cấu hình SNS notification và xác nhận email khi có yêu cầu. | 13/05/2026 | 14/05/2026 | AWS Backup and SNS console records |

### Kết quả đạt được Tuần 4:

- Xuất bản và kiểm tra được website tĩnh nhiều file trên S3.
- Hiểu ảnh hưởng của Block Public Access, Object Ownership, ACL và cách xử lý lỗi 403.
- Bật Versioning, kiểm tra dung lượng object và cấu hình Cross-Region Replication.
- Tạo được CloudFormation stack từ template/artifact lưu trên S3.
- Nắm quy trình cấu hình Backup vault, Backup plan, Backup rule và SNS notification.
