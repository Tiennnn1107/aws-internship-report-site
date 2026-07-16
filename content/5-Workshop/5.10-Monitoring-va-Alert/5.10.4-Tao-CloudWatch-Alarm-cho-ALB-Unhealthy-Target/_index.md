---
title: "Create an Alarm for Unhealthy ALB Targets"
date: 2026-07-10
weight: 4
chapter: false
pre: " <b> 5.10.4. </b> "
---

### 5.10.4. Create an Alarm for Unhealthy ALB Targets

This CloudWatch alarm monitors the number of targets that fail health checks in the Application Load Balancer's Target Group. When at least one target becomes unhealthy, the system sends an SNS notification so that the backend can be investigated.

#### Step 1: Select the UnHealthyHostCount metric

Open **CloudWatch → Alarms → All alarms → Create alarm → Select metric**. Navigate to **ApplicationELB → Per AppELB, per TG Metrics**, search for `UnHealthyHostCount`, and select the correct `recruit-alb` and `recruit-tg` Target Group pair.

![Select the UnHealthyHostCount metric for the ALB and Target Group](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.4-Tao-CloudWatch-Alarm-cho-ALB-Unhealthy-Target/chon-metric-unhealthy-host.jpg>)

This metric represents the number of targets that the ALB considers unhealthy. The graph currently shows 0, indicating that the targets are passing their health checks. Choose **Select metric** to continue.

#### Step 2: Configure the period and alarm threshold

Configure the metric and condition as follows:

- **Namespace:** `AWS/ApplicationELB`.
- **Metric name:** `UnHealthyHostCount`.
- **Statistic:** `Average`.
- **Period:** `1 minute`.
- **Threshold type:** `Static`.
- **Condition:** `Greater/Equal` with a threshold of `1`.

![Configure the UnHealthyHostCount threshold](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.4-Tao-CloudWatch-Alarm-cho-ALB-Unhealthy-Target/cau-hinh-nguong-unhealthy-host.jpg>)

The condition is met when the average unhealthy target count is at least one during a one-minute period. This short period detects backend failures quickly. In production, requiring multiple consecutive datapoints can reduce alerts caused by brief target restarts.

#### Step 3: Send notifications to the SNS topic

On **Configure actions**, select **In alarm**, then choose **Select an existing SNS topic** and select `recruitpro-alert-topic`.

![Select the SNS topic for unhealthy target notifications](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.4-Tao-CloudWatch-Alarm-cho-ALB-Unhealthy-Target/chon-sns-topic.jpg>)

The email endpoint shown below confirms that the topic has a recipient. When the alarm enters **In alarm**, CloudWatch publishes an event to SNS, which forwards the notification by email. No other actions are required for this workshop.

#### Step 4: Name the alarm

In **Add alarm details**, enter `RecruitPro-ALB-Unhealthy-Target`.

![Name the unhealthy ALB target alarm](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.4-Tao-CloudWatch-Alarm-cho-ALB-Unhealthy-Target/dat-ten-alarm.jpg>)

The name identifies the system, monitored resource, and alarm condition. In production, a description or tags can record the Target Group, environment, and responsible team.

#### Step 5: Review and create the alarm

On **Preview and create**, verify the complete configuration before choosing **Create alarm**.

![Review and create the unhealthy ALB target alarm](</images/5-Workshop/5.10-Monitoring-va-Alert/5.10.4-Tao-CloudWatch-Alarm-cho-ALB-Unhealthy-Target/xem-lai-va-tao-alarm.jpg>)

The Review page confirms the `UnHealthyHostCount` metric, `Average` statistic, one-minute period, threshold greater than or equal to 1, and notification to `recruitpro-alert-topic`. The alarm may initially show **Insufficient data**, then change to **OK** when all targets are healthy or **In alarm** when a target fails its health check.
