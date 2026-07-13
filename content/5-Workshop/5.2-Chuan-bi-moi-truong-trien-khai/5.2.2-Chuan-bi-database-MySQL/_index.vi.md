---
title: "Chuẩn bị database MySQL"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.2.2. </b> "
---

### 5.2.2. Chuẩn bị database MySQL

Tạo database `recruitment_db` trên MySQL. Có thể chạy các lệnh dưới đây từ máy có cài MySQL client hoặc từ EC2 backend.

#### 1. Tạo database

```bash
mysql -h <MYSQL_HOST> -P 3306 -u <MYSQL_USER> -p
```

```sql
CREATE DATABASE IF NOT EXISTS recruitment_db
  CHARACTER SET utf8mb4
  COLLATE utf8mb4_unicode_ci;
USE recruitment_db;
```

Cấu hình Spring Boot:

```properties
spring.datasource.url=jdbc:mysql://<MYSQL_HOST>:3306/recruitment_db?useUnicode=true&characterEncoding=UTF-8&serverTimezone=Asia/Ho_Chi_Minh
spring.datasource.username=<MYSQL_USER>
spring.datasource.password=<MYSQL_PASSWORD>
```

#### 2. Import schema và dữ liệu mẫu

Lưu phần tạo bảng và phần dữ liệu mẫu được cung cấp trong file `recruitment_db.sql`. Phần dữ liệu mẫu phải chạy sau phần tạo bảng để các khóa ngoại hợp lệ.

```bash
mysql -h <MYSQL_HOST> -P 3306 -u <MYSQL_USER> -p \
  --default-character-set=utf8mb4 recruitment_db < recruitment_db.sql
```

Dữ liệu mẫu gồm `job_fields`, `users`, `companies`, `candidate_profiles`, `job_postings`, `applications`, `interviews`, `notifications` và `blogs`.

Khi chạy lại seed, đặt đoạn dọn dữ liệu sau trước các lệnh `INSERT`:

```sql
SET FOREIGN_KEY_CHECKS = 0;
DELETE FROM notifications;
DELETE FROM interviews;
DELETE FROM applications;
DELETE FROM job_skills;
DELETE FROM job_postings;
DELETE FROM candidate_profiles;
DELETE FROM recruiter_approval_requests;
DELETE FROM companies;
DELETE FROM blogs;
DELETE FROM users;
DELETE FROM job_fields;
SET FOREIGN_KEY_CHECKS = 1;
```

Thứ tự `INSERT`: `job_fields` → `users` → `companies`/`candidate_profiles` → `job_postings` → `applications` → `interviews`/`notifications`/`blogs`.

> Mật khẩu mẫu là `password123` ở dạng BCrypt hash. Không sử dụng tài khoản mẫu trên production.

#### 3. Kiểm tra

```sql
USE recruitment_db;
SHOW TABLES;
SELECT COUNT(*) AS total_users FROM users;
SELECT COUNT(*) AS total_jobs FROM job_postings;
SELECT COUNT(*) AS total_blogs FROM blogs;
```

Nếu tiếng Việt bị lỗi, kiểm tra client dùng UTF-8 và luôn thêm `--default-character-set=utf8mb4` khi import.
