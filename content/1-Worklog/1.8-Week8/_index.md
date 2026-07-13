---
title: "Week 8 Worklog"
date: 2026-06-05
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

{{% notice warning %}}
 **Note:** The following content records the learning and implementation activities completed during the week and is intended for the personal worklog report.
{{% /notice %}}

### Week 8 Objectives:

- Deploy a private RDS MySQL database and an EC2 backend in a private app subnet.
- Administer EC2 through Systems Manager without assigning a public IP.
- Deploy RecruitPro as a JAR managed by systemd and verify RDS connectivity.

### Tasks carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 06/05/2026 | Created a DB subnet group from both private DB subnets and launched private Single-AZ RDS MySQL on port `3306` with database `recruitpro`. | 06/05/2026 | 06/05/2026 | RDS configuration records |
| 06/06/2026 | Allowed TCP `3306` from the EC2 Security Group to RDS and created `RecruitPro-BE` in a private app subnet without a public IP. | 06/06/2026 | 06/06/2026 | EC2 and Security Group records |
| 06/07/2026 | Created an EC2 IAM Role, attached `AmazonSSMManagedInstanceCore`, and connected through Systems Manager Session Manager. | 06/07/2026 | 06/07/2026 | Systems Manager connection record |
| 06/08/2026 | Installed Java 17 and a MySQL/MariaDB client and verified the EC2-to-RDS connection on port `3306`. | 06/08/2026 | 06/08/2026 | EC2 terminal verification |
| 06/09/2026 | Created `recruitpro`, imported the SQL file, and checked tables and data without recording credentials in the worklog. | 06/09/2026 | 06/09/2026 | Database import verification |
| 06/10/2026 – 06/11/2026 | Prepared `/etc/recruitpro.env`, deployed `/opt/recruitpro/app.jar`, and created `recruitpro.service`.<br>&emsp;Checked `systemctl status`, `journalctl`, and `curl localhost:8080`. | 06/10/2026 | 06/11/2026 | systemd status and application logs |

### Week 8 Achievements:

- Deployed Single-AZ RDS MySQL in the private DB subnet group with the `recruitpro` database.
- Created `RecruitPro-BE` without a public IP and administered it through Session Manager.
- Installed Java 17 and a database client and validated EC2-to-RDS connectivity.
- Imported SQL data, deployed `app.jar`, and operated the application with `recruitpro.service`.
- Verified service status, logs, and the local response without exposing passwords or secrets.
