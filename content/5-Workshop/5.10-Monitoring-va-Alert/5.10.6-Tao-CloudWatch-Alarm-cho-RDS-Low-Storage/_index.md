---
title: "Create an Alarm for Low RDS Storage"
date: 2026-07-10
weight: 6
chapter: false
pre: " <b> 5.10.6. </b> "
---

### 5.10.6. Create an Alarm for Low RDS Storage

This CloudWatch alarm monitors the free storage available on RDS. When `recruitpro-db` has less than 1 GB remaining, the system sends an SNS notification so that data can be cleaned up, storage can be increased, or database growth can be investigated before capacity is exhausted.

#### Step 1: Select the FreeStorageSpace metric

Open **CloudWatch → Alarms → All alarms → Create alarm → Select metric**. Navigate to **RDS → DBInstanceIdentifier**, search for `FreeStorageSpace`, and select the `recruitpro-db` DB instance.

![Select the RDS FreeStorageSpace metric](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.6-Tao-CloudWatch-Alarm-cho-RDS-Low-Storage/chon-metric-free-storage-space.jpg>)

This metric measures the number of free storage bytes. The graph shows approximately 19.5 GB available, well above the alarm threshold. Choose **Select metric** to continue.

#### Step 2: Configure the period and storage threshold

Configure the metric and condition as follows:

- **Namespace:** `AWS/RDS`.
- **Metric name:** `FreeStorageSpace`.
- **DBInstanceIdentifier:** `recruitpro-db`.
- **Statistic:** `Average`.
- **Period:** `5 minutes`.
- **Threshold type:** `Static`.
- **Condition:** `Lower` with a threshold of `1000000000` bytes.

![Configure the RDS free-storage threshold](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.6-Tao-CloudWatch-Alarm-cho-RDS-Low-Storage/cau-hinh-nguong-low-storage.jpg>)

`1,000,000,000` bytes equals 1 decimal GB, or about 0.93 GiB. The condition must be **Lower** because risk increases as free space decreases. A 1 GB threshold is suitable for the workshop; production thresholds should account for allocated storage and data growth rate.

#### Step 3: Send notifications to the SNS topic

On **Configure actions**, select **In alarm**, then choose **Select an existing SNS topic** and select `recruitpro-alert-topic`.

![Select the SNS topic for RDS storage notifications](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.6-Tao-CloudWatch-Alarm-cho-RDS-Low-Storage/chon-sns-topic.jpg>)

The email endpoint confirms that the topic has a recipient. When free storage falls below the threshold, CloudWatch publishes the event to SNS, which forwards the alert by email.

#### Step 4: Name the alarm

In **Add alarm details**, enter `RecruitPro-RDS-Low-Storage`.

![Name the low-storage RDS CloudWatch alarm](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.6-Tao-CloudWatch-Alarm-cho-RDS-Low-Storage/dat-ten-alarm.jpg>)

The name clearly identifies the database and alarm condition. In production, a description and tags can record the threshold, environment, and response procedure.

#### Step 5: Review and create the alarm

On **Preview and create**, verify the configuration and choose **Create alarm**.

![Review and create the low-storage RDS alarm](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.6-Tao-CloudWatch-Alarm-cho-RDS-Low-Storage/xem-lai-va-tao-alarm.jpg>)

The Review page confirms the `FreeStorageSpace` metric for `recruitpro-db`, the `Average` statistic, a five-minute period, a threshold lower than `1,000,000,000` bytes, and notification to `recruitpro-alert-topic`. The alarm remains **OK** while sufficient storage is available and enters **In alarm** when free space falls below the threshold.
