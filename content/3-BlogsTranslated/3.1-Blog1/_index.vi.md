---
title: "Hướng dẫn chuyển đổi từ Amazon EC2 sang EKS Auto Mode với Kiro CLI và MCP Servers"
date: 2026-07-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
author: "AWS Containers Blog"
---


Trong quá trình chạy ứng dụng trên Amazon EC2, bạn có thể đã gặp phải những bài toán như: cập nhật AMI, quản lý Auto Scaling Group, và tối ưu chi phí. EKS Auto Mode giúp giải phóng bạn khỏi các nhiệm vụ đó bằng cách tự động hóa vòng đời node, mở rộng tài nguyên và cấu hình hạ tầng.

![Kiến trúc chuyển đổi sang EKS Auto Mode](/images/3-Blog/b1.1.png)

## Tại sao là EKS Auto Mode?

EKS Auto Mode giúp giảm bớt sự phức tạp của Kubernetes bằng cách tự động:

- cấp phát và thay thế node,
- autoscaling theo nhu cầu thực tế,
- cấu hình mạng và lưu trữ,
- duy trì control plane và worker capacity.

Kết quả là bạn có thể chạy Kubernetes mà không cần quản lý trực tiếp fleet EC2.

## Kiro CLI + MCP Servers làm gì?

Kiro CLI là trợ lý di chuyển thông minh, còn MCP Servers cung cấp lớp xác thực và hội nhập công cụ. Cả hai phối hợp để tự động hóa luồng di chuyển và giảm thiểu sai sót thủ công.

<!-- ![Luồng xác thực Kiro CLI và MCP](/images/3-Blog/b1.2.png) -->

![Các bước xác thực và triển khai cuối cùng](/images/3-Blog/b1.3.png)

Hình này tóm tắt các bước xác thực và triển khai cuối cùng trong quy trình di chuyển từ EC2 sang EKS Auto Mode, bao gồm kiểm tra container, chính sách và chuyển traffic.

## Quy trình di chuyển thực tế

1. Kiểm tra hiện trạng ứng dụng trên EC2: dịch vụ, mạng, lưu trữ, và phụ thuộc.
2. Dùng Kiro CLI để phân tích cấu hình và đề xuất kế hoạch di chuyển.
3. MCP Servers áp các validation gate cho từng bước, đảm bảo cấu hình, chính sách và mạng được kiểm duyệt trước khi triển khai.
4. Di chuyển theo từng giai đoạn: containerize, tạo cluster EKS Auto Mode, và chuyển traffic.
5. Kiểm tra sẵn sàng và chuyển ứng dụng từ EC2 sang EKS Auto Mode.

## Lợi ích khi di chuyển

- Không còn quản lý AMI và script bootstrap thủ công.
- Giảm tải vận hành cho autoscaling và node replacement.
- Tập trung đội vào code và dịch vụ thay vì EC2.
- Đạt được mô hình cloud-native ổn định hơn.

## Thay đổi tư duy vận hành

Sau khi di chuyển, nhóm thường chuyển từ:

- quản lý instance và ASG thủ công
- sang tập trung vào container, manifest và pipeline.

Luồng vận hành mới gồm:

- định nghĩa image và deployment,
- dùng Kiro CLI để hướng dẫn và xác thực,
- dựa vào MCP gate để tự động an toàn,
- giám sát ứng dụng thay vì node.

## Kết luận

Chuyển từ EC2 sang EKS Auto Mode không chỉ là đổi nền tảng, mà còn là cơ hội nâng cấp tư duy vận hành. Với Kiro CLI và MCP Servers, hành trình di chuyển trở nên dễ đoán hơn và ít rủi ro hơn. Nếu bạn đang containerize hệ thống cũ, đây là giải pháp đáng thử.

Link gốc: https://aws.amazon.com/vi/blogs/containers/migrate-amazon-ec2-to-eks-auto-mode-using-kiro-cli-and-mcp-servers/

<p class="blog-community-link"><span>Thảo luận trong cộng đồng:</span><a href="https://www.facebook.com/groups/awsstudygroupfcj/permalink/2209780886453538/">Xem bài viết trên Facebook</a></p>
