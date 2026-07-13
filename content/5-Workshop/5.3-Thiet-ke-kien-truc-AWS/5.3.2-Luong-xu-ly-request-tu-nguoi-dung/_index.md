---
title: "User request processing flow"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.3.2. </b> "
---

### 5.3.2. User request processing flow

When a user accesses RecruitPro, the request passes through the following AWS layers:

```text
User
    ↓ HTTPS
CloudFront / CDN
    ↓
Application Load Balancer (ALB)
    ↓ HTTP :8080
EC2 Backend (Spring Boot)
    ↓ JDBC :3306
Amazon RDS MySQL
```

#### 1. The user sends a request

The browser sends an HTTPS request containing the HTTP method, URL, headers, cookies or JWT, and form data when applicable.

```http
GET /api/jobs?page=0&size=10 HTTP/1.1
Host: recruitpro.example.com
Authorization: Bearer <JWT_TOKEN>
```

#### 2. CloudFront receives and distributes the request

CloudFront receives the request at the nearest edge location, handles SSL/TLS, and checks the cache. Static files such as HTML, CSS, JavaScript, and images can be served directly from cache. Dynamic API requests are forwarded to the ALB and private data is not cached.

#### 3. The ALB routes the request to EC2

The ALB checks the target group and forwards traffic only to healthy EC2 instances. Security Groups allow application traffic to EC2 only from the ALB; external users cannot access the EC2 private IP directly.

#### 4. Spring Boot processes the business logic

The application receives the request in a Controller, validates JWT and input data, calls the Service layer, reads or writes data through a Repository/DAO, and returns an HTTP response.

Example application flow:

```text
POST /api/applications
  → ApplicationController
  → ApplicationService
  → validate candidate and job posting
  → ApplicationRepository.save()
  → RDS MySQL
  → return HTTP 201 Created
```

#### 5. EC2 connects to RDS MySQL

The backend connects to RDS through its internal VPC endpoint. Credentials are stored in environment variables or AWS Systems Manager Parameter Store rather than in source code. The RDS Security Group allows port `3306` only from the backend EC2 Security Group.

#### 6. The response returns to the user

RDS returns the result to the Service, Spring Boot creates a JSON response, and the response travels through the ALB and CloudFront back to the browser. Dynamic responses are forwarded; static resources may be served from cache.

```http
HTTP/1.1 200 OK
Content-Type: application/json

{"content": [], "page": 0, "size": 10}
```

#### 7. Error handling

- No CloudFront origin access: check origin, DNS, and access settings.
- No healthy ALB target: check health checks and the EC2 application.
- Backend cannot connect to RDS: check endpoint, subnets, routes, and port `3306` Security Groups.
- Invalid request: return `400 Bad Request`.
- Missing authentication or permission: return `401 Unauthorized` or `403 Forbidden`.
- Unexpected failure: log to EC2/CloudWatch and return `500 Internal Server Error`.

This flow separates content delivery, load balancing, business processing, and data storage, making the system easier to scale and troubleshoot.
