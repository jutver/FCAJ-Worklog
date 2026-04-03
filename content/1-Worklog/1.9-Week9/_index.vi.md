---
title: "Nhật ký Công việc Tuần 9"
date: "2025-09-09"
weight: 09
chapter: false
pre: " <b> 1.9. </b> "
---
### Mục tiêu Tuần 9:

* Tiếp tục thực hiện **workshop**

### Các nhiệm vụ được thực hiện trong tuần này:
| Ngày | Nhiệm vụ | Ngày Bắt đầu | Ngày Hoàn thành | Tài liệu Tham khảo |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Sửa đổi Kiến trúc **AWS** (**AWS Architecture revised**): <br>&emsp; + Loại bỏ **AWS Detective** <br>&emsp; + Cập nhật với **Step Function Workflow** thay vì một **AWS Lambda Function** đơn lẻ <br>&emsp; + Thêm **Custom Dashboard** (Dashboard Tùy chỉnh): Một trang web **static custom dashboard** được **host** bằng **S3** và sử dụng **Athena** để truy vấn từ **data lake** <br> - Môn học ở trường: <br> &emsp; + **KS57**: Hoàn thành **Quản trị dự án và duy trì đổi mới trong chuyển đổi số** | 03/11/2025 | 03/11/2025 | [Quản trị dự án và duy trì đổi mới trong chuyển đổi số](https://www.coursera.org/account/accomplishments/verify/IC06JCSZ7AVG) |
| 3   | - **Export GuardDuty Findings** thành công sang **S3 Bucket** <br> - Thử nghiệm với **AWS Glue Crawler**: <br>&emsp; + Thất bại trên **CloudWatch** và **CloudTrail logs**, **schema** quá phức tạp đối với **Crawler** (Cần nghiên cứu cách thay thế) <br>&emsp; + Chạy thành công trên các **GuardDuty Findings** đã được **export**: Phải cập nhật **KMS Policy** để cho phép **Crawler** giải mã dữ liệu <br> - Nghiên cứu **ETL Pipeline** cho **logs**| 04/11/2025 | 04/11/2025      | |
| 4   | - Họp nhóm: Báo cáo tiến độ: <br>&emsp; + **IR Workflow**: Hoàn thành một nửa, chức năng cách ly **EC2 (EC2 quarantine function)** đã xong, chưa kiểm thử với **findings** <br>&emsp; + Giao nhiệm vụ thiết kế **frontend dashboard** <br>&emsp; + Giao nhiệm vụ nghiên cứu **Glue ETL Pipeline** <br>&emsp; + Đăng ký tham gia **VPBank Cloud Day 2025** cùng các thành viên trong nhóm | 05/11/2025 | 05/11/2025 || 
| 5   | - Họp nhóm <br> - Nghiên cứu phương pháp tiếp cận **ETL Pipeline**: <br>&emsp; + Thay vì sử dụng **Glue ETL Jobs**, chúng tôi sử dụng một **custom Lambda ETL pipeline** cho **CloudTrail** và **CloudWatch logs** <br>&emsp; + Lưu **raw logs** vào một **Raw Log S3 Bucket** sau đó sử dụng **ETL Lambda** để xử lý dữ liệu và ghi nó vào một **Processed Data S3** để sau đó được **Crawl** <br> - Sửa đổi Kiến trúc **AWS**: Thêm một nhóm mới: nhóm **DATA PREP** chứa **Raw Log S3 Bucket** và **ETL Lambda** <br>- Môn học ở trường: <br> &emsp; + **ENW493c**: Hoàn thành **Advanced Writing** | 06/11/2025 | 06/11/2025      | [Advanced Writing](https://www.coursera.org/account/accomplishments/verify/EDQ1NY2UG063) |
| 6   | - Nghiên cứu **Kinesis Data Firehose** để thu thập **logs**: Tốt cho việc sử dụng trong tương lai, không phù hợp cho dự án hiện tại vì **real-time streaming data** không cần thiết, sử dụng **batch processing** tốt hơn <br> - Xây dựng thành công **ETL Pipeline** cho **CloudTrail logs**: Được kích hoạt bởi việc tạo **object** trong **CloudTrail Raw Log Bucket** và định dạng lại **raw logs** thành **JSONL** và lưu nó vào **Processed S3** <br> - **Crawl** và truy vấn thành công **log** đã xử lý để hiển thị **CloudTrail Events** | 07/11/2025 | 07/11/2025      | |


### Thành tựu Tuần 9:

* **Tinh chỉnh Kiến trúc**:

  * Cập nhật cơ chế Ứng phó Sự cố (**IR**) để sử dụng **Step Functions Workflow** thay vì một hàm **Lambda** đơn lẻ.

  * Giới thiệu **Custom Dashboard** (trang web tĩnh được **host** trên **S3**) sử dụng **Athena** để truy vấn **data lake**.
  
  * Tạo một nhóm **DATA PREP** mới trong kiến trúc, bao gồm **Raw Log S3 Bucket** và **ETL Lambda** để quản lý chuyển đổi **log**.

* Cấu hình thành công **pipeline** để **export GuardDuty Findings** sang **S3 Bucket**.

* Xây dựng và triển khai **custom ETL Lambda pipeline** để xử lý **CloudTrail logs**, được kích hoạt bởi các **object** mới trong **Raw Log S3 Bucket**.

* **Crawl** và truy vấn thành công **CloudTrail logs** đã xử lý bằng **Glue/Athena** để hiển thị **CloudTrail Events**.

* Các thành viên trong nhóm đã hoàn thành một nửa **IR Step Functions Workflow**, với chức năng cách ly **EC2 (EC2 quarantine function)** đã xong.

* Giao nhiệm vụ thiết kế **frontend dashboard** và nghiên cứu **Glue ETL Pipeline**.

* Đã đăng ký tham gia sự kiện **VPBank Cloud Day 2025** cùng các thành viên trong nhóm.