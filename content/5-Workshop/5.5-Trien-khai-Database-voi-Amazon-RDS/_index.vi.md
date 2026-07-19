---
title: "Triển khai Database với Amazon RDS"
date: 2026-07-10
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

## 5.5. Triển khai Database với Amazon RDS

Phần này triển khai MySQL trên Amazon RDS trong private database subnet. Kết nối được giới hạn chỉ từ Security Group của EC2 backend. Sau khi tạo database, backend sẽ kết nối đến RDS và import schema cùng dữ liệu mẫu của RecruitPro.
