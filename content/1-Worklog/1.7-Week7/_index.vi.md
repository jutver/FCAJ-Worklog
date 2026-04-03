---
title: "Nhật ký Công việc Tuần 7"
date: "2025-10-20"
weight: 07
chapter: false
pre: " <b> 1.7. </b> "
---
### Mục tiêu Tuần 7:

* Kết nối và làm quen với các thành viên của **First Cloud Journey**.
* Hiểu các dịch vụ **AWS** cơ bản, cách sử dụng **console & CLI**.

### Các nhiệm vụ được thực hiện trong tuần này:
| Ngày | Nhiệm vụ | Ngày Bắt đầu | Ngày Hoàn thành | Tài liệu Tham khảo |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Học các kiến thức cơ bản về **GuardDuty** với "**Getting Hands on with Amazon GuardDuty - AWS Virtual Workshop**" <br> - Làm quen với **GuardDuty** bằng cách sử dụng **Amazon Q** để tạo một **lab** cơ bản: <br> &emsp; + Tạo **sample finding** qua cài đặt <br> &emsp; + Học giao diện **finding** <br> &emsp; + Kiểm thử **EC2** bằng cách quét cổng **scanme.nmap.org** <br> &emsp; + Mô phỏng **DNS exfiltration** trên **EC2** <br> &emsp; + **GuardDuty** không cảnh báo **findings** từ **VPC Flow Logs** như mong đợi <br> &emsp; + Kích hoạt **GuardDuty findings** thông qua **CloudTrail** bằng cách truy cập **API ListPolicies** bằng thông tin xác thực **root** <br> - Học thêm bằng cách làm các **workshop GuardDuty** <br> - Họp nhóm trực tuyến: Phân công các thành viên nghiên cứu các dịch vụ sẽ được sử dụng trong **workshop** | 20/10/2025 | 20/10/2025| [Getting Hands on with Amazon GuardDuty - AWS Virtual Workshop](https://www.youtube.com/watch?v=eq3_H-aiHhk) <br><br> [GuardDuty Workshop](https://catalog.workshops.aws/security/en-US) |
| 3   | - Kích hoạt thành công các cảnh báo mẫu **GuardDuty** với nhiều mức độ nghiêm trọng và loại khác nhau qua **CloudShell CLI** => Môi trường kiểm thử dễ dàng hơn <br> - Tạo một danh sách mối đe dọa tùy chỉnh (**custom threat list**) gồm các **IP** và tên miền cho **GuardDuty** qua các lệnh **CloudShell** mặc dù nó không hoạt động | 21/10/2025 | 21/10/2025      ||
| 4   | - Họp nhóm: <br> &emsp; + Ôn tập nhanh kiến thức **AWS Services** <br> &emsp; + Thảo luận về các thay đổi trong đề xuất <br> - Cập nhật Kiến trúc **AWS**: Thêm **AWS Detective** <br> - Sửa đổi đề xuất: <br> &emsp; + Thêm việc sử dụng **AWS Detective** <br> &emsp; + Thêm kế hoạch cho **CDK** sau khi hoàn thành **workshop** <br> - Đề xuất của cố vấn: <br> &emsp; + Trực quan hóa dữ liệu nhưng không sử dụng **QuickSight**, thay vào đó tạo một **custom-coded dashboard** (Đang nghiên cứu) <br> &emsp; + Lưu **GuardDuty findings** trong **S3 bucket** để phân tích (Đang nghiên cứu) <br> - Cấu hình thành công **EventBridge** để kích hoạt khi có các **GuardDuty findings** cụ thể và: <br> &emsp; + Gửi **SNS emails** đến tất cả các thành viên trong nhóm <br> &emsp; + Kích hoạt một **Lambda script** đơn giản <br> - Xây dựng ý tưởng bổ sung cho **workshop**: Tạo một trang đồ thị dữ liệu đơn giản được **host** trong **S3** và sử dụng **API Gateway** và **Lambda** để kéo dữ liệu **forensics** từ **Amazon Athena** (Đang nghiên cứu)| 22/10/2025 | 22/10/2025      | |
| 5   | - Thử **AWS Card Clash** với các thành viên trong nhóm: Bất ngờ là công cụ tốt để học về các dịch vụ và chức năng của chúng, vị trí của chúng trong Kiến trúc <br> - Ôn tập Kiến thức **AWS Services** cho Giữa kỳ: Sử dụng **Google Gemini** để tạo các bài **quiz** dựa trên các yêu cầu được cung cấp| 23/10/2025 | 23/10/2025      |[AWS Card Clash](https://aws.amazon.com/training/digital/aws-card-clash/)|
| 6   | - Cấu hình thành công danh sách mối đe dọa (**threat list**) của **GuardDuty** để kích hoạt **findings** từ các hoạt động của **EC2 Instance** | 24/10/2025 | 26/10/2025 <br> - Môn học ở trường: <br> &emsp; + **KS57**: Hoàn thành **Pháp luật và đạo đức trong công nghệ số**  |[Pháp luật và đạo đức trong công nghệ số](https://www.coursera.org/account/accomplishments/verify/7JELDK2MGGKL) |


### Thành tựu Tuần 7:

* Thực hành **GuardDuty**:

  * Hoàn thành "**Getting Hands on with Amazon GuardDuty - AWS Virtual Workshop**" và một **lab** chuyên sâu được tạo bằng **Amazon Q**.

  * Tạo, kiểm thử và kích hoạt thành công nhiều **GuardDuty findings** khác nhau thông qua cài đặt console, hoạt động **EC2** và truy cập **API CloudTrail**.

  * Thiết lập một môi trường kiểm thử dễ dàng hơn bằng cách kích hoạt thành công các cảnh báo mẫu với các mức độ nghiêm trọng và loại khác nhau qua **CloudShell CLI**.

  * Cấu hình thành công **GuardDuty threat list** để kích hoạt **findings** từ các hoạt động của **EC2 Instance**.

* Phát triển Đề xuất **Workshop** và Kiến trúc:

  * Cập nhật đề xuất và Kiến trúc **AWS** để tích hợp **AWS Detective** cho khả năng điều tra sâu hơn.

  * Thêm kế hoạch triển khai **CDK** sau khi hoàn thành **workshop**.

  * Bắt đầu nghiên cứu các đề xuất của cố vấn, bao gồm **custom-coded data visualization** và lưu **GuardDuty findings** vào **S3** để phân tích.

  * Xây dựng một ý tưởng **workshop** mới về một trang **data graphing** đơn giản được **host** trong **S3** sử dụng **API Gateway** và **Lambda**.

* Tích hợp Dịch vụ và Tự động hóa:

  * Cấu hình thành công **EventBridge** để hành động dựa trên các **GuardDuty findings** cụ thể.

  * Tự động hóa thông báo bằng cách gửi **SNS emails** đến các thành viên trong nhóm và kích hoạt một **Lambda script** dựa trên cảnh báo **GuardDuty**.