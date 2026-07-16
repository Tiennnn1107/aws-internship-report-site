---
title: "Tổng kết các dịch vụ AWS đã sử dụng"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.12.1. </b> "
---

### 5.12.1. Tổng kết các dịch vụ AWS đã sử dụng

Workshop đã triển khai RecruitPro theo kiến trúc nhiều lớp trên AWS. Mỗi dịch vụ đảm nhiệm một vai trò riêng trong mạng, ứng dụng, dữ liệu, lưu trữ, phân phối nội dung và giám sát. Cách phân tách này giúp hệ thống dễ quản lý, bảo mật và mở rộng hơn so với việc đặt toàn bộ thành phần trên một máy chủ public.

#### Kiến trúc sau khi hoàn thành

```text
Người dùng
    │
    ▼
Amazon CloudFront
    │
    ▼
Application Load Balancer (public subnet)
    │
    ▼
Amazon EC2 - Spring Boot (private subnet)
    ├────────► Amazon RDS for MySQL (private subnet)
    └────────► Amazon S3 (CV và deployment artifact)

Amazon CloudWatch ──► Amazon SNS ──► Email cảnh báo
AWS IAM ────────────► cấp quyền EC2 truy cập S3
```

CloudFront đang sử dụng domain mặc định do AWS cấp. Route 53 và ACM chưa được cấu hình trong workshop này nên không được tính vào danh sách dịch vụ đã triển khai.

#### Lớp mạng và kết nối

| Thành phần | Vai trò đã triển khai |
|---|---|
| Amazon VPC | Tạo mạng riêng và cô lập tài nguyên của RecruitPro. |
| Public Subnet | Đặt ALB, NAT Gateway và các thành phần cần kết nối Internet trực tiếp. |
| Private Subnet | Đặt EC2 Backend và RDS, hạn chế truy cập trực tiếp từ Internet. |
| Internet Gateway | Cung cấp đường truyền Internet cho các public subnet. |
| NAT Gateway | Cho phép EC2 trong private subnet tải package và artifact mà không cần public IP. |
| Route Table | Điều hướng traffic giữa subnet, Internet Gateway, NAT Gateway và S3 Endpoint. |
| Security Group | Chỉ cho phép traffic cần thiết giữa ALB, EC2 và RDS. |
| S3 Gateway Endpoint | Cho phép private subnet truy cập S3 qua mạng AWS mà không đi qua NAT Gateway. |

Thiết kế mạng bảo đảm người dùng chỉ tiếp cận ALB. EC2 nhận request ứng dụng từ Security Group của ALB, còn RDS chỉ mở cổng MySQL `3306` cho Security Group của EC2.

#### Lớp ứng dụng và dữ liệu

| Dịch vụ | Vai trò đã triển khai |
|---|---|
| Amazon EC2 | Chạy backend Spring Boot của RecruitPro dưới dạng `systemd` service. |
| Application Load Balancer | Cung cấp endpoint public, thực hiện health check và chuyển request đến EC2 healthy. |
| Target Group | Đăng ký EC2 Backend và xác định cổng, giao thức cùng đường dẫn health check. |
| Amazon RDS for MySQL | Lưu dữ liệu người dùng, nhà tuyển dụng, công việc, hồ sơ ứng tuyển và các dữ liệu nghiệp vụ. |
| Amazon S3 | Lưu CV của ứng viên và file JAR dùng để triển khai backend. |

Việc tách file khỏi database giúp RDS chỉ quản lý dữ liệu có cấu trúc. Ứng dụng lưu object key hoặc URL của file S3 thay vì lưu dữ liệu nhị phân trực tiếp trong MySQL.

#### Phân phối nội dung và bảo mật truy cập

| Dịch vụ | Vai trò đã triển khai |
|---|---|
| Amazon CloudFront | Cung cấp domain CDN và chuyển request của người dùng đến ALB origin. |
| AWS IAM | Cấp IAM Role và policy cho EC2 truy cập đúng S3 bucket cần thiết. |

CloudFront được cấu hình cho ứng dụng động với đầy đủ HTTP method, `CachingDisabled` và origin request policy phù hợp. IAM Role giúp ứng dụng truy cập S3 mà không phải lưu access key cố định trong source code hoặc trên EC2.

#### Giám sát và cảnh báo

| Dịch vụ | Vai trò đã triển khai |
|---|---|
| Amazon CloudWatch | Thu thập metric và tạo alarm cho EC2, ALB và RDS. |
| Amazon SNS | Nhận sự kiện từ CloudWatch Alarm và gửi thông báo đến email đã xác nhận. |

Các alarm đã cấu hình gồm:

- EC2 `CPUUtilization > 80%` trong chu kỳ 5 phút.
- ALB `HTTPCode_Target_5XX_Count >= 1` trong chu kỳ 5 phút.
- ALB `UnHealthyHostCount >= 1` trong chu kỳ 1 phút.
- RDS `CPUUtilization > 80%` trong chu kỳ 5 phút.
- RDS `FreeStorageSpace < 1,000,000,000 bytes` trong chu kỳ 5 phút.

#### Kết quả đạt được

Sau workshop, RecruitPro có một luồng truy cập hoàn chỉnh từ CloudFront đến ALB, EC2 và RDS; file được lưu riêng trên S3; tài nguyên backend nằm trong private subnet; quyền truy cập AWS được cấp qua IAM Role; các chỉ số quan trọng được CloudWatch giám sát và gửi email cảnh báo qua SNS.

Kiến trúc hiện tại phù hợp cho mục đích học tập và thử nghiệm. Khi triển khai production, hệ thống nên bổ sung HTTPS với ACM, custom domain với Route 53, nhiều EC2 trên nhiều Availability Zone, RDS Multi-AZ, quản lý secret tập trung, AWS WAF, log tập trung và chính sách backup phù hợp.
