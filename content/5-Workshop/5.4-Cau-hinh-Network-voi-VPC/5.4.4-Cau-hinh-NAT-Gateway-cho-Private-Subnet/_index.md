---
title: "Configure a NAT Gateway for the Private Subnet"
date: 2026-07-10
weight: 4
chapter: false
pre: " <b> 5.4.4. </b> "
---

### 5.4.4. Configure a NAT Gateway for the Private Subnet

1. Open **VPC → NAT gateways → Create NAT gateway**.
2. Enter `Recruit-nat-1a`, choose `public-alb-1a`, and select `Public` connectivity.
3. Allocate an Elastic IP and create the NAT Gateway.
4. Wait until its state changes from `Pending` to `Available`.

{{% notice note %}}
A NAT Gateway incurs hourly and data-processing charges. One NAT Gateway is sufficient for this workshop; production environments should consider one per AZ for higher availability.
{{% /notice %}}

Verify that the NAT Gateway is in a public subnet, has an Elastic IP, and is `Available`.

![Cấu hình NAT Gateway](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.4-Cau-hinh-NAT-Gateway-cho-Private-Subnet/NAT.png>)
![NAT Gateway hoạt động](</images/5-Workshop/5.4-Cau-hinh-Network-voi-VPC/5.4.4-Cau-hinh-NAT-Gateway-cho-Private-Subnet/nat%202.png>)
