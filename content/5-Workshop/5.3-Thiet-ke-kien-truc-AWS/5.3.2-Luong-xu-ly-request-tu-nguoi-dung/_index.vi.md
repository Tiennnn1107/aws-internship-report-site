---
title: "Luồng xử lý request từ người dùng"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.3.2. </b> "
---

### 5.3.2. Luồng xử lý request từ người dùng

Khi người dùng truy cập RecruitPro, request đi qua các lớp AWS theo luồng sau:

```text
Người dùng
    ↓ HTTPS
CloudFront / CDN
    ↓
Application Load Balancer (ALB)
    ↓ HTTP :8080
EC2 Backend (Spring Boot)
    ↓ JDBC :3306
Amazon RDS MySQL
```

#### 1. Người dùng gửi request

Người dùng truy cập tên miền của hệ thống bằng trình duyệt. Trình duyệt gửi request HTTPS, kèm theo phương thức HTTP, URL, header, cookie hoặc JWT và dữ liệu biểu mẫu nếu có.

Ví dụ khi xem danh sách việc làm:

```http
GET /api/jobs?page=0&size=10 HTTP/1.1
Host: recruitpro.example.com
Authorization: Bearer <JWT_TOKEN>
```

#### 2. CloudFront tiếp nhận và phân phối request

CloudFront nhận request tại edge location gần người dùng nhất, xử lý SSL/TLS và kiểm tra cache. Các file tĩnh như HTML, CSS, JavaScript và hình ảnh có thể được trả trực tiếp từ cache. Request API động được chuyển tiếp đến ALB và không lưu cache dữ liệu riêng tư.

#### 3. ALB phân phối đến EC2 backend

ALB nhận request từ CloudFront rồi kiểm tra target group. Chỉ những EC2 instance đang ở trạng thái `healthy` mới nhận request. ALB phân phối request giúp hệ thống tiếp tục hoạt động khi một instance gặp lỗi.

Security Group của EC2 chỉ cho phép traffic ứng dụng từ ALB; người dùng bên ngoài không truy cập trực tiếp private IP của EC2.

#### 4. Spring Boot xử lý nghiệp vụ

Trên EC2, ứng dụng Spring Boot thực hiện các bước:

1. Nhận request tại Controller.
2. Kiểm tra JWT, quyền truy cập và dữ liệu đầu vào.
3. Gọi Service để xử lý nghiệp vụ tuyển dụng.
4. Gọi Repository/DAO để đọc hoặc ghi dữ liệu.
5. Trả response JSON và mã trạng thái HTTP cho người dùng.

Ví dụ luồng ứng tuyển:

```text
POST /api/applications
  → ApplicationController
  → ApplicationService
  → kiểm tra candidate và job posting
  → ApplicationRepository.save()
  → RDS MySQL
  → trả về HTTP 201 Created
```

#### 5. EC2 kết nối RDS MySQL

Backend kết nối RDS bằng endpoint nội bộ trong VPC. Kết nối sử dụng user/password được quản lý trong biến môi trường hoặc AWS Systems Manager Parameter Store, không ghi trực tiếp trong source code.

RDS Security Group chỉ cho phép EC2 backend kết nối cổng `3306`. Dữ liệu trao đổi giữa backend và RDS không đi qua Internet công cộng.

#### 6. Trả response về người dùng

RDS trả kết quả cho Service, sau đó Spring Boot tạo response JSON. Response đi ngược qua ALB và CloudFront về trình duyệt. Với dữ liệu động, CloudFront chuyển tiếp response mới; với tài nguyên tĩnh, CloudFront có thể trả từ cache.

```http
HTTP/1.1 200 OK
Content-Type: application/json

{"content": [], "page": 0, "size": 10}
```

#### 7. Các trường hợp lỗi

- CloudFront không truy cập được origin: kiểm tra origin, DNS và quyền truy cập.
- ALB không có target healthy: kiểm tra health check và ứng dụng trên EC2.
- Backend không kết nối được RDS: kiểm tra endpoint, subnet, route table và Security Group cổng `3306`.
- Request không hợp lệ: Spring Boot trả `400 Bad Request`.
- Chưa đăng nhập hoặc không đủ quyền: trả `401 Unauthorized` hoặc `403 Forbidden`.
- Lỗi ngoài dự kiến: ghi log trên EC2/CloudWatch và trả `500 Internal Server Error`.

Luồng này giúp tách riêng lớp phân phối nội dung, cân bằng tải, xử lý nghiệp vụ và lưu trữ dữ liệu; nhờ đó hệ thống dễ mở rộng và kiểm tra lỗi hơn.
