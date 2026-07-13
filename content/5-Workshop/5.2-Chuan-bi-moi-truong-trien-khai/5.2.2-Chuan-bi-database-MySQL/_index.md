---
title: "Prepare MySQL database"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.2.2. </b> "
---

### 5.2.2. Prepare MySQL database

Create the `recruitment_db` database on MySQL from a machine with the MySQL client installed or from the backend EC2 instance.

#### 1. Create the database

```bash
mysql -h <MYSQL_HOST> -P 3306 -u <MYSQL_USER> -p
```

```sql
CREATE DATABASE IF NOT EXISTS recruitment_db
  CHARACTER SET utf8mb4
  COLLATE utf8mb4_unicode_ci;
USE recruitment_db;
```

Spring Boot configuration:

```properties
spring.datasource.url=jdbc:mysql://<MYSQL_HOST>:3306/recruitment_db?useUnicode=true&characterEncoding=UTF-8&serverTimezone=Asia/Ho_Chi_Minh
spring.datasource.username=<MYSQL_USER>
spring.datasource.password=<MYSQL_PASSWORD>
```

#### 2. Import schema and sample data

Save the table-creation SQL and the provided sample-data SQL in `recruitment_db.sql`. Run the sample data after the schema so that foreign keys are valid.

```bash
mysql -h <MYSQL_HOST> -P 3306 -u <MYSQL_USER> -p \
  --default-character-set=utf8mb4 recruitment_db < recruitment_db.sql
```

The sample data contains `job_fields`, `users`, `companies`, `candidate_profiles`, `job_postings`, `applications`, `interviews`, `notifications`, and `blogs`.

Before re-running the seed, place this cleanup block before the `INSERT` statements:

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

Run inserts in this order: `job_fields` → `users` → `companies`/`candidate_profiles` → `job_postings` → `applications` → `interviews`/`notifications`/`blogs`.

> Sample passwords are `password123` stored as BCrypt hashes. Do not use sample accounts in production.

#### 3. Verify

```sql
USE recruitment_db;
SHOW TABLES;
SELECT COUNT(*) AS total_users FROM users;
SELECT COUNT(*) AS total_jobs FROM job_postings;
SELECT COUNT(*) AS total_blogs FROM blogs;
```

If Vietnamese text is corrupted, ensure the client uses UTF-8 and include `--default-character-set=utf8mb4` during import.
