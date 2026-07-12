---
title: "Cấu hình NAT Gateway cho Private Subnet"
date: 2026-07-10
weight: 4
chapter: false
pre: " <b> 5.4.4. </b> "
---

## Các bước chi tiết

1. Vào **VPC → NAT gateways → Create NAT gateway**.
2. Nhập `Recruit-nat-1a`, chọn subnet `public-alb-1a`, connectivity type `Public`.
3. Chọn **Allocate Elastic IP**, sau đó **Create NAT gateway**.

![Cấu hình NAT Gateway](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.4-Cau-hinh-NAT-Gateway-cho-Private-Subnet/NAT.png>)

4. Chờ trạng thái chuyển từ `Pending` sang `Available`.

![NAT Gateway hoạt động](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.4-Cau-hinh-NAT-Gateway-cho-Private-Subnet/nat%202.png>)

{{% notice note %}}
NAT Gateway phát sinh chi phí theo giờ và lưu lượng. Có thể dùng một NAT cho workshop; production nên cân nhắc một NAT mỗi AZ để tăng tính sẵn sàng.
{{% /notice %}}

## Xác minh

NAT Gateway ở public subnet, có Elastic IP và trạng thái `Available`.
