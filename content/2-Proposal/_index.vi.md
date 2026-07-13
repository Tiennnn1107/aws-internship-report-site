---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
# RecruitBox — Cloud-Based Recruitment Platform on AWS

## Giải pháp triển khai hệ thống tuyển dụng trực tuyến trên AWS

## 1. Tóm tắt điều hành

RecruitBox là hệ thống tuyển dụng trực tuyến được triển khai trên AWS nhằm hỗ trợ quy trình tuyển dụng giữa ứng viên, nhà tuyển dụng và quản trị viên. Hệ thống cho phép người dùng đăng ký, đăng nhập, xem danh sách việc làm, cập nhật hồ sơ cá nhân, upload CV và quản lý dữ liệu tuyển dụng. Ứng dụng được xây dựng bằng Spring Boot, Thymeleaf và MySQL, sau đó được triển khai lên hạ tầng AWS theo mô hình web application thực tế.

Giải pháp sử dụng Amazon EC2 để chạy backend Spring Boot, Amazon RDS MySQL để lưu trữ dữ liệu quan hệ, Amazon S3 để lưu trữ CV và deployment artifacts, Application Load Balancer để phân phối request đến backend, CloudFront để cung cấp lớp truy cập CDN/HTTPS phía trước ALB, và CloudWatch kết hợp SNS để giám sát và gửi cảnh báo qua email.

Hệ thống được triển khai trong một VPC riêng tại region Asia Pacific (Singapore), với public subnet cho ALB/NAT Gateway và private subnet cho EC2 backend và RDS database. Thiết kế này giúp tách biệt các thành phần public và private, tăng tính bảo mật và mô phỏng gần hơn với kiến trúc cloud production thực tế.

## 2. Tuyên bố vấn đề

### Vấn đề hiện tại

Trong các hệ thống tuyển dụng truyền thống, việc quản lý ứng viên, hồ sơ cá nhân, CV và thông tin tuyển dụng thường được thực hiện rời rạc qua email, file lưu trữ thủ công hoặc database nội bộ. Cách tiếp cận này gây khó khăn trong việc mở rộng, quản lý file CV, giám sát hệ thống và đảm bảo khả năng truy cập ổn định cho người dùng.

Ngoài ra, nếu ứng dụng chỉ chạy trên máy local hoặc một server đơn lẻ, hệ thống sẽ thiếu các yếu tố quan trọng như phân tách network, kiểm soát truy cập, lưu trữ file tập trung, monitoring, cảnh báo lỗi và khả năng mở rộng trong tương lai.

### Giải pháp

RecruitBox được triển khai trên AWS để giải quyết các vấn đề trên bằng cách xây dựng một hệ thống tuyển dụng có kiến trúc cloud rõ ràng. Ứng dụng backend được triển khai trên EC2 trong private subnet, database được lưu trong Amazon RDS MySQL cũng ở private subnet, trong khi Application Load Balancer nằm ở public subnet để tiếp nhận request từ người dùng.

Amazon S3 được sử dụng để lưu trữ file CV của ứng viên và file artifact dùng cho quá trình deploy ứng dụng. IAM Role và IAM Policy được cấu hình để EC2 có thể truy cập S3 một cách an toàn mà không cần hard-code access key. CloudWatch được dùng để theo dõi EC2, ALB và RDS, trong khi SNS gửi email cảnh báo khi có alarm xảy ra.

CloudFront được tích hợp phía trước ALB để cung cấp lớp CDN/HTTPS và cải thiện mô hình truy cập của hệ thống. Ngoài ra, Systems Manager Session Manager được dùng để truy cập EC2 private instance mà không cần mở SSH public.

### Lợi ích và giá trị mang lại

Giải pháp giúp hệ thống tuyển dụng có khả năng vận hành trên môi trường cloud thực tế, thay vì chỉ chạy local. Dữ liệu ứng viên, thông tin việc làm và hồ sơ được lưu trữ trong RDS MySQL; file CV được lưu riêng trên S3; backend được đặt trong private subnet để giảm rủi ro bảo mật; và hệ thống có monitoring/alert để phát hiện lỗi sớm.

Về mặt học tập và workshop, project thể hiện được cách kết hợp nhiều dịch vụ AWS để xây dựng một ứng dụng thực tế, bao gồm compute, database, storage, networking, security, content delivery và monitoring. Đây là nền tảng tốt để phát triển thêm các tính năng như CI/CD, Auto Scaling, HTTPS custom domain, Cognito authentication hoặc pipeline xử lý CV trong tương lai.

## 3. Kiến trúc giải pháp

RecruitBox sử dụng kiến trúc cloud web application trên AWS. Người dùng truy cập hệ thống thông qua CloudFront hoặc trực tiếp qua Application Load Balancer. ALB nhận request HTTP và chuyển tiếp đến EC2 backend đang chạy ứng dụng Spring Boot. Backend xử lý nghiệp vụ, xác thực người dùng, đọc/ghi dữ liệu vào Amazon RDS MySQL và upload file CV lên Amazon S3.

Hệ thống được triển khai bên trong một VPC riêng. Public subnet chứa Application Load Balancer và NAT Gateway. Private app subnet chứa EC2 backend, còn private database subnet chứa RDS MySQL. Route table, Internet Gateway, NAT Gateway và Security Group được cấu hình để kiểm soát luồng truy cập giữa các thành phần.

CloudWatch thu thập metric từ EC2, ALB và RDS. Các CloudWatch Alarm được cấu hình cho EC2 CPU cao, ALB Target 5XX, ALB Unhealthy Target, RDS CPU cao và RDS Low Storage. Khi alarm được kích hoạt, CloudWatch gửi sự kiện đến SNS Topic và SNS gửi email cảnh báo cho quản trị viên.
![mô hình kiến trúc](/images/2-Proposal/architected.jpg)

### Luồng kiến trúc tổng quan

```text
User
→ CloudFront
→ Application Load Balancer
→ EC2 Spring Boot Backend
→ Amazon RDS MySQL

EC2 Spring Boot Backend
→ Amazon S3 CV Storage

EC2 / ALB / RDS
→ CloudWatch Alarm
→ SNS Topic
→ Admin Email
```

### Dịch vụ AWS sử dụng

- **Amazon VPC:** Tạo mạng riêng cho toàn bộ hệ thống, bao gồm public subnet, private app subnet và private database subnet.
- **Public Subnet:** Chứa ALB và NAT Gateway, cho phép các thành phần public tiếp nhận request từ Internet.
- **Private App Subnet:** Chứa EC2 backend để ứng dụng không bị public trực tiếp ra Internet.
- **Private DB Subnet:** Chứa RDS MySQL để database chỉ có thể truy cập từ backend.
- **Internet Gateway:** Cho phép public subnet kết nối Internet.
- **NAT Gateway:** Cho phép EC2 trong private subnet tải package, truy cập S3 hoặc Internet outbound mà không cần public IP.
- **Route Table:** Điều hướng traffic giữa public subnet, private subnet, Internet Gateway và NAT Gateway.
- **Security Group:** Kiểm soát inbound/outbound traffic giữa ALB, EC2 và RDS.
- **IAM Role/Policy:** Cấp quyền cho EC2 truy cập S3 bucket mà không cần lưu access key trong source code.
- **Amazon EC2:** Chạy ứng dụng Spring Boot backend dưới dạng file JAR và quản lý bằng systemd service.
- **Amazon RDS MySQL:** Lưu trữ dữ liệu quan hệ như user, job posting, candidate profile, application và thông tin tuyển dụng.
- **Amazon S3:** Lưu trữ CV của ứng viên, file JAR deploy artifact và file database backup/import.
- **Application Load Balancer:** Public endpoint của hệ thống, nhận request từ người dùng và forward đến EC2 backend.
- **Amazon CloudFront:** CDN/HTTPS layer phía trước ALB, giúp hệ thống có endpoint HTTPS dạng `cloudfront.net` và hỗ trợ phân phối nội dung.
- **AWS Systems Manager Session Manager:** Truy cập EC2 private instance mà không cần mở SSH public.
- **Amazon CloudWatch:** Theo dõi metric của EC2, ALB và RDS.
- **Amazon SNS:** Gửi email cảnh báo cho admin khi CloudWatch Alarm được kích hoạt.

## 4. Triển khai kỹ thuật

### Các giai đoạn triển khai

Dự án được triển khai theo nhiều giai đoạn, bắt đầu từ phân tích ứng dụng, thiết kế kiến trúc AWS, tạo hạ tầng mạng, triển khai database, deploy backend, public ứng dụng, tích hợp CloudFront và cuối cùng là cấu hình monitoring.

Giai đoạn đầu tiên là chuẩn bị source code Spring Boot, database MySQL và file JAR build từ local. Sau đó, hạ tầng AWS được thiết kế với VPC, public/private subnet, route table, Internet Gateway và NAT Gateway để tách biệt các thành phần public và private.

Tiếp theo, Amazon RDS MySQL được tạo trong private database subnet. EC2 backend được tạo trong private app subnet, gắn IAM Role để truy cập S3 và sử dụng Systems Manager Session Manager để kết nối. Ứng dụng Spring Boot được deploy lên EC2 dưới dạng `app.jar`, chạy bằng systemd service.

Sau khi backend hoạt động, Application Load Balancer và Target Group được tạo để public ứng dụng ra Internet thông qua ALB DNS. CloudFront được cấu hình phía trước ALB để cung cấp CDN/HTTPS access. Cuối cùng, CloudWatch Alarm và SNS Email Alert được triển khai để giám sát hệ thống.

### Yêu cầu kỹ thuật

- **Backend Application:** Ứng dụng sử dụng Spring Boot, Thymeleaf và MySQL. File JAR được build từ source code và deploy lên EC2.
- **Database:** Amazon RDS MySQL chạy trong private subnet, chỉ cho phép EC2 backend truy cập qua port 3306.
- **File Storage:** Amazon S3 được dùng để lưu CV ứng viên và deployment artifacts. Bucket được bật Block Public Access để tránh public file không mong muốn.
- **Networking:** VPC được chia thành public subnet và private subnet. ALB nằm trong public subnet, EC2 và RDS nằm trong private subnet. NAT Gateway giúp EC2 private subnet có outbound Internet.
- **Security:** Security Group được cấu hình theo nguyên tắc chỉ mở port cần thiết. ALB nhận HTTP từ Internet, EC2 chỉ nhận port 8080 từ ALB, RDS chỉ nhận MySQL từ EC2.
- **Monitoring:** CloudWatch Alarm theo dõi các chỉ số quan trọng và SNS gửi email alert cho admin.

## 5. Lộ trình và mốc triển khai

### Giai đoạn 1: Chuẩn bị ứng dụng

- Kiểm tra source code Spring Boot.
- Build file JAR từ local.
- Chuẩn bị file SQL database.
- Xác định region AWS triển khai là Singapore.

### Giai đoạn 2: Thiết kế và tạo network

- Tạo VPC.
- Tạo public subnet, private app subnet và private database subnet.
- Cấu hình Internet Gateway.
- Cấu hình NAT Gateway.
- Cấu hình Route Table.
- Tạo Security Group cho ALB, EC2 và RDS.

### Giai đoạn 3: Triển khai database và backend

- Tạo Amazon RDS MySQL trong private subnet.
- Tạo EC2 backend trong private subnet.
- Cài Java và MySQL client trên EC2.
- Upload JAR và SQL lên S3.
- Tải artifact từ S3 về EC2.
- Import database vào RDS.
- Chạy Spring Boot bằng systemd service.

### Giai đoạn 4: Public ứng dụng

- Tạo Target Group cho EC2 backend.
- Tạo Application Load Balancer.
- Cấu hình listener HTTP port 80.
- Kiểm tra truy cập qua ALB DNS.
- Tích hợp CloudFront phía trước ALB.
- Cấu hình CORS để hỗ trợ truy cập qua CloudFront.

### Giai đoạn 5: Monitoring và alert

- Tạo SNS Topic.
- Tạo email subscription và confirm subscription.
- Tạo CloudWatch Alarm cho EC2, ALB và RDS.
- Kiểm tra trạng thái alarm và action gửi email.

### Giai đoạn 6: Kiểm thử hệ thống

- Kiểm thử đăng ký và đăng nhập.
- Kiểm thử xem danh sách việc làm.
- Kiểm thử cập nhật hồ sơ ứng viên.
- Kiểm thử upload CV lên S3.
- Kiểm thử truy cập qua ALB và CloudFront.
- Kiểm thử CloudWatch Alarm và SNS notification.

## 6. Ước tính ngân sách

Chi phí thực tế phụ thuộc vào thời gian chạy tài nguyên, region, instance type và lượng traffic. Dự án sử dụng mô hình triển khai nhỏ phục vụ workshop, vì vậy ưu tiên các cấu hình tiết kiệm chi phí như EC2 nhỏ, RDS Single-AZ, S3 dung lượng thấp và CloudWatch alarm cơ bản.

Các thành phần có thể phát sinh chi phí gồm:

- **Amazon EC2:** Chi phí chạy instance backend.
- **Amazon RDS MySQL:** Chi phí database instance, storage và backup.
- **Application Load Balancer:** Chi phí theo thời gian chạy và lượng request.
- **NAT Gateway:** Chi phí theo thời gian chạy và data processed.
- **Amazon S3:** Chi phí lưu trữ CV, artifact và số lượng request.
- **Amazon CloudFront:** Chi phí request và data transfer nếu vượt free tier hoặc dùng pay-as-you-go.
- **Amazon CloudWatch:** Chi phí alarm, logs và metric nếu vượt mức miễn phí.
- **Amazon SNS:** Chi phí gửi notification, thường rất nhỏ với email alert cơ bản.
- **Data Transfer:** Chi phí truyền dữ liệu giữa Internet và AWS nếu có traffic đáng kể.

Đối với môi trường workshop, ngân sách nên được kiểm tra bằng AWS Pricing Calculator trước khi triển khai chính thức. Khi hoàn tất demo, cần dọn dẹp các tài nguyên tốn phí như NAT Gateway, ALB, EC2 và RDS để tránh phát sinh chi phí không cần thiết.

## 7. Đánh giá rủi ro

### Ma trận rủi ro

- **EC2 backend bị lỗi hoặc service dừng:** Ảnh hưởng cao, xác suất trung bình. Nếu backend dừng, người dùng không thể truy cập chức năng hệ thống.
- **RDS không kết nối được:** Ảnh hưởng cao, xác suất trung bình. Nếu RDS Security Group hoặc endpoint sai, backend không thể đọc/ghi dữ liệu.
- **S3 upload CV thất bại:** Ảnh hưởng trung bình, xác suất trung bình. Nếu IAM Role thiếu quyền `s3:PutObject`, ứng viên không thể upload CV.
- **CloudFront bị chặn bởi account hoặc policy:** Ảnh hưởng trung bình, xác suất trung bình. Nếu CloudFront account bị giới hạn hoặc cấu hình behavior sai, một số request động có thể lỗi.
- **Chi phí tăng do NAT Gateway, ALB hoặc RDS chạy lâu:** Ảnh hưởng trung bình, xác suất trung bình.
- **Email alert không gửi được:** Ảnh hưởng thấp đến trung bình, xác suất trung bình. Nếu SNS subscription chưa confirm, CloudWatch Alarm sẽ không gửi email.

### Chiến lược giảm thiểu

Đối với EC2, ứng dụng được quản lý bằng systemd service để có thể restart tự động khi gặp lỗi. CloudWatch Alarm theo dõi EC2 CPU và ALB Unhealthy Target để phát hiện sự cố backend.

Đối với RDS, database được đặt trong private subnet và chỉ cho phép EC2 backend truy cập qua Security Group. Kết nối được kiểm tra bằng MySQL client trên EC2 trước khi chạy ứng dụng.

Đối với S3, IAM Role được cấp quyền cụ thể cho bucket CV và bucket deploy artifact. Điều này giúp ứng dụng có thể upload CV mà không cần hard-code access key.

Đối với chi phí, tài nguyên được triển khai ở mức nhỏ phục vụ workshop và cần dọn dẹp sau khi hoàn thành. Các dịch vụ như NAT Gateway, ALB, EC2 và RDS nên được kiểm tra thường xuyên trong Billing Dashboard.

### Kế hoạch dự phòng

Nếu CloudFront gặp giới hạn hoặc request upload bị chặn, hệ thống vẫn có thể hoạt động thông qua ALB DNS. Nếu EC2 backend lỗi, có thể kiểm tra log bằng `journalctl` và restart service. Nếu RDS import lỗi, có thể import lại database từ file SQL lưu trong S3 deploy bucket.

## 8. Kết quả kỳ vọng

Sau khi hoàn thành, RecruitBox có thể hoạt động như một hệ thống tuyển dụng trực tuyến triển khai trên AWS. Người dùng có thể truy cập website, đăng ký, đăng nhập, xem danh sách việc làm, cập nhật hồ sơ cá nhân và upload CV. Backend xử lý nghiệp vụ trên EC2, dữ liệu được lưu trong RDS MySQL và file CV được lưu trên S3.

Về kiến trúc, project thể hiện được cách triển khai một web application thực tế trên AWS với đầy đủ các lớp: network, compute, database, storage, load balancing, CDN, security và monitoring. Hệ thống sử dụng nhiều dịch vụ AWS phối hợp với nhau thay vì chỉ chạy ứng dụng trên một server đơn lẻ.

Về giá trị học tập, dự án giúp hiểu cách thiết kế VPC, đặt EC2/RDS trong private subnet, sử dụng NAT Gateway cho outbound access, cấp quyền bằng IAM Role, public ứng dụng bằng ALB, tích hợp CloudFront và xây dựng monitoring bằng CloudWatch/SNS.

Trong tương lai, hệ thống có thể được mở rộng bằng cách thêm Route 53 và ACM cho custom domain HTTPS, Auto Scaling Group cho EC2 backend, CI/CD pipeline với CodePipeline/CodeBuild/CodeDeploy, Cognito cho authentication, hoặc pipeline xử lý CV bằng S3 Event, Lambda/Worker và AI service.