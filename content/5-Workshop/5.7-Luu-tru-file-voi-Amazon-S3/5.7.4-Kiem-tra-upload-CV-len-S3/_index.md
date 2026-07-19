---
title: "Test CV Uploads to S3"
date: 2026-07-10
weight: 4
chapter: false
pre: " <b> 5.7.4. </b> "
---

### 5.7.4. Test CV Uploads to S3

1. Sign in with a candidate account and open the profile page.
2. Select a valid PDF CV within the configured size limit and save the profile.
3. Confirm that the application reports a successful upload and that a new encrypted object appears under the CV bucket prefix.
4. Open and download the CV through the application to verify read access.
5. Test an invalid file type, an oversized file, and unauthenticated access. The application must reject each request without creating an orphaned S3 object.

The bucket must remain private; access should be authorized by the backend through its EC2 IAM role rather than public object URLs.
