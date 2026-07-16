---
title: "Create a High-CPU Alarm for Amazon RDS"
date: 2026-07-10
weight: 5
chapter: false
pre: " <b> 5.10.5. </b> "
---

### 5.10.5. Create a High-CPU Alarm for Amazon RDS

This CloudWatch alarm monitors CPU utilization on the RDS database. When the average CPU usage of `recruitpro-db` exceeds 80%, the system sends an SNS notification so that database queries, connections, and load can be investigated.

#### Step 1: Select the RDS CPUUtilization metric

Open **CloudWatch → Alarms → All alarms → Create alarm → Select metric**. Navigate to **RDS → DBInstanceIdentifier**, search for `CPUUtilization`, and select the `recruitpro-db` DB instance.

![Select the CPUUtilization metric for recruitpro-db](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.5-Tao-CloudWatch-Alarm-cho-RDS-CPU/chon-metric-rds-cpu.jpg>)

The graph shows the database CPU percentage over time. In the image, utilization remains around 3–6%. Selecting the metric by DB instance ensures that the alarm monitors only the system database. Choose **Select metric** to continue.

#### Step 2: Configure the period and CPU threshold

Configure the metric and condition as follows:

- **Namespace:** `AWS/RDS`.
- **Metric name:** `CPUUtilization`.
- **DBInstanceIdentifier:** `recruitpro-db`.
- **Statistic:** `Average`.
- **Period:** `5 minutes`.
- **Threshold type:** `Static`.
- **Condition:** `Greater` with a threshold of `80`.

![Configure the RDS CPU threshold](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.5-Tao-CloudWatch-Alarm-cho-RDS-CPU/cau-hinh-nguong-rds-cpu.jpg>)

The condition is met when average CPU utilization exceeds 80% during a five-minute period. This detects sustained high CPU load rather than short spikes. Repeated alarms should prompt checks of slow queries, connection pools, indexes, and DB instance capacity.

#### Step 3: Send notifications to the SNS topic

On **Configure actions**, select **In alarm**, then choose **Select an existing SNS topic** and select `recruitpro-alert-topic`.

![Select the SNS topic for RDS CPU notifications](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.5-Tao-CloudWatch-Alarm-cho-RDS-CPU/chon-sns-topic.jpg>)

The email endpoint confirms that the topic has a recipient. When CPU exceeds the threshold, CloudWatch publishes the event to SNS, which forwards the notification by email. No other actions are required for this workshop.

#### Step 4: Name the alarm

In **Add alarm details**, enter `RecruitPro-RDS-High-CPU`.

![Name the high-CPU RDS CloudWatch alarm](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.5-Tao-CloudWatch-Alarm-cho-RDS-CPU/dat-ten-alarm.jpg>)

The alarm name clearly identifies the system, resource type, and condition. In production, a description and tags can record the environment, severity, and responsible team.

#### Step 5: Review and create the alarm

On **Preview and create**, verify the configuration and choose **Create alarm**.

![Review and create the RDS CPU CloudWatch alarm](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.5-Tao-CloudWatch-Alarm-cho-RDS-CPU/xem-lai-va-tao-alarm.jpg>)

The Review page confirms the `CPUUtilization` metric for `recruitpro-db`, the `Average` statistic, a five-minute period, a CPU threshold greater than 80%, and notification to `recruitpro-alert-topic`. The alarm may initially show **Insufficient data**, then change to **OK** or **In alarm** according to the CPU data.
