---
title: "Create a High-CPU CloudWatch Alarm for the EC2 Backend"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.10.2. </b> "
---

### 5.10.2. Create a High-CPU Alarm for the EC2 Backend

This CloudWatch alarm monitors CPU usage on the backend EC2 instance. When the average CPU utilization exceeds the configured threshold, the alarm enters the **In alarm** state and sends a notification through the SNS topic created in section 5.10.1.

#### Step 1: Select the EC2 CPUUtilization metric

Open **CloudWatch → Alarms → All alarms → Create alarm**, then choose **Select metric**. In the metric selection window, open **EC2 → Per-Instance Metrics**, search for `CPUUtilization`, and select the instance named `RecruitPro-BE`.

![Select the CPUUtilization metric for the RecruitPro-BE instance](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.2-Tao-CloudWatch-Alarm-cho-EC2-CPU/chon-metric-ec2-cpu.jpg>)

The graph shows the instance's CPU utilization over time. Selecting a per-instance metric ensures that the alarm monitors only the RecruitPro backend instance instead of combining data from other EC2 instances. Choose **Select metric** to continue.

#### Step 2: Configure the statistic and alarm threshold

In the **Metric** section, configure:

- **Statistic:** `Average`, to evaluate the average CPU utilization during each period.
- **Period:** `5 minutes`, to evaluate data in five-minute intervals.

In the **Conditions** section, select **Static**, choose **Greater**, and set the CPU threshold to `80`.

![Configure the CPU alarm condition](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.2-Tao-CloudWatch-Alarm-cho-EC2-CPU/cau-hinh-nguong-cpu.jpg>)

The final configuration shown on the Review page evaluates the condition **CPUUtilization > 80%**. The value `10000` visible in the input screenshot was a temporary value entered before the threshold was corrected to `80`; it is not the final alarm threshold. An 80% threshold detects sustained high CPU load without triggering notifications for ordinary short-term fluctuations.

After verifying the condition, choose **Next**.

#### Step 3: Send notifications to the SNS topic

On the **Configure actions** page, select **In alarm** as the alarm state trigger. This means that CloudWatch sends a notification when the metric exceeds the configured threshold.

![Select the SNS topic for CPU alarm notifications](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.2-Tao-CloudWatch-Alarm-cho-EC2-CPU/chon-sns-topic.jpg>)

Choose **Select an existing SNS topic**, then select `recruitpro-alert-topic`. The interface displays the email endpoint subscribed to the topic, confirming where the alarm notification will be delivered. Lambda and Auto Scaling actions are not required for this workshop. Choose **Next** to continue.

#### Step 4: Name the CloudWatch alarm

In the **Add alarm details** section, enter `RecruitPro-EC2-High-CPU` as the alarm name.

![Name the EC2 CPU CloudWatch alarm](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.2-Tao-CloudWatch-Alarm-cho-EC2-CPU/dat-ten-alarm.jpg>)

This name identifies the system, monitored resource, and alarm condition, making the alarm easy to locate when multiple alarms exist. The description and tags are optional but can provide additional operational context in a production environment. Choose **Next** to review the configuration.

#### Step 5: Review and create the alarm

On the **Preview and create** page, verify the complete configuration before creating the alarm.

![Review and create the CloudWatch alarm](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.2-Tao-CloudWatch-Alarm-cho-EC2-CPU/xem-lai-va-tao-alarm.jpg>)

The image confirms the following final settings:

- **Namespace:** `AWS/EC2`.
- **Metric:** `CPUUtilization` for the `RecruitPro-BE` instance.
- **Statistic:** `Average`.
- **Period:** `5 minutes`.
- **Condition:** CPU utilization is greater than `80%`.
- **Action:** when the alarm enters the **In alarm** state, send a notification to `recruitpro-alert-topic`.
- **Alarm name:** `RecruitPro-EC2-High-CPU`.

If all settings are correct, choose **Create alarm**. CloudWatch may initially display **Insufficient data** while it collects metric data. The alarm then changes to **OK** or **In alarm**, depending on the observed CPU utilization.
