---
title: "Import Data into RDS"
date: 2026-07-10
weight: 4
chapter: false
pre: " <b> 5.5.4. </b> "
---

### 5.5.4. Import Data into RDS

Từ EC2, kết nối đến RDS MySQL bằng tài khoản quản trị:

```bash
mysql -h <RDS_ENDPOINT> -P 3306 -u admin -p
```

Create the application database in MySQL:

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

Replace `<RDS_ENDPOINT>` with the RDS endpoint. When prompted, enter the password for the `admin` account; do not place the password directly in the command.
