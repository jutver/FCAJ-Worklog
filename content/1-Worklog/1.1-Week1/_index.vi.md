---
title: "Nhật ký Công việc Tuần 1"
date: "2025-09-09"
weight: 01
chapter: false
pre: " <b> 1.1. </b> "
---

### Mục tiêu Tuần 1:

* Kết nối với các thành viên và cố vấn của **FCJ**.
* Tìm hiểu về môi trường làm việc văn phòng.
* Cài đặt **Linux**, học cách sử dụng **Linux** đúng cách.
* Học các kiến thức cơ bản về **AWS**, **console** và **CLI**.
* Hoàn thành **module** một và hai.


### Các nhiệm vụ được thực hiện trong tuần này:
| Ngày | Nhiệm vụ | Ngày Bắt đầu | Ngày Hoàn thành | Tài liệu Tham khảo |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Đọc quy tắc thực tập <br> - Tạo tài khoản **AWS** <br>  - Học **AWS** là gì <br>- Hoàn thành Lab 1 Module 1 (Học cách tạo tài khoản **AWS** và quản lý nhóm người dùng) <br>- Hoàn thành Lab 7 Module 1 (Học cách tạo ngân sách sử dụng dịch vụ) <br>- Lab 7-3 (**Usage Budget**) không thể hoàn thành do lỗi trong **dropdown usage type**, không hiển thị gì <br>- Hoàn thành Lab 9 Module 1 (Học về **AWS Support Services**, loại hình, lợi ích và cách yêu cầu hỗ trợ) | 08/09/2025 | 08/09/2025 | [Create new AWS Account](https://000001.awsstudygroup.com/1-create-new-aws-account/) <br><br> [MFA for AWS Accounts](https://000001.awsstudygroup.com/2-mfa-setup-for-aws-user-root/) <br><br> [Create Admin Group and Admin User](https://000001.awsstudygroup.com/3-create-admin-user-and-group/) <br><br> [Account Authentication Support](https://000001.awsstudygroup.com/4-verify-new-account/) <br><br> [Explore and Configure AWS Management Console](https://000001.awsstudygroup.com/5-explore-and-configure-the-aws-management-console/) <br><br> [Creating Support Cases and Case Management in AWS](https://000001.awsstudygroup.com/6-support-cases/) |
| 3   | - Bắt đầu lý thuyết Module 2: <br>&emsp; + Học về **VPC** (Amazon Virtual Private Cloud)<br>&emsp; + Học về **Subnets** và **Routetable**, **Security Groups**<br>&emsp; + Học về **ENI** và **EIP**<br>&emsp; + Học về **VPC Peering** và **Transit Gateway** <br>&emsp; + Học về **Elastic Load Balancing**<br>&emsp; + Học về **EC2**<br> - Thiết lập trang web cho báo cáo **workshop** <br> - Cài đặt **Hugo** <br> - Viết **worklog** thành công bằng **markdown** và **Hugo** | 09/09/2025 | 09/09/2025 | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Hoàn thành các **lab** của Module 2 <br> - Lab 3: <br>&emsp; + Học về các tài nguyên cần thiết để tạo và chạy các **EC2 instances** <br>&emsp; + Cấu hình và chạy các **EC2 instances** thành công <br>&emsp; + Kết nối và **ping** đến các **EC2 instances** thành công <br>&emsp; + Tạo **NAT Gateway** để cho phép kết nối **EC2 private** <br> - Lab 10: <br>&emsp; + Học cách tạo và sử dụng các cặp khóa (**key pairs**) để bảo mật <br>&emsp; + Học cách cấu hình **security groups** để quản lý kết nối <br>&emsp; + Kết nối và sử dụng **RDP** qua **EC2** thành công <br>&emsp; + Thiết lập **hybrid DNS** với **Route 53 Resolver** (Đang tiến hành, **Cloud Formation template** không tạo **security group** để tiếp tục **lab**) <br> - Lab 19: <br>&emsp; + Tạo **VPC Peering Connection** thành công <br> &emsp; + Học cách cấu hình **Network ACLs** <br> &emsp; + Bật **Cross-Peer DNS** để giải quyết tên **host private** <br> - Tải xuống và sử dụng **MobaXTerm** để kết nối với các **EC2 instances** <br> - Tải xuống và sử dụng **PuTTY** để cấu hình các cặp khóa | 10/09/2025 | 11/09/2025 | [Lab 3](https://000003.awsstudygroup.com/) <br><br> [Lab 10](https://000010.awsstudygroup.com/) <br><br> [Lab 19](https://000019.awsstudygroup.com/) |
| 5   | - Lab 20: <br>&emsp; + Tạo **AWS Transit Gateway** thành công để cho phép kết nối giữa các **VPC** qua một **hub** chung <br>&emsp;&emsp; • Tệp **yaml Cloud Formation template** không được cập nhật, tạo thất bại <br>&emsp;&emsp; • Đã sửa tệp **template**, thay đổi loại **EC2 instance** thành **t3.micro** <br> - Học được bài học đắt giá về việc tại sao cần dọn dẹp tài nguyên sau khi làm **lab**, bị tính phí 12$ **credits** <br> - Xác minh các kế hoạch chi phí và ngân sách hoạt động đúng như dự định, đã được thông báo qua **email**. | 11/09/2025 | 11/09/2025 | [Lab 20](https://000020.awsstudygroup.com/) |
| 6   | - Bắt đầu lý thuyết Module 3 <br>&emsp; + Học về **EBS**, tính năng **Instance store** và kiểm tra **User** và **Meta Data** <br>&emsp; + Học về **Amazon Lightsail** <br>&emsp; + Học về **Elastic File System (EFS)** và **FSx** <br>&emsp; + Học về **MGN** <br>&emsp; + Học cách sử dụng **S3 Buckets** trên **AWS** <br>- Hoàn thành các **lab** của Module 3 <br>- Lab 13: Tạo **Backup Plan** và **Vaults** thành công cho dữ liệu trong **S3 Buckets** <br>&emsp; + Thiết lập thông báo cho các sự kiện **Backup** thành công <br>&emsp; + Khôi phục **backup** thành công <br> - Lab 24: <br>&emsp; + Tạo **storage gateway** <br>&emsp; + Hoàn thành chia sẻ tệp thành công <br> - Lab 57: <br>&emsp; + **Host static website** bằng **S3 Buckets** thành công <br>&emsp; + Cấu hình các công cụ sửa đổi truy cập (**access modifiers**) thành công <br>&emsp; + Cấu hình Tăng tốc **Static Websites** với **Cloudfront** không hoạt động, bỏ qua bước này <br>&emsp; + Tạo **bucket versions** thành công <br>&emsp; + Di chuyển đối tượng giữa các **buckets** <br>&emsp; + Nhân bản **bucket** giữa các **regions**. | 12/09/2025 | 12/09/2025 | [Lab 13](https://000013.awsstudygroup.com/) <br><br> [Lab 24](https://000024.awsstudygroup.com/) <br><br> [Lab 57](https://000057.awsstudygroup.com/)|


### Thành tựu Tuần 1:

* Đã tạo và bảo mật tài khoản **AWS**, bao gồm thiết lập ngân sách và khám phá các dịch vụ hỗ trợ.

* Hoàn thành lý thuyết và các **lab** thực hành cho **VPC**, **Subnets**, **Security Groups**, và **Routetables**.

* Triển khai và kết nối thành công với các **EC2 instances**, cấu hình **NAT Gateway**, và quản lý các kết nối chính bằng **VPC Peering** và **AWS Transit Gateway**.

* Có kinh nghiệm thực hành với **S3 Buckets** (**static website hosting**, quản lý phiên bản, nhân bản), **AWS Backup**, và **Storage Gateway**.

* Thiết lập Tài liệu: Cài đặt **Hugo** thành công và cấu hình trang web để viết **worklog** bằng **markdown**.

* Thành thạo Công cụ: Học cách sử dụng **MobaXTerm** và **PuTTY** để kết nối và quản lý các **EC2 instances**.

* Đã sửa thành công một **CloudFormation template** lỗi thời trong **lab Transit Gateway** và học được cách quản lý chi phí thông qua cảnh báo ngân sách.

* Hoàn thành Module 1 và Module 2, và có một khởi đầu vững chắc cho Module 3.