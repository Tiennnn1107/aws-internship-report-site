---
title: "Các dịch vụ AWS sử dụng trong hệ thống"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.3.3. </b> "
---

### 5.3.3. Các dịch vụ AWS sử dụng trong hệ thống

Hệ thống RecruitPro sử dụng các dịch vụ AWS để triển khai ứng dụng, lưu trữ dữ liệu, phân phối nội dung và giám sát vận hành.

```text
Route 53
    ↓ DNS
CloudFront ─────── S3 (frontend, CV và file tĩnh)
    ↓ origin
Application Load Balancer
    ↓
EC2 (Spring Boot backend)
    ↓
RDS MySQL

CloudWatch ── giám sát EC2, ALB, RDS
SNS ───────── gửi cảnh báo
IAM ───────── phân quyền truy cập AWS
VPC ───────── mạng riêng, subnet và Security Group
```

#### Bảng tổng hợp dịch vụ

| Dịch vụ | Vai trò trong hệ thống |
|---|---|
| Amazon VPC | Tạo mạng riêng cho toàn bộ hệ thống, gồm public subnet và private subnet. |
| Public/Private Subnet | ALB nằm ở public subnet; EC2 backend và RDS được đặt trong private subnet để hạn chế truy cập trực tiếp. |
| Security Group | Kiểm soát traffic giữa CloudFront/ALB, EC2 và RDS. |
| Amazon Route 53 | Quản lý DNS và trỏ tên miền đến CloudFront hoặc endpoint cần thiết. |
| Amazon CloudFront | Phân phối frontend, hình ảnh và file tĩnh từ edge location; chuyển tiếp API đến ALB. |
| Amazon S3 | Lưu frontend artifact, CV, hình ảnh và các file upload của người dùng. |
| Application Load Balancer | Nhận request từ CloudFront và phân phối đến EC2 backend healthy. |
| Amazon EC2 | Chạy ứng dụng Spring Boot backend và các service của hệ thống. |
| Amazon RDS for MySQL | Lưu users, companies, job postings, applications, interviews và blogs. |
| AWS IAM | Quản lý user, role và policy; cấp quyền tối thiểu cho EC2 truy cập S3. |
| Amazon CloudWatch | Thu thập log, metric và tạo alarm cho EC2, ALB và RDS. |
| Amazon SNS | Gửi email cảnh báo khi CloudWatch phát hiện chỉ số vượt ngưỡng. |

#### 1. Lớp mạng và bảo mật

Amazon VPC là lớp mạng chính của hệ thống. Internet Gateway cho phép các thành phần public như ALB nhận request từ bên ngoài. NAT Gateway cho phép EC2 trong private subnet truy cập Internet khi cần cập nhật package hoặc tải artifact, nhưng không mở EC2 trực tiếp ra Internet.

Security Group được cấu hình theo nguyên tắc chỉ mở đúng cổng cần thiết:

- ALB: nhận HTTPS/HTTP từ người dùng.
- EC2: chỉ nhận traffic ứng dụng từ Security Group của ALB.
- RDS: chỉ nhận MySQL port `3306` từ Security Group của EC2.
- SSH: chỉ cho phép từ địa chỉ quản trị được chỉ định, hoặc sử dụng Session Manager khi phù hợp.

#### 2. Lớp ứng dụng và dữ liệu

EC2 chạy backend Spring Boot, xử lý authentication, tuyển dụng, ứng tuyển và phỏng vấn. ALB thực hiện health check để chỉ gửi request đến instance hoạt động bình thường.

RDS MySQL cung cấp database có tính sẵn sàng và backup được quản lý bởi AWS. Database không nằm ở public subnet và chỉ được truy cập từ backend EC2.

S3 lưu trữ các file không phù hợp để lưu trực tiếp trong database như CV, ảnh đại diện và file deploy. Ứng dụng chỉ lưu URL hoặc object key trong MySQL.

#### 3. Lớp phân phối nội dung

CloudFront giúp giảm độ trễ khi người dùng tải frontend, JavaScript, CSS, hình ảnh và các tài nguyên tĩnh. Với API động, CloudFront chuyển tiếp request đến ALB và không cache dữ liệu cá nhân hoặc response cần xác thực.

Route 53 cung cấp DNS để người dùng truy cập hệ thống bằng tên miền dễ nhớ thay vì địa chỉ IP hoặc endpoint kỹ thuật.

#### 4. IAM và quản lý quyền

IAM Role được gắn cho EC2 để backend có thể truy cập đúng S3 bucket cần thiết. Không lưu access key cố định trong source code hoặc file public.

Các policy nên áp dụng quyền tối thiểu, ví dụ chỉ cho phép `s3:GetObject` và `s3:PutObject` trên bucket RecruitPro, thay vì cấp toàn quyền cho tất cả bucket.

#### 5. Giám sát và cảnh báo

CloudWatch theo dõi CPU, network, trạng thái target của ALB, CPU và storage của RDS, cũng như log ứng dụng. SNS nhận thông báo từ CloudWatch và gửi cảnh báo qua email khi có sự cố.

Các alarm tiêu biểu:

- EC2 CPU utilization cao.
- ALB có target unhealthy hoặc phát sinh nhiều lỗi 5XX.
- RDS CPU cao hoặc storage sắp đầy.
- Ứng dụng phát sinh nhiều lỗi trong log.

Nhờ kết hợp các dịch vụ trên, hệ thống có thể phân tách rõ mạng, ứng dụng, database, lưu trữ và monitoring; đồng thời dễ mở rộng và kiểm soát chi phí hơn.
