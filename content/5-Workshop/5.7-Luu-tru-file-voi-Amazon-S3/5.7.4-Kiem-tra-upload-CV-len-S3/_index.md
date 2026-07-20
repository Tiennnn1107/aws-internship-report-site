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

![Selecting a PDF CV from the computer for upload](</images/5-Workshop/5.7-Luu-tru-file-voi-Amazon-S3/5.7.4-Kiem-tra-upload-CV-len-S3/chon-file-cv-pdf.jpg>)

3. Confirm that the application reports a successful upload and that a new encrypted object appears under the CV bucket prefix.

![CV files uploaded to the cv prefix in Amazon S3](</images/5-Workshop/5.7-Luu-tru-file-voi-Amazon-S3/5.7.4-Kiem-tra-upload-CV-len-S3/kiem-tra-cv-tren-s3.jpg>)

4. Open and download the CV through the application to verify read access.

![CV displayed successfully on the candidate profile](</images/5-Workshop/5.7-Luu-tru-file-voi-Amazon-S3/5.7.4-Kiem-tra-upload-CV-len-S3/hien-thi-cv-tren-ho-so.jpg>)

![Opening a CV from Amazon S3 through a temporary signed URL](</images/5-Workshop/5.7-Luu-tru-file-voi-Amazon-S3/5.7.4-Kiem-tra-upload-CV-len-S3/mo-cv-tu-s3-qua-ung-dung.jpg>)

5. Test an invalid file type, an oversized file, and unauthenticated access. The application must reject each request without creating an orphaned S3 object.

The bucket must remain private; access should be authorized by the backend through its EC2 IAM role rather than public object URLs.

![Amazon S3 denying direct access to the CV through a public URL](</images/5-Workshop/5.7-Luu-tru-file-voi-Amazon-S3/5.7.4-Kiem-tra-upload-CV-len-S3/tu-choi-truy-cap-cong-khai-cv-s3.jpg>)
