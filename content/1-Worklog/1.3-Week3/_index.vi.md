---
title: "Nhật ký Công việc Tuần 3"
date: "2025-09-22"
weight: 03
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu Tuần 3:

* Hoàn thành Module 5
* Hỗ trợ đồng đội với các **lab** trước đó
* Thực hiện lại các **lab** không khả dụng với các gói miễn phí (**free tiers**)
* Thực hiện 2 nghiên cứu bổ sung
* Thảo luận ý tưởng dự án

### Các nhiệm vụ được thực hiện trong tuần này:
| Ngày | Nhiệm vụ | Ngày Bắt đầu | Ngày Hoàn thành | Tài liệu Tham khảo |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   |- Lab 25: Không thể thực hiện hiện tại, tài khoản đang ở **free tier** <br> - Nâng cấp tài khoản lên gói trả phí <br> - Thử lại **lab** 25: <br>&emsp; + **Template** được cung cấp sử dụng **runtime nodejs12.x** cho các hàm **Lambda**, không còn được hỗ trợ, đã sửa bằng cách thay đổi thành **nodejs20.x** <br>&emsp; + Tạo **FSx file system** <br>&emsp; + **Endpoint S3 bucket** để kiểm thử dữ liệu chỉ có thể truy cập ở **region US**, vì vậy phải thay đổi thành **Read-S3Object -BucketName nasanex -KeyPrefix /AVHRR -Folder Z:/nasanex/AVHRR -Region us-west-2** <br>&emsp; + Tạo **file shares** <br>&emsp; + Tạo **HDD** và **SSD FSx** <br>&emsp; + 25.4: Phiên bản công cụ được cung cấp đã lỗi thời, đã tải xuống phiên bản mới nhất <br>&emsp; + Kiểm thử hiệu suất ổ đĩa thành công với nhiều tham số khác nhau <br>&emsp; + Giám sát hiệu suất bằng **CloudWatch**: **Alarm** được kích hoạt, **throughput** đạt tối đa 400MB <br>&emsp; + Học cách **deduplicate files**:<br>&emsp;&emsp; • Lịch trình **dedup** mặc định là mỗi Thứ Bảy <br>&emsp;&emsp; • Chạy **dedup** ban đầu không tối ưu hóa gì do **fileAge** mặc định -> đã thay đổi thành 0 => Tối ưu hóa một nửa số tệp <br>&emsp; + Tạo **shadow copies** để **backup** <br>&emsp; + Học cách quản lý các tệp đang mở và cách đóng chúng từ kết nối <br>&emsp; + Tạo thành công **user quotas** để quản lý dung lượng lưu trữ <br>&emsp; + Bật chia sẻ tệp **Continuously Available (CA)** trên **Amazon FSx** để nhiều người dùng có thể sử dụng cùng lúc <br>&emsp; + Mở rộng **throughput** và **storage** trên **AWS Console** <br> - Học mô hình trách nhiệm chia sẻ (**shared responsibility model**): Cả nhà cung cấp và khách hàng đều có trách nhiệm về bảo mật <br> - Module 5-2: **Best practice** là tạo một **admin IAM user** thay vì sử dụng tài khoản **root** <br> - **IAM Principal**: Truy cập tài nguyên trong **AWS Account** <br> - **IAM Policy**: **Identity based** và **Resource based** <br> - **IAM Role**: Một tập hợp các quy tắc kiểm soát quyền truy cập vào tài nguyên và dịch vụ cho **IAM User** <br> - **IAM Role** có thể được sử dụng để bật **cross account** <br> - Môn học ở trường: <br>&emsp; + **ENW493c**: Hoàn thành **Understanding Research Methods**| 22/09/2025 | 22/09/2025      | [Lab25](https://000025.awsstudygroup.com/1-introduce/) <br><br> [Understanding Research Methods](https://www.coursera.org/account/accomplishments/verify/463JCBE1NHYH)   |
| 3   | - Module 5: <br>- **Amazon Cognito**: Một dịch vụ quản lý xác thực, quyền và người dùng, với hai tính năng chính: <br>&emsp; + **User pool**: Một tập hợp các tài khoản người dùng và thông tin xác thực, cho phép các dịch vụ xác thực bên thứ ba <br>&emsp; + **Identity pools**: Một ánh xạ các quyền và thông tin xác thực có thể được áp dụng cho người dùng <br> - **AWS Organization**: Quản lý nhiều **AWS Accounts** và tài nguyên <br>&emsp; + Tổ chức các tài khoản theo **OU** và sử dụng **Service Control Policies** để xác định quyền cho người dùng trong tổ chức <br> **AWS Identity Center (SSO)**: Quản lý Ủy quyền **AWS** và Ứng dụng: <br>&emsp; + Tận dụng các **permission sets** <br> - **AWS KMS**: Tạo và quản lý các khóa mã hóa: <br>&emsp; + **CMK (Customer Managed Key)** là tài nguyên chính, được sử dụng để tạo, mã hóa và giải mã **Data Key** <br> - **AWS Security Hub**: Quét và kiểm thử các chính sách và **best practices** dựa trên bảo mật <br>- Tiếp tục với **lab** 14: <br>&emsp; + Tạo **role** và **S3 Bucket** <br>&emsp; + Phiên bản **Ubuntu** mới nhất (25.04) bao gồm phiên bản **kernel** không được hỗ trợ, yêu cầu cài đặt lại để tiếp tục <br>&emsp; + Cài đặt **Ubuntu** 24.04: Thất bại, **kernel** của nó vẫn không được hỗ trợ <br>&emsp; + Cài đặt **Ubuntu** 22.04 <br>&emsp; + **Import VM** vào **AWS** thành công <br>&emsp; + Kết nối thành công với **EC2 instance** được tạo từ **AMI** bằng tên người dùng và mật khẩu của **VM**    | 23/09/2025 | 23/09/2025      | [Lab 14](https://000014.awsstudygroup.com/) |
| 4   | Tiếp tục với **lab** 14: <br>&emsp; + Tạo **export bucket**, cấu hình quyền <br>&emsp; + **Export instances** thành công sang định dạng **.OVA** để sử dụng <br>- Lab 18: Bật **Security Hub** và cấu hình **AWS Config** để ghi lại dữ liệu để phân tích (Có thể mất một thời gian dài để điểm số được tính toán) | 24/09/2025 | 24/09/2025      | [Lab 14](https://000014.awsstudygroup.com/) |
| 5   | - Lab 22: <br>&emsp; + Tạo các hàm **Lambda** để chạy và dừng các **EC2 instances** dựa trên lịch trình và **tags** <br>&emsp; + Ghi nhật ký thông báo qua **Slack** <br> - Lab 28:<br>&emsp; + Tạo các **IAM policies** và **role**, chỉ cho phép truy cập từ **Singapore Region** (**ap-southeast-1**) <br>&emsp; + Hạn chế truy cập **EC2** từ các **regions** bên ngoài chính sách <br>&emsp; + Hạn chế tạo các **EC2 instances** mà không có **tags** hợp lệ <br> Lab 30: Hạn chế **IAM user** chỉ sử dụng **region** được chỉ định để truy cập **EC2** <br> - Lab 18 (Cập nhật): **Security** quét xong, đạt điểm bảo mật 85%, 1 lỗ hổng nghiêm trọng: **IAM User** có **administrative access policy** <br>- Lab 33: <br>&emsp; + Tạo **Key Management Service** <br>&emsp; + Thiết lập **CloudTrail** để ghi nhật ký dữ liệu trong **S3 Bucket** <br>&emsp; + Tạo **Athena** để truy vấn **logs** <br>&emsp; + **KMS** từ chối truy cập thành công đối với người dùng không có ủy quyền | 25/09/2025 | 25/09/2025      | [Lab 22](https://000022.awsstudygroup.com/) <br><br> [Lab 28](https://000028.awsstudygroup.com/) <br><br> [Lab 30](https://000030.awsstudygroup.com/) <br><br> [Lab 18](https://000018.awsstudygroup.com/) <br><br> [Lab 33](https://000033.awsstudygroup.com/)  |
| 6   | - Lab 44: Cấu hình điều kiện **role**, hạn chế truy cập bằng **IP**, thời gian và các yếu tố khác <br> - Lab 48:<br>&emsp; + Sử dụng **IAM access key** để tải tệp lên **S3** qua **EC2 Instance** <br>&emsp; + Tải tệp lên **S3** qua **EC2 Instance** mà không cần **access key** bằng cách sử dụng **IAM Roles** <br> - Lab 12: <br>&emsp; + Tạo **AWS Organization** <br>&emsp; + Tạo các tài khoản và chuyển chúng vào các đơn vị (**units**) <br>&emsp; + Mời các tài khoản vào tổ chức <br>&emsp; + Chuyển đổi **roles** cho các tài khoản thuộc tổ chức <br>&emsp; + Thiết lập các **policies** cho các tài khoản thuộc tổ chức <br>&emsp; + Cài đặt **Python** để tiếp tục **lab** <br>&emsp; + Tạo và cấu hình người dùng và nhóm bằng **Identity Store APIs** qua **AWS CLI** <br> Các **lab** từ **AWS for Microsoft Workloads**: <br>&emsp; + Quản lý người dùng và nhóm trên **Microsoft AD** qua **AWS CLI** <br>&emsp; + Học cách khắc phục sự cố các **EC2 instances** bằng cách tách các **volumes** của **instance** bị lỗi và gắn nó vào một **instance** đang chạy khác để cấu hình và khắc phục sự cố <br>&emsp; + Học cách gắn các **licenses** vào các **EC2 instances** với **Microsoft AD**, **demo** với **LibreOffice**   | 26/09/2025 | 26/09/2025      | [Lab 44](https://000044.awsstudygroup.com/) <br><br> [Lab 48](https://000048.awsstudygroup.com/) <br><br> [Lab 12](https://000012.awsstudygroup.com/) <br><br> [Microsoft Workloads](https://www.youtube.com/playlist?list=PLhr1KZpdzukdJllxulUM7pMB7aJ2_FfTP) |


### Thành tựu Tuần 3:

* Nâng cấp tài khoản **AWS** thành công để hoàn thành các **lab** trước đây không khả dụng trên **Free Tier** và học cách điều chỉnh tài nguyên, chẳng hạn như sửa các phiên bản **Lambda runtime** lỗi thời.

* **Advanced Storage (FSx)**: Hoàn thành Lab 25, tạo và cấu hình **Amazon FSx file system**. Đạt được các kỹ năng thực tế trong việc quản lý **data deduplication**, tạo **shadow copies** để **backup**, đặt **user quotas** và mở rộng **throughput** đồng thời giám sát hiệu suất với **CloudWatch**.

* Hoàn thành lý thuyết Module 5 và các **lab** bảo mật chuyên sâu:

  *  Học các khái niệm về **IAM**, **Roles**, **Policies**, **Cognito**, **Organizations**, **Identity Center (SSO)**, và **KMS**.

  *  Triển khai các **Region Restriction policies** (Lab 28 & 30) cho việc tạo và truy cập **EC2**.

  *  Cấu hình **Role Conditions** để hạn chế truy cập dựa trên **IP** và thời gian (Lab 44).

  *  Thực hành bảo mật việc tải tệp lên **S3** bằng cách sử dụng **IAM Roles** thay vì **access keys** (Lab 48).

* Bật **Security Hub** và **AWS Config** (Lab 18), đạt điểm bảo mật 85% và xác định một lỗ hổng nghiêm trọng (**IAM User administrative access**).

* Tạo các hàm **Lambda** để lên lịch bắt đầu và dừng các **EC2 instances** dựa trên **tags** (Lab 22) và ghi nhật ký thông báo qua **Slack**.

* Giải quyết thành công các vấn đề tương thích **kernel** bằng cách chọn phiên bản **Ubuntu** chính xác (22.04), **import** một **VM** vào **AWS**, tạo **AMI**, và **export instance** trở lại định dạng **.OVA** (Lab 14).

* Thiết lập **AWS Organization**, tạo **Organizational Units (OUs)** và tài khoản, cấu hình **Service Control Policies**, và thực hành chuyển đổi **roles** cho các tài khoản (Lab 12).

* **AWS for Microsoft Workloads**: Hoàn thành các **lab** bổ sung tập trung vào:

  *  Quản lý người dùng/nhóm trong **Microsoft AD** qua **AWS CLI**.

  *  Khắc phục sự cố **EC2** nâng cao bằng cách tách và gắn lại các **volumes**.

  *  Gắn các **licenses** vào các **EC2 instances** bằng **Microsoft AD** (đã **demo** với **Libre Office**).

* Thiết lập **CloudTrail** để ghi nhật ký dữ liệu vào **S3** và sử dụng **Amazon Athena** để truy vấn các **logs** này cho phân tích kiểm tra và bảo mật (Lab 33).