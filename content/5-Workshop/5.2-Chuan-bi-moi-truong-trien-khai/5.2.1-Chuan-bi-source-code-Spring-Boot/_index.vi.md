---
title: "Chuẩn bị source code Spring Boot"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.2.1. </b> "
---

### 5.2.1. Chuẩn bị source code Spring Boot

Clone hoặc mở dự án RecruitBox Spring Boot và xác nhận source code có các class ứng dụng, Maven Wrapper, file `pom.xml` và các file cấu hình cần thiết.

1. Kiểm tra máy đã cài đặt phiên bản Java Development Kit tương thích.
2. Kiểm tra `application.properties` và chuyển các giá trị phụ thuộc môi trường sang biến môi trường. Không commit mật khẩu database, AWS credential hoặc secret khác.
3. Chạy kiểm thử và build file JAR triển khai:

```bash
./mvnw clean package
```

Trên Windows, chạy:

```powershell
.\mvnw.cmd clean package
```

4. Xác nhận quá trình build thành công và file JAR được tạo trong thư mục `target`. Artifact này sẽ được tải lên và triển khai trên EC2 backend ở bước sau.

![Source code Spring Boot](/images/5-Workshop/5.2-Chuan-bi-moi-truong-trien-khai/5.2.1-Chuan-bi-source-code-Spring-Boot/source-code.jpg)
