---
title: "Create an SNS Topic for Email Alerts"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.10.1. </b> "
---

### 5.10.1. Create an SNS Topic for Email Alerts

Amazon SNS receives notifications from CloudWatch alarms. When a monitored metric crosses its threshold, CloudWatch publishes a message to the SNS topic and SNS delivers it to the confirmed email endpoint.

## Step 1: Create the SNS topic

In **Asia Pacific (Singapore)** (`ap-southeast-1`), open **Amazon SNS → Topics → Create topic**.

- Select `Standard`, which supports email delivery and is appropriate for CloudWatch notifications.
- Enter `recruitpro-alert-topic` as the topic name.
- The display name can remain empty because it is mainly used for SMS.

Keep the default encryption, access, delivery, and logging settings for this workshop, then create the topic.

## Step 2: Create an email subscription

Open `recruitpro-alert-topic`, choose **Create subscription**, and configure:

- **Topic ARN:** the ARN of `recruitpro-alert-topic` in `ap-southeast-1`.
- **Protocol:** `Email`.
- **Endpoint:** the address that will receive alerts.

No filter or redrive policy is required for basic email alerts. Create the subscription to send the confirmation request.

## Step 3: Confirm the subscription

Open the **AWS Notification - Subscription Confirmation** message from `no-reply@sns.amazonaws.com` and select **Confirm subscription**. Check the spam folder if the message is not in the inbox.

## Step 4: Verify the subscription

Return to the topic's **Subscriptions** tab. The email endpoint must show status **Confirmed**. The topic can now be selected as the notification target for subsequent CloudWatch alarms.
