---
title: "Week 11 Worklog"
date: 2026-06-26
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

{{% notice warning %}}
 **Note:** The following content records the learning and implementation activities completed during the week and is intended for the personal worklog report.
{{% /notice %}}

### Week 11 Objectives:

- Set up email notifications through SNS.
- Create CloudWatch Alarms for key EC2, ALB, and RDS operational metrics.
- Validate alarm states and the notification path from resources to the administrator email.

### Tasks carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 06/26/2026 | Created SNS topic `recruitpro-alert-topic`, added an email subscription, and confirmed it from the email message. | 06/26/2026 | 06/26/2026 | SNS topic and subscription records |
| 06/27/2026 | Created `RecruitPro-EC2-High-CPU` and `RecruitPro-ALB-Target-5XX` and configured SNS alarm actions. | 06/27/2026 | 06/27/2026 | CloudWatch Alarm records |
| 06/28/2026 | Created `RecruitPro-ALB-Unhealthy-Target` and checked the related metric and target health. | 06/28/2026 | 06/28/2026 | CloudWatch and ALB metrics |
| 06/29/2026 | Created `RecruitPro-RDS-High-CPU` and `RecruitPro-RDS-Low-Storage` and connected their actions to the SNS topic. | 06/29/2026 | 06/29/2026 | CloudWatch and RDS metrics |
| 06/30/2026 | Observed `OK`, `In alarm`, and `Insufficient data` states and verified one ALB 5XX alarm activation. | 06/30/2026 | 06/30/2026 | Alarm history and notification email |
| 07/01/2026 – 07/02/2026 | Captured the alarm list with `Actions enabled` and documented EC2/ALB/RDS → CloudWatch → SNS → Admin Email. | 07/01/2026 | 07/02/2026 | Monitoring screenshots and personal notes |

### Week 11 Achievements:

- Created `recruitpro-alert-topic` and confirmed its email subscription.
- Completed five correctly named CloudWatch Alarms for EC2, ALB, and RDS.
- Connected alarm actions to SNS and observed all three alarm states.
- Verified that the ALB 5XX alarm could enter `In alarm` and send a notification.
- Completed monitoring evidence without using SES because SES was not deployed.
