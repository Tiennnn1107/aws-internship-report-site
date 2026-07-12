---
title: "Deploy file JAR lên EC2"
date: 2026-07-10
weight: 4
chapter: false
pre: " <b> 5.6.4. </b> "
---

### 5.6.4. Deploy file JAR lên EC2

#### Bước 1: Build ứng dụng tại máy local

Tại thư mục source code, chạy:

```powershell
mvnw.cmd clean package -DskipTests
copy target\j2pp-0.0.1-SNAPSHOT.jar app.jar
```

Upload các artifact lên bucket triển khai:

- JAR: `s3://recruitpro-deploy-artifacts-tien/app.jar`
- SQL (nếu có): `s3://recruitpro-deploy-artifacts-tien/recruitment_db.sql`

Có thể upload bằng AWS Console hoặc AWS CLI:

```powershell
aws s3 cp app.jar s3://recruitpro-deploy-artifacts-tien/app.jar
aws s3 cp recruitment_db.sql s3://recruitpro-deploy-artifacts-tien/recruitment_db.sql
```

#### Bước 2: Tải artifact xuống EC2

Trong Session Manager, chạy:

```bash
aws s3 cp s3://recruitpro-deploy-artifacts-tien/app.jar /tmp/app.jar
aws s3 cp s3://recruitpro-deploy-artifacts-tien/recruitment_db.sql /tmp/recruitment_db.sql
```

Di chuyển file JAR vào thư mục ứng dụng:

```bash
sudo mv /tmp/app.jar /opt/recruitpro/app.jar
sudo chown ec2-user:ec2-user /opt/recruitpro/app.jar
```

{{% notice note %}}
IAM Role gắn với EC2 phải có quyền `s3:GetObject` đối với bucket artifact. Nếu không có file SQL, bỏ qua lệnh tải `recruitment_db.sql`.
{{% /notice %}}
