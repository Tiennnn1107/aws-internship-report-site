---
title: "Import dữ liệu vào RDS"
date: 2026-07-10
weight: 4
chapter: false
pre: " <b> 5.5.4. </b> "
---

### 5.5.4. Import dữ liệu vào RDS

Từ EC2, kết nối đến RDS MySQL bằng tài khoản quản trị:

```bash
mysql -h <RDS_ENDPOINT> -P 3306 -u admin -p
```

Tạo database cho ứng dụng trong MySQL:

```sql
CREATE DATABASE IF NOT EXISTS recruitpro;
SHOW DATABASES;
EXIT;
```

Import dữ liệu từ file SQL đã tải về EC2:

```bash
mysql -h <RDS_ENDPOINT> -P 3306 -u admin -p recruitpro < /tmp/recruitment_db.sql
```

Kết nối lại để kiểm tra kết quả:

```bash
mysql -h <RDS_ENDPOINT> -P 3306 -u admin -p
```

```sql
USE recruitpro;
SHOW TABLES;
SELECT * FROM users LIMIT 5;
EXIT;
```

Thay `<RDS_ENDPOINT>` bằng endpoint của RDS. Khi được yêu cầu, nhập mật khẩu của tài khoản `admin`; không ghi mật khẩu trực tiếp trong câu lệnh.
