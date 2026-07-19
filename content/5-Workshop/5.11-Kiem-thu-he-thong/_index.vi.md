---
title: "Kiểm thử hệ thống"
date: 2026-07-10
weight: 11
chapter: false
pre: " <b> 5.11. </b> "
---

## 5.11. Kiểm thử hệ thống

Mục tiêu của phần này là kiểm tra toàn bộ **luồng nghiệp vụ quan trọng**, thay vì chỉ kiểm tra từng màn hình. Mỗi chức năng cần ít nhất một trường hợp thành công, một trường hợp dữ liệu không hợp lệ và một trường hợp người dùng không có quyền. Các luồng ảnh hưởng trực tiếp đến tuyển dụng được ưu tiên kiểm thử trước.

## Phạm vi và mức ưu tiên

| Mức | Phạm vi | Yêu cầu |
|---|---|---|
| **P0 - Bắt buộc** | Đăng nhập, phân quyền, xác thực công ty, đăng tin, ứng tuyển, pipeline, phỏng vấn, offer/từ chối | Phải đạt trước khi nghiệm thu hoặc triển khai |
| **P1 - Quan trọng** | Hồ sơ, CV, tìm kiếm, theo dõi đơn, xem ứng viên, nhắn tin, quản trị người dùng/tin tuyển dụng | Phải kiểm thử đầy đủ trong vòng regression |
| **P2 - Bổ trợ** | Lưu việc làm, Job Alerts, blog, dashboard thống kê | Có thể kiểm thử sau P0/P1 nhưng vẫn phải có test case |

Không cần thử mọi tổ hợp dữ liệu có thể xảy ra. Tuy nhiên, **tất cả chức năng đã công bố phải có test case**; các luồng P0/P1 phải được kiểm thử end-to-end và kiểm thử lại sau mỗi thay đổi lớn.

## Điều kiện kiểm thử

- CloudFront, ALB target, EC2 service và RDS ở trạng thái healthy.
- Chuẩn bị tài khoản riêng cho `candidate`, `recruiter`, `admin` và một công ty chưa được duyệt.
- Dùng email, CV và dữ liệu công ty giả; không dùng thông tin cá nhân thật.
- Mỗi test case ghi: mã, tiền điều kiện, bước thực hiện, dữ liệu, kết quả mong đợi, kết quả thực tế, trạng thái và bằng chứng.

## Ma trận bao phủ chức năng

| Nhóm | Luồng cần kiểm thử | Ưu tiên |
|---|---|---|
| Xác thực và phân quyền | Đăng ký/đăng nhập; sai mật khẩu; email trùng; truy cập chéo vai trò; đăng xuất/hết phiên | P0 |
| Ứng viên | Hồ sơ và CV; tìm kiếm; ứng tuyển; theo dõi trạng thái; lưu việc; Job Alerts; nhắn tin | P0-P2 |
| Nhà tuyển dụng | Xác thực công ty; đăng tin; xem hồ sơ; Kanban; lịch phỏng vấn; offer/từ chối; nhắn tin | P0-P1 |
| Quản trị viên | Dashboard; duyệt công ty; quản lý tin, blog và người dùng | P0-P2 |
| Hạ tầng | CloudFront/ALB, RDS, S3, CORS, monitoring và cảnh báo | P0-P1 |

## Tiêu chí hoàn thành

- 100% test case P0 và P1 đã được chạy; không còn lỗi nghiêm trọng hoặc lỗi cao đang mở.
- Các luồng P0 đạt trên CloudFront và không thể bị bỏ qua bằng cách gọi API trực tiếp.
- Dữ liệu chuyển trạng thái nhất quán giữa ứng viên, nhà tuyển dụng và quản trị viên.
- CV chỉ được truy cập bởi đúng chủ thể có quyền; log và thông báo lỗi không làm lộ secret hoặc dữ liệu nhạy cảm.
- Mỗi kết quả **Đạt** có ảnh chụp, response API hoặc log tương ứng. Chức năng chưa có bằng chứng phải ghi **Chưa kiểm thử**, không suy diễn là đã đạt.

## Đo lường phi chức năng

Chạy lượng request có kiểm soát và ghi p50/p95 response time, error rate, CPU, DB connections cùng CloudFront cache hit rate. Sau kiểm thử lỗi phải khôi phục cấu hình, kiểm tra dữ liệu và xác nhận alarm trở lại `OK`.
