---
title: "Tạo S3 Gateway Endpoint"
date: 2026-07-12
weight: 6
chapter: false
pre: " <b> 5.4.6. </b> "
---

## Mục tiêu

Cho phép EC2 trong private subnet truy cập Amazon S3 qua mạng AWS mà không đi qua NAT Gateway hoặc Internet Gateway. Gateway Endpoint cho S3 không tính phí theo giờ.

## Điều kiện đầu vào

- `RecruitVPC` đã được tạo.
- Private application route table đã associate với hai private app subnet.
- Tài khoản đang thao tác có quyền tạo và sửa VPC Endpoint.

## Các bước chi tiết

1. Mở **Amazon VPC Console** tại Region đang triển khai.
2. Trong thanh điều hướng, chọn **Endpoints → Create endpoint**.
3. Name tag nhập `s3-gwe`; **Service category** chọn **AWS services**.
4. Trong ô tìm kiếm Services, nhập `s3`.
5. Chọn service có tên dạng `com.amazonaws.ap-southeast-1.s3` và **Type = Gateway**. Không chọn interface endpoint.
6. Trong **VPC**, chọn `RecruitVPC`.
7. Trong **Route tables**, chọn `Recruit-private-app-rt` đang liên kết với hai private app subnet. Không chọn public hoặc database route table.
8. Trong **Policy**, giữ **Full access** để kiểm thử ban đầu. Không thêm tag nếu workshop không yêu cầu.
9. Chọn **Create endpoint**, chờ thông báo tạo thành công rồi mở endpoint vừa tạo.

## Xác minh

1. Trạng thái endpoint là `Available`.
2. Mở `Recruit-private-app-rt`; tab **Routes** phải có route tới prefix list S3 (`pl-...`) với target là VPC Endpoint (`vpce-...`).
3. Trên EC2 backend chạy:

```bash
aws s3 ls
aws s3 ls s3://<ten-cv-bucket>
```

Hai lệnh phải hoạt động khi EC2 có IAM Role phù hợp.

## Bảo mật và tối ưu

Sau khi kiểm thử, thay Full access bằng endpoint policy giới hạn đúng hai bucket và chỉ cho phép các action cần thiết. Endpoint không thay thế IAM policy; cả IAM policy, bucket policy và endpoint policy đều phải cho phép request.

## Clean-up

Vào **VPC → Endpoints**, chọn `s3-gwe` → **Actions → Delete VPC endpoints**. Route prefix list sẽ tự được gỡ khỏi route table.
