---
title: "Event 23/5/2026 - FCAJ Community Day"
date: 2026-05-23
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Bài thu hoạch FCAJ Community Day

Ngày 23/05/2026, tôi tham gia FCAJ Community Day cùng một người bạn. Sự kiện có nhiều chủ đề khác nhau, từ cách làm việc hiệu quả với AI đến CloudFront, trải nghiệm hackathon và hệ thống Multi-Agent. Trong bài này, tôi tập trung ghi lại những nội dung bản thân thấy dễ áp dụng nhất vào việc học và dự án của mình.

## Các phiên chia sẻ

Chương trình gồm các phần trình bày:

- Anh Tịnh: **Context Is Everything**.
- Phạm Ngô Hải Anh: **Friendly AI Assistant with Amazon Quick**.
- Nguyễn Tuấn Thịnh: **From Edge to Origin**.
- Team VIB: **36 Hours with LotusHacks**.
- Đào Đức: **Non-Determinism of Deterministic LLM Settings**.
- Cát Vy: **Enterprise-Grade Multi-Agent System**.

## Những nội dung tôi chú ý

### Context quan trọng khi sử dụng AI

Trước đây tôi thường nghĩ prompt càng dài thì AI càng trả lời tốt. Sau phần chia sẻ, tôi hiểu rằng điều quan trọng hơn là thông tin phải liên quan đến yêu cầu. Một context tốt nên nói rõ mục tiêu, dữ liệu cần dùng, giới hạn và dạng kết quả mong muốn. Nếu đưa quá nhiều tài liệu không liên quan, AI có thể bỏ sót phần chính và tốn thêm token.

Ý tưởng về một “bộ não AI thứ hai” cũng khá thú vị. Thay vì nhập lại thông tin trong mỗi lần hỏi, hệ thống có thể lưu tài liệu, tìm đúng nội dung cần thiết rồi mới gửi cho mô hình. Tôi thấy cách này phù hợp khi cần quản lý ghi chú học tập hoặc tài liệu của một dự án dài hạn.

### AI Assistant cho công việc

Phần Amazon Quick cho thấy trợ lý AI trong doanh nghiệp không chỉ dùng để hỏi đáp. Trợ lý có thể lấy dữ liệu từ nhiều nguồn, hỗ trợ nghiên cứu, tạo báo cáo và thực hiện một số công việc lặp lại. Ví dụ được trình bày là hỗ trợ Project Manager tạo biên bản họp, gửi email và chuẩn bị lịch họp tiếp theo.

Điểm tôi ghi nhớ là khi AI được dùng với dữ liệu nội bộ thì quyền truy cập và bảo mật phải được kiểm soát. Một trợ lý tiện lợi nhưng truy cập sai dữ liệu vẫn có thể gây ra rủi ro.

### CloudFront ở phía trước ứng dụng

Phiên CloudFront giúp tôi hiểu CDN không chỉ có nhiệm vụ làm website tải nhanh hơn. CloudFront còn giảm lượng request đi thẳng về origin, hỗ trợ HTTPS và kết hợp với AWS Shield hoặc AWS WAF để bảo vệ ứng dụng. Nội dung được cache tại edge location nên người dùng có thể nhận dữ liệu từ vị trí gần hơn.

Nội dung này liên quan trực tiếp đến dự án RecruitPro của tôi vì hệ thống cũng sử dụng CloudFront phía trước Application Load Balancer. Sau sự kiện, tôi hiểu rõ hơn lý do nên hạn chế để người dùng truy cập origin trực tiếp.

### Bài học từ LotusHacks

Team VIB chia sẻ quá trình làm sản phẩm UTMorpho trong 36 giờ. Khó khăn không chỉ nằm ở code mà còn ở giới hạn thời gian, token, sự mệt mỏi và việc AI tạo ra nhiều nội dung không cần thiết. Nhóm đã thay đổi hướng tập trung vào chức năng chính và trải nghiệm chỉnh sửa.

Từ phần này, tôi rút ra rằng khi thời gian ít thì không nên cố đưa tất cả ý tưởng vào sản phẩm. Một chức năng chính chạy ổn định và dễ demo sẽ có giá trị hơn nhiều chức năng chưa hoàn thiện.

### Temperature bằng 0 vẫn có thể cho kết quả khác

Phần về tính bất định của LLM làm tôi khá bất ngờ. Dù temperature được đặt bằng 0, cùng một prompt vẫn có thể cho kết quả hơi khác nhau. Nguyên nhân có thể liên quan đến phép tính trên GPU, xử lý song song hoặc cách request được gom thành batch.

Vì vậy, không nên xem kết quả từ LLM là hoàn toàn cố định. Với chức năng quan trọng, hệ thống nên giới hạn định dạng đầu ra, kiểm tra kết quả và có cách xử lý khi nội dung không đúng yêu cầu. Structured output hoặc JSON cũng giúp ứng dụng dễ kiểm tra hơn.

### Hệ thống Multi-Agent trong doanh nghiệp

Phần cuối sử dụng bài toán đánh giá tín dụng startup để giải thích Multi-Agent. Thay vì một agent làm tất cả, hệ thống chia nhiệm vụ cho các agent chuyên về tài chính, thị trường, đội ngũ, rủi ro và tuân thủ. Manager Agent có nhiệm vụ điều phối và tổng hợp kết quả.

Cách chia nhỏ này giúp từng agent tập trung vào một chuyên môn và có thể kiểm tra chéo lẫn nhau. Tuy nhiên, hệ thống doanh nghiệp còn cần giới hạn quyền truy cập, bảo vệ dữ liệu, ghi lại quá trình xử lý và cho phép con người kiểm tra quyết định. Tôi thấy đây là điểm khác biệt lớn giữa một demo AI và một hệ thống có thể sử dụng thực tế.

## Điều tôi học được sau sự kiện

- Chỉ cung cấp context liên quan thay vì đưa thật nhiều thông tin cho AI.
- Viết rõ mục tiêu, giới hạn và định dạng đầu ra trong prompt.
- Dùng CloudFront không chỉ để cache mà còn để hỗ trợ bảo vệ origin.
- Ưu tiên chức năng quan trọng nhất khi làm sản phẩm trong thời gian ngắn.
- Không phụ thuộc vào việc temperature bằng 0 để xem đầu ra LLM là cố định.
- Luôn kiểm tra dữ liệu đầu vào, đầu ra và quyền truy cập của các AI Agent.

## Liên hệ với dự án của tôi

Sau sự kiện, nội dung tôi có thể áp dụng sớm nhất là phần CloudFront. Trong RecruitPro, tôi có thể kiểm tra lại cache behavior, hạn chế truy cập trực tiếp vào origin và tìm hiểu thêm cách kết hợp AWS WAF. Đối với AI, tôi sẽ viết prompt có cấu trúc rõ hơn và không sử dụng kết quả tạo ra ngay khi chưa kiểm tra.

## Minh chứng tham dự sự kiện

![Hình ảnh cá nhân tại FCAJ Community Day](</images/4-EventParticipated/4.1-Event1/check-in-fcaj-community-day.jpg>)

![Hình ảnh chụp trong thời gian diễn ra sự kiện](</images/4-EventParticipated/4.1-Event1/chia-se-cloudfront-bao-ve-ddos.jpg>)

## Kết luận

FCAJ Community Day giúp tôi có thêm góc nhìn thực tế về AI và AWS. Tôi thích nhất phiên CloudFront vì có liên quan trực tiếp đến hệ thống đang triển khai, còn phần LLM và Multi-Agent giúp tôi hiểu rằng ứng dụng AI thực tế cần nhiều lớp kiểm soát hơn một chương trình demo. Đây là những kiến thức tôi có thể tiếp tục tìm hiểu và áp dụng trong các dự án sau này.
