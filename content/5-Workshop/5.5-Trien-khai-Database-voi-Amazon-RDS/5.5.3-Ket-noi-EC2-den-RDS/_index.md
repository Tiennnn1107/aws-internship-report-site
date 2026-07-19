---
title: "Connect EC2 to RDS"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.5.3. </b> "
---

### 5.5.3. Connect EC2 to RDS

Confirm that `RecruitPro-BE` and RDS use the same VPC. The RDS security group must allow TCP `3306` from the EC2 backend security group, never from `0.0.0.0/0`.

Copy the RDS hostname and connect to the EC2 instance with Session Manager. On Amazon Linux 2023, install the client and test the connection:

```bash
sudo dnf install mariadb105 -y
mysql -h <RDS_ENDPOINT> -P 3306 -u admin -p
```

Configure Spring Boot in `/etc/recruitpro.env`:

```dotenv
SPRING_DATASOURCE_URL=jdbc:mysql://<RDS_ENDPOINT>:3306/recruitpro
SPRING_DATASOURCE_USERNAME=admin
SPRING_DATASOURCE_PASSWORD=<RDS_PASSWORD>
```

Restart the service and inspect its logs:

```bash
sudo systemctl restart recruitpro
sudo systemctl status recruitpro
sudo journalctl -u recruitpro -n 100 --no-pager
```

`HikariPool`, `Hibernate`, and the application `Started` message indicate a successful connection. For timeouts, check the VPC, port 3306 rule, endpoint, routes, and NACLs. For access errors, verify the credentials and database name.
