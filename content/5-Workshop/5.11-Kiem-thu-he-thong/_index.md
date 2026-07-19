---
title: "System testing"
date: 2026-07-10
weight: 11
chapter: false
pre: " <b> 5.11. </b> "
---

## 5.11. System testing

This section validates complete business flows rather than isolated screens. Each function should include a successful case, an invalid-input case, and an unauthorized-access case. Recruitment-critical flows receive the highest priority.

## Scope and priority

| Priority | Scope | Requirement |
|---|---|---|
| **P0 — Mandatory** | Sign-in, authorization, company approval, job posting, applications, pipeline, interviews, offers and rejection | Must pass before acceptance or deployment |
| **P1 — Important** | Profiles, CVs, search, application tracking, candidate review, messaging, user and job administration | Must be covered by regression testing |
| **P2 — Supporting** | Saved jobs, job alerts, blog, and statistics dashboard | May follow P0/P1 but still requires test cases |

## Test prerequisites

- CloudFront, the ALB target, EC2 service, and RDS are healthy.
- Separate `candidate`, `recruiter`, and `admin` accounts are available, together with an unapproved company.
- Use synthetic emails, CVs, and company data rather than real personal information.
- Record the case ID, preconditions, steps, input, expected and actual results, status, and evidence.

## Functional coverage

| Group | Required flows | Priority |
|---|---|---|
| Authentication and authorization | Registration/sign-in, wrong password, duplicate email, cross-role access, sign-out and session expiry | P0 |
| Candidate | Profile and CV, search, apply, track status, save jobs, job alerts, messaging | P0–P2 |
| Recruiter | Company approval, post jobs, review profiles, Kanban pipeline, interviews, offers/rejection, messaging | P0–P1 |
| Administrator | Dashboard, company approval, job, blog, and user management | P0–P2 |
| Infrastructure | CloudFront/ALB, RDS, S3, CORS, monitoring, and alerts | P0–P1 |

## Completion criteria

- Run 100% of P0 and P1 cases with no open critical or high-severity defects.
- P0 flows work through CloudFront and cannot bypass authorization by calling APIs directly.
- State changes remain consistent across candidate, recruiter, and administrator views.
- CV access is restricted to authorized principals, and logs or errors expose no secrets.
- Every passing result has a screenshot, API response, or log. Cases without evidence remain **Not tested**.

For non-functional measurement, record p50/p95 response time, error rate, CPU, database connections, and CloudFront cache behavior under controlled load.
