---
title: "Giới thiệu hệ thống RecruitBox trên AWS"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

## 5.1. Giới thiệu hệ thống RecruitBox trên AWS

RecruitBox là hệ thống tuyển dụng trực tuyến được xây dựng nhằm hỗ trợ kết nối ứng viên với nhà tuyển dụng trên một nền tảng tập trung. Ứng dụng sử dụng Spring Boot để xử lý nghiệp vụ phía máy chủ, Thymeleaf để xây dựng giao diện, MySQL để quản lý dữ liệu quan hệ và cơ chế lưu trữ tệp để tiếp nhận CV của ứng viên. Mục tiêu của hệ thống là số hóa quy trình tuyển dụng, giúp việc quản lý thông tin việc làm, hồ sơ ứng viên và dữ liệu tuyển dụng trở nên thuận tiện, nhất quán hơn.

Các chức năng chính của RecruitBox bao gồm đăng ký và đăng nhập tài khoản; cho phép ứng viên xem danh sách việc làm, cập nhật hồ sơ cá nhân và tải CV lên hệ thống; đồng thời cung cấp chức năng để nhà tuyển dụng hoặc quản trị viên quản lý dữ liệu liên quan đến quá trình tuyển dụng. Các chức năng này tạo thành một quy trình cơ bản, từ lúc ứng viên tiếp cận thông tin việc làm cho đến khi hồ sơ và CV được lưu trữ để phục vụ việc xem xét, quản lý.

Việc triển khai RecruitBox trên AWS giúp hệ thống có một môi trường vận hành ổn định, dễ mở rộng và tách biệt rõ ràng giữa các thành phần mạng, ứng dụng, cơ sở dữ liệu và lưu trữ tệp. Thay vì đặt toàn bộ hệ thống trên một máy chủ duy nhất, các dịch vụ AWS được sử dụng đúng theo vai trò chuyên biệt, qua đó hỗ trợ kiểm soát truy cập, nâng cao tính sẵn sàng, theo dõi trạng thái vận hành và giảm rủi ro khi một thành phần gặp sự cố.

Trong kiến trúc tổng quan, người dùng truy cập ứng dụng thông qua CloudFront hoặc Application Load Balancer. ALB tiếp nhận và chuyển tiếp request đến EC2 Backend đang chạy ứng dụng Spring Boot. Dữ liệu quan hệ như tài khoản, hồ sơ và thông tin việc làm được lưu trong Amazon RDS for MySQL, trong khi Amazon S3 lưu trữ CV của ứng viên và artifact dùng để triển khai ứng dụng. VPC và IAM cung cấp nền tảng mạng cùng cơ chế phân quyền truy cập giữa các tài nguyên.

Bên cạnh các thành phần phục vụ trực tiếp cho ứng dụng, Amazon CloudWatch được sử dụng để theo dõi các chỉ số vận hành của EC2, ALB và RDS. Khi một chỉ số vượt ngưỡng cảnh báo đã cấu hình, Amazon SNS gửi thông báo qua email để người quản trị có thể kiểm tra và xử lý kịp thời. Các mục tiếp theo sẽ trình bày lần lượt quá trình chuẩn bị, thiết kế kiến trúc, cấu hình hạ tầng và triển khai chi tiết hệ thống RecruitBox trên AWS.
