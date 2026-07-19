---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
# RecruitBox — Cloud-Based Recruitment Platform on AWS

## An AWS-Based Online Recruitment System

## 1. Executive Summary

RecruitBox is an online recruitment platform deployed on AWS to support the recruitment process among candidates, recruiters, and administrators. The system allows users to register, log in, browse job postings, update personal profiles, upload CV files, and manage recruitment data. The application is built with Spring Boot, Thymeleaf, and MySQL, then deployed on AWS using a practical cloud web application architecture.

The solution uses Amazon EC2 to run the Spring Boot backend, Amazon RDS for MySQL to store relational data, Amazon S3 to store candidate CVs and deployment artifacts, an Application Load Balancer to route requests to the backend, Amazon CloudFront to provide a CDN and HTTPS access layer in front of the ALB, and Amazon CloudWatch together with Amazon SNS for monitoring and email alerts.

The system is deployed inside a dedicated VPC in the Asia Pacific (Singapore) Region. Public subnets contain the ALB and NAT Gateway, while private subnets contain the EC2 backend and RDS database. This design separates public and private components, improves security, and more closely represents a production-style cloud architecture.

## 2. Problem Statement

### Current Challenges

In traditional recruitment systems, candidate information, personal profiles, CV files, and job data are often managed separately through email, manually stored files, or local databases. This approach makes it difficult to scale the system, manage CV files, monitor service health, and provide stable access for users.

In addition, when an application runs only on a local machine or a single public server, it lacks important capabilities such as network isolation, access control, centralized file storage, monitoring, alerting, and future scalability.

### Proposed Solution

RecruitBox is deployed on AWS to address these issues through a clearly structured cloud architecture. The backend application runs on an EC2 instance in a private application subnet. The Amazon RDS for MySQL database is also deployed privately, while the Application Load Balancer is placed in public subnets to receive requests from users.

Amazon S3 is used to store candidate CV files and application deployment artifacts. IAM roles and policies allow EC2 to access S3 securely without hard-coded access keys. Amazon CloudWatch monitors EC2, ALB, and RDS metrics, while Amazon SNS delivers email notifications when alarms are triggered.

Amazon CloudFront is integrated in front of the ALB to provide CDN delivery and an HTTPS endpoint. AWS Systems Manager Session Manager is used to connect to the private EC2 instance without exposing SSH access to the public Internet.

### Benefits and Value

The solution enables the recruitment system to operate in a real cloud environment rather than only on a local machine. Candidate data, job information, and profiles are stored in Amazon RDS for MySQL; CV files are stored separately in Amazon S3; the backend remains in a private subnet; and monitoring and alerting help detect operational problems early.

From a workshop and learning perspective, the project demonstrates how multiple AWS services can be combined to build a practical application across compute, database, storage, networking, security, content delivery, and monitoring layers. It also provides a foundation for future improvements such as CI/CD, Auto Scaling, a custom HTTPS domain, Amazon Cognito, or an automated CV-processing pipeline.

## 3. Solution Architecture

RecruitBox follows a cloud-based web application architecture on AWS. Users access the system through Amazon CloudFront or directly through the Application Load Balancer. The ALB receives HTTP requests and forwards them to the EC2 instance running the Spring Boot backend. The backend handles business logic and authentication, reads and writes relational data in Amazon RDS for MySQL, and uploads CV files to Amazon S3.

The system is deployed within a dedicated VPC. Public subnets contain the Application Load Balancer and NAT Gateway. Private application subnets contain the EC2 backend, while private database subnets contain Amazon RDS for MySQL. Route tables, the Internet Gateway, NAT Gateway, and security groups control communication between components.

Amazon CloudWatch collects metrics from EC2, ALB, and RDS. CloudWatch alarms are configured for high EC2 CPU utilization, ALB target 5XX errors, unhealthy ALB targets, high RDS CPU utilization, and low RDS free storage. When an alarm is triggered, CloudWatch sends a notification to an SNS topic, which then delivers an email alert to the administrator.

![RecruitBox AWS solution architecture](/images/2-Proposal/architected.jpg)

### High-Level Architecture Flow

```text
User
→ Amazon CloudFront
→ Application Load Balancer
→ EC2 Spring Boot Backend
→ Amazon RDS for MySQL

EC2 Spring Boot Backend
→ Amazon S3 CV Storage

EC2 / ALB / RDS
→ CloudWatch Alarm
→ SNS Topic
→ Administrator Email
```

### AWS Services Used

- **Amazon VPC:** Provides an isolated network for the entire system, including public, private application, and private database subnets.
- **Public Subnets:** Host the Application Load Balancer and NAT Gateway.
- **Private Application Subnets:** Host the EC2 backend without exposing the instance directly to the Internet.
- **Private Database Subnets:** Host Amazon RDS for MySQL and restrict access to the backend.
- **Internet Gateway:** Provides Internet connectivity for public subnets.
- **NAT Gateway:** Allows the EC2 instance in a private subnet to access packages, S3, and external services without a public IP address.
- **Route Tables:** Direct traffic between subnets, the Internet Gateway, and the NAT Gateway.
- **Security Groups:** Control inbound and outbound traffic among the ALB, EC2, and RDS.
- **IAM Roles and Policies:** Grant EC2 permission to access S3 without storing access keys in the source code.
- **Amazon EC2:** Runs the Spring Boot backend as a JAR file managed by a systemd service.
- **Amazon RDS for MySQL:** Stores relational data such as users, job postings, candidate profiles, applications, and recruitment information.
- **Amazon S3:** Stores candidate CV files, deployment JAR files, and database backup or import files.
- **Application Load Balancer:** Provides the public application endpoint and forwards requests to the EC2 backend.
- **Amazon CloudFront:** Provides a CDN and HTTPS layer in front of the ALB using a `cloudfront.net` endpoint.
- **AWS Systems Manager Session Manager:** Provides administrative access to the private EC2 instance without opening public SSH.
- **Amazon CloudWatch:** Monitors EC2, ALB, and RDS metrics.
- **Amazon SNS:** Sends email alerts when CloudWatch alarms are triggered.

## 4. Technical Implementation

### Implementation Phases

The project is implemented in several phases, beginning with application analysis and AWS architecture design, followed by network creation, database deployment, backend deployment, public application access, CloudFront integration, and monitoring configuration.

The first phase prepares the Spring Boot source code, the MySQL database, and the JAR file built on the local development machine. The AWS network is then created using a VPC, public and private subnets, route tables, an Internet Gateway, and a NAT Gateway.

Next, Amazon RDS for MySQL is deployed in private database subnets. The EC2 backend is launched in a private application subnet, attached to an IAM role for S3 access, and managed through Systems Manager Session Manager. The Spring Boot application is deployed as `app.jar` and managed by a systemd service.

After the backend is operational, a target group and Application Load Balancer are created to expose the application through the ALB DNS name. Amazon CloudFront is configured in front of the ALB to provide CDN and HTTPS access. Finally, CloudWatch alarms and SNS email alerts are configured to monitor the system.

### Technical Requirements

- **Backend Application:** Spring Boot, Thymeleaf, and MySQL. The JAR file is built locally and deployed to EC2.
- **Database:** Amazon RDS for MySQL runs in private subnets and accepts connections only from the EC2 backend on port 3306.
- **File Storage:** Amazon S3 stores CV files and deployment artifacts. Block Public Access remains enabled.
- **Networking:** The VPC is divided into public and private subnets. The ALB runs publicly, while EC2 and RDS remain private. The NAT Gateway provides outbound Internet connectivity for the EC2 instance.
- **Security:** Security groups expose only required ports. The ALB accepts HTTP traffic from users, EC2 accepts port 8080 traffic only from the ALB, and RDS accepts MySQL traffic only from the EC2 security group.
- **Monitoring:** CloudWatch alarms monitor key metrics, and SNS sends email alerts to the administrator.

## 5. Roadmap and Implementation Milestones

### Phase 1: Application Preparation

- Review the Spring Boot source code.
- Build the JAR file locally.
- Prepare the SQL database file.
- Select the Asia Pacific (Singapore) Region for deployment.

### Phase 2: Network Design and Creation

- Create the VPC.
- Create public, private application, and private database subnets.
- Configure the Internet Gateway.
- Configure the NAT Gateway.
- Configure route tables.
- Create security groups for ALB, EC2, and RDS.

### Phase 3: Database and Backend Deployment

- Create Amazon RDS for MySQL in private subnets.
- Launch the EC2 backend in a private subnet.
- Install Java and the MySQL client on EC2.
- Upload the JAR and SQL files to S3.
- Download deployment artifacts from S3 to EC2.
- Import the database into RDS.
- Run the Spring Boot application through a systemd service.

### Phase 4: Public Application Access

- Create a target group for the EC2 backend.
- Create the Application Load Balancer.
- Configure an HTTP listener on port 80.
- Test access through the ALB DNS name.
- Integrate CloudFront in front of the ALB.
- Configure CORS for access through the CloudFront domain.

### Phase 5: Monitoring and Alerting

- Create an SNS topic.
- Create and confirm an email subscription.
- Create CloudWatch alarms for EC2, ALB, and RDS.
- Verify alarm states and SNS actions.

### Phase 6: System Testing

- Test user registration and login.
- Test job browsing.
- Test candidate profile updates.
- Test CV upload to S3.
- Test access through ALB and CloudFront.
- Test CloudWatch alarms and SNS notifications.

## 6. Budget Estimate

Actual costs depend on resource runtime, Region, instance type, traffic, and storage usage. The project uses a small workshop-oriented deployment and prioritizes cost-efficient configurations such as a small EC2 instance, a Single-AZ RDS instance, limited S3 storage, and basic CloudWatch alarms.

Potential cost components include:

- **Amazon EC2:** Backend instance runtime.
- **Amazon RDS for MySQL:** Database instance, storage, and backups.
- **Application Load Balancer:** Hourly usage and processed traffic.
- **NAT Gateway:** Hourly usage and processed data.
- **Amazon S3:** Storage and request costs for CV files and deployment artifacts.
- **Amazon CloudFront:** Request and data-transfer costs when usage exceeds free limits or uses pay-as-you-go pricing.
- **Amazon CloudWatch:** Alarm, log, and custom metric costs if usage exceeds free allocations.
- **Amazon SNS:** Notification delivery costs, which are generally minimal for basic email alerts.
- **Data Transfer:** Internet and inter-service data transfer where applicable.

The infrastructure budget should be reviewed using AWS Pricing Calculator before production deployment. After the workshop or demonstration, cost-generating resources such as NAT Gateway, ALB, EC2, and RDS should be stopped or removed to avoid unnecessary charges.

## 7. Risk Assessment

### Risk Matrix

- **EC2 backend failure or stopped service:** High impact, medium probability. Users cannot access application functions when the backend is unavailable.
- **RDS connectivity failure:** High impact, medium probability. Incorrect endpoints or security-group rules prevent the backend from reading or writing data.
- **S3 CV upload failure:** Medium impact, medium probability. Missing `s3:PutObject` permissions prevent candidates from uploading CV files.
- **CloudFront account or policy restrictions:** Medium impact, medium probability. Incorrect behavior settings or account limitations may block dynamic requests.
- **Unexpected NAT Gateway, ALB, or RDS costs:** Medium impact, medium probability.
- **SNS email alerts not delivered:** Low-to-medium impact, medium probability. Notifications are not delivered when the email subscription has not been confirmed.

### Mitigation Strategies

The Spring Boot application is managed by systemd so it can restart automatically after a failure. CloudWatch monitors EC2 CPU utilization and unhealthy ALB targets to detect backend issues.

Amazon RDS is deployed in private subnets and is accessible only from the EC2 backend through security-group rules. Connectivity is validated using the MySQL client on EC2 before the application is started.

IAM roles grant specific access to the CV and deployment S3 buckets. This enables secure file upload without hard-coded credentials.

To control costs, resources are sized for workshop use and should be reviewed regularly in AWS Billing. NAT Gateway, ALB, EC2, and RDS should be removed or stopped after the project is completed.

### Contingency Plan

If CloudFront is unavailable or blocks a request, the application can remain accessible through the ALB DNS name. If the EC2 backend fails, administrators can inspect logs with `journalctl` and restart the systemd service. If the RDS import fails, the database can be restored by re-importing the SQL file stored in the S3 deployment bucket.

## 8. Expected Outcomes

After implementation, RecruitBox will operate as an online recruitment platform hosted on AWS. Users will be able to access the website, register, log in, browse job postings, update personal profiles, and upload CV files. The backend will process business logic on EC2, relational data will be stored in Amazon RDS for MySQL, and CV files will be stored in Amazon S3.

From an architectural perspective, the project demonstrates the deployment of a practical web application with networking, compute, database, storage, load balancing, content delivery, security, and monitoring layers. Multiple AWS services work together instead of running the application on a single isolated server.

From a learning perspective, the project provides practical experience in designing a VPC, deploying EC2 and RDS in private subnets, using a NAT Gateway for outbound connectivity, granting access through IAM roles, exposing an application through an ALB, integrating CloudFront, and implementing monitoring through CloudWatch and SNS.

Future improvements may include Route 53 and AWS Certificate Manager for a custom HTTPS domain, an Auto Scaling Group for the EC2 backend, a CI/CD pipeline using CodePipeline, CodeBuild, and CodeDeploy, Amazon Cognito for identity management, or an automated CV-processing pipeline using S3 events, Lambda or a worker service, and an AI service.
