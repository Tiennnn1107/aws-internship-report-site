---
title: "Introduction to the RecruitBox System on AWS"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

## 5.1. Introduction to the RecruitBox System on AWS

RecruitBox is an online recruitment system designed to connect candidates and employers through a centralized platform. The application uses Spring Boot for backend business logic, Thymeleaf for the user interface, MySQL for relational data management, and file storage for candidate CVs. Its primary objective is to digitize the recruitment process and make job, candidate profile, and recruitment data management more convenient and consistent.

The main functions of RecruitBox include user registration and authentication; allowing candidates to browse job listings, update their personal profiles, and upload CVs; and enabling employers or administrators to manage recruitment data. Together, these functions form a basic workflow from the moment a candidate discovers a job to the storage and review of their profile and CV.

Deploying RecruitBox on AWS provides a stable and scalable operating environment with clear separation between networking, application, database, and file-storage components. Instead of hosting the entire system on a single server, AWS services are assigned specialized responsibilities. This approach supports access control, improves availability, enables operational monitoring, and reduces the impact of failures in individual components.

In the overall architecture, users access the application through CloudFront or an Application Load Balancer. The ALB receives requests and forwards them to the EC2 backend running the Spring Boot application. Relational data such as accounts, profiles, and job information is stored in Amazon RDS for MySQL, while Amazon S3 stores candidate CVs and application deployment artifacts. VPC and IAM provide the networking foundation and access-control mechanisms for communication between resources.

In addition to the components serving the application directly, Amazon CloudWatch monitors operational metrics from EC2, ALB, and RDS. When a metric exceeds a configured alarm threshold, Amazon SNS sends an email notification so that the administrator can investigate and respond promptly. The following sections describe the preparation, architecture design, infrastructure configuration, and detailed deployment of RecruitBox on AWS.
