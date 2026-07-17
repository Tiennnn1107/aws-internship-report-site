---
title: "Kiểm thử đăng ký và đăng nhập"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.11.1. </b> "
---

### 5.11.1. Kiểm thử đăng ký và đăng nhập

1. Open the **Register** page, enter the full name, email, and password, select the **Candidate** role, accept the terms, and submit the form.
2. The application displays a successful registration message and asks the user to sign in.

![Candidate account registered successfully](</images/5-Workshop/5.11-Kiem-thu-he-thong/5.11.1-Kiem-thu-dang-ky-va-dang-nhap/dang-ky-tai-khoan-thanh-cong.jpg>)

3. Sign in with the newly created account. After successful authentication, the application redirects to the home page and displays the account name in the navigation bar.

![Candidate account signed in successfully](</images/5-Workshop/5.11-Kiem-thu-he-thong/5.11.1-Kiem-thu-dang-ky-va-dang-nhap/dang-nhap-thanh-cong.jpg>)

**Result:** The registration and sign-in flow works correctly through CloudFront; the candidate account is created and the authenticated session is maintained.
