---
title: "Nhật ký Công việc Tuần 12"
date: "2025-11-24"
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---
### Mục tiêu Tuần 12:

* Kết nối và làm quen với các thành viên của **First Cloud Journey**.
* Hiểu các dịch vụ **AWS** cơ bản, cách sử dụng **console & CLI**.

### Các nhiệm vụ được thực hiện trong tuần này:
| Ngày | Nhiệm vụ | Ngày Bắt đầu | Ngày Hoàn thành | Tài liệu Tham khảo |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Cài đặt **AWS CDK** thành công với **AWS CLI** <br> Hoàn thành hướng dẫn tạo ứng dụng đầu tiên với **CDK**: <br>&emsp; + Triển khai **stacks** trên **AWS Accounts** <br>&emsp; + Sử dụng **diff** để so sánh các thay đổi <br>&emsp; + **Destroy stack** sau khi hoàn thành <br> - Tạo **Github Organization** cho nhóm | 24/11/2025 | 24/11/2025      |[CDK Tutorial](https://docs.aws.amazon.com/cdk/v2/guide/hello-world.html)|
| 3   | - Thêm vào **IR Step Functions**: Thêm **Map State** để lặp qua các **Isolated Instances** và kích hoạt **SSM Lambda** cho các **Instances** đó để thu thập **logs** từ chúng cho **forensics** <br> - Hỗ trợ thành công việc tạo **auto export CloudWatch logs**: Sử dụng **Lambda** để phân tích **subscription filter** từ **log stream** đến **Raw Log S3 bucket**, sẽ phải sửa đổi **CloudWatch ETL Lambda** để hoạt động với **auto export** mới thay vì **batch export job** <br> - Cập nhật **CloudTrail ETL Lambda**: Nhận thấy chi phí lưu trữ cao bất thường trong **Processed CloudTrail Log bucket** => **Lambda Function** hiện tại lưu tệp dưới dạng **.jsonl** chưa **unzip** => Cập nhật **function** để các tệp được nén bằng **gzip** trước khi lưu <br> - **CloudTrail ETL Lambda** có một số lỗi và lần gọi đột biến khi nhiều người tương tác với tài khoản => Tăng giới hạn **timeout** <br> **CDK**: Di chuyển môi trường kiểm thử **CDK** sang một tài khoản mới <br> - **CDK**: Tạo một **Stack** cho phép **GuardDuty** và **CloudTrail** cùng với **Raw Log S3 Bucket**   | 25/11/2025 | 25/11/2025      ||
| 4   | - **CDK**: Cập nhật **Bucket** và **CloudTrail Policy** để tái tạo cơ sở hạ tầng hiện tại: gặp phải **circular dependencies** nhưng đã được giải quyết <br> **CDK**: Tái tạo thành công **CloudTrail ETL pipeline** với **Raw** và **Processed log buckets**, **ETL Lambda** và **Glue table** để được truy vấn bằng **Athena** và đặt các **policies** liên quan | 26/11/2025 | 26/11/2025      | |
| 5   | - **CDK**: Cấu hình **CloudWatch**, **Log Group**, **DNS Query logging**, thêm **cdk-context** để người dùng nhập **VPC ids** nhằm thêm **logging** cho phân tích <br> - Tối ưu hóa: **CloudTrail logs** đã quá nhiều, kiểm tra nhanh cho thấy nó cũng **log S3 Put events** từ các **ETL Lambdas**, gây ra một vòng lặp => Tạo **custom event exclusion** trong tab **CloudTrail Events** để loại trừ các **API** được gọi bởi các **ETL Lambdas** <br> - Loại trừ sự kiện theo **Lambda's ARN** không đáng tin cậy => Loại trừ **API** từ **log buckets** <br> - **CDK**: Không thể cấu hình **advanced event selectors** trong **CDK** nên điều đó sẽ phải được loại bỏ <br>- **CDK**: Cấu hình thành công **CloudWatch Auto Export Lambda** và **Subscription Filter**: Gặp nhiều lỗi quyền từ **Subscription Filter permission** để gọi **Lambda** => Sử dụng **L2 construct** và **explicit dependency** cho **_create_subscription_filter**  | 27/11/2025 | 27/11/2025 | |
| 6   | - **CDK**: Thêm **CloudWatch ETL** và **Glue Table** liên quan cùng **Processed Bucket**  <br> -**CDK**: Thêm **KMS Key** để cho phép **GuardDuty** **export findings** sang **S3 Bucket** và thêm **GuardDutyETL** để xử lý các **findings** cho việc truy vấn => Hoàn thành đầy đủ **ETL Pipeline** và **Data Forensics** <br> - Họp nhóm: <br>&emsp; + Giao nhiệm vụ **CDK** cho các thành viên <br>&emsp; + Bắt đầu cập nhật đề xuất và sơ đồ kiến trúc <br> - Sửa và cải thiện **IR Step Functions**: <br>&emsp; + Sửa **EC2Isolate Lambda**: Phương pháp **parsing** sai <br>&emsp; + Cải thiện **state**: Thêm **Parsing Lambda** và sắp xếp lại các chức năng <br>&emsp; + **SSM** Thất bại do thiếu **IAM**: **Role** sẽ được thêm vào **SSM Forensics Function** <br> - Tham gia **AWS Cloud Mastery Series #3: AWS Well-Architected – Security Pillar Workshop**   | 28/11/2025 | 30/11/2025  |[Tóm tắt và Trải nghiệm Sự kiện](../../4-EventParticipated/4.6-Event6)|


### Thành tựu Tuần 12:
* **AWS CDK**
    * Cài đặt và học các kiến thức cơ bản về **AWS CDK** thành công và hoàn thành hướng dẫn giới thiệu, bao gồm triển khai **stack**, so sánh thay đổi (**diff**), và hủy (**destruction**).
    * Tạo **GitHub Organization** cho nhóm.
    * Phát triển và triển khai cơ sở hạ tầng **ETL** nền tảng bằng **CDK**, bao gồm:
        * **Stacks** để kích hoạt **GuardDuty** và **CloudTrail**, cùng với **Raw Log S3 Bucket** cần thiết.
        * Tái tạo thành công **CloudTrail ETL pipeline** hoàn chỉnh (**Raw/Processed buckets**, **ETL Lambda**, **Glue Table**, và các **policies** liên quan).
        * Cấu hình các thành phần **CloudWatch logging** (**Log Group**, **DNS Query logging**) và **CloudWatch Auto Export Lambda** sử dụng **L2 construct** để giải quyết lỗi quyền **subscription filter**.
        * Hoàn thành đầy đủ **ETL pipeline** và **Data Forensics** bằng cách thêm **CloudWatch ETL**, **GuardDuty ETL**, các **Glue Tables** liên quan, và cấu hình **KMS Key** cho **GuardDuty export**.
* **Tối ưu hóa ETL Pipeline và Giảm Chi phí**
    * Cập nhật **CloudTrail ETL Lambda** để nén tệp bằng **gzip** trước khi lưu vào **Processed S3 Bucket**, giảm đáng kể chi phí lưu trữ.
    * Giải quyết các lỗi và lần gọi đột biến trong **CloudTrail ETL Lambda** bằng cách **tăng giới hạn timeout**.
    * Tối ưu hóa **CloudTrail logging** bằng cách tạo **custom event exclusions** để ngăn chặn việc **log S3 Put events** được kích hoạt bởi các **ETL Lambdas**, giải quyết một vòng lặp **logging** tiềm năng.
* **Cải tiến Quy trình Ứng phó Sự cố (IR) Workflow**
    * Cải tiến **IR Step Functions Workflow** bằng cách thêm **Map State** để lặp lại các **isolated instances** và kích hoạt **SSM Lambda** để thu thập **logs** cho **forensics**.
    * Sửa **EC2 Isolate Lambda** (phương pháp **parsing** không chính xác) và cải thiện **state** **workflow** tổng thể bằng cách thêm **Parsing Lambda** và sắp xếp lại các chức năng.
    * Xác định và ghi nhận nhu cầu thêm **IAM role** chính xác vào **SSM Forensics Function** để giải quyết các lỗi **SSM**.
    * Hỗ trợ tạo cơ chế **CloudWatch log auto-export** thông qua **subscription filter** và **Lambda**.
* **Tham gia Sự kiện**
    * Đã tham gia **AWS Cloud Mastery Series #3: AWS Well-Architected – Security Pillar Workshop**.