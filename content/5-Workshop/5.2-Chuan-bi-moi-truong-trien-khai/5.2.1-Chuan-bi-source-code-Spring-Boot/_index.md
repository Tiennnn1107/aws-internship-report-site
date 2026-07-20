---
title: "Prepare the Spring Boot Source Code"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.2.1. </b> "
---

### 5.2.1. Prepare the Spring Boot Source Code

Clone or open the RecruitBox Spring Boot project and verify that the source tree contains the application classes, Maven wrapper, `pom.xml`, and configuration files.

1. Confirm that a supported Java Development Kit is installed.
2. Review `application.properties` and replace environment-specific values with environment variables. Do not commit database passwords, AWS credentials, or other secrets.
3. Run the automated tests and build the deployable JAR:

```bash
./mvnw clean package
```

On Windows, run:

```powershell
.\mvnw.cmd clean package
```

4. Confirm that the build completes successfully and that the JAR file is created in the `target` directory. This artifact will be uploaded and deployed to the backend EC2 instance in a later step.

![Source code Spring Boot](/images/5-Workshop/5.2-Chuan-bi-moi-truong-trien-khai/5.2.1-Chuan-bi-source-code-Spring-Boot/source-code.jpg)
