---
title: "Nhật ký Công việc Tuần 11"
date: "2025-11-17"
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu Tuần 11:

* Tinh chỉnh dự án.


### Các nhiệm vụ được thực hiện trong tuần này:
| Ngày | Nhiệm vụ | Ngày Bắt đầu | Ngày Hoàn thành | Tài liệu Tham khảo |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Tham gia **AWS Cloud Mastery Series #2 - DevOps on AWS**: Thu được nhiều giá trị tốt về **CDK** và **CloudFormation** cho dự án, nhận được một số khuyến nghị từ cố vấn về chiến lược **demo**, viết về trải nghiệm sự kiện | 17/11/2025 | 17/11/2025      |[Tóm tắt và Trải nghiệm Sự kiện](../../4-EventParticipated/4.4-Event4)|
| 3   | - Tổng quan **Dashboard**: Cập nhật thêm các trường hiển thị ban đầu <br> - Sửa đổi Kiến trúc: <br>&emsp; + Loại bỏ **Crawler** khỏi kiến trúc <br>&emsp; + Thêm **SQS** giữa **EventBridge** và **StepFunctions**  <br> - Ghi nhận chi phí của các cuộc gọi **S3 API**, đặc biệt là **S3 Bucket** cho **CloudTrail logs**. **Lambda** được cấu hình để xử lý mọi **CloudTrail log**, dẫn đến số lượng lớn cuộc gọi **S3 GET**, vì vậy chúng tôi phải cập nhật chi phí tương ứng <br> - Thành viên nhóm đã cách ly **EC2** thành công trong môi trường kiểm thử <br> - Nâng cấp thành công **GuardDuty ETL Lambda** để tạo **table** mà không cần **Crawler** và trả về các trường chi tiết hơn <br> - Thành viên nhóm đã nâng cấp thành công **CloudWatch ETL Lambda** để tạo **table** mà không cần **Crawler**. Tôi đã giúp tạo **trigger** và cập nhật mã **Lambda** để xử lý tệp **exported** mới <br> Sao lưu mã **Lambda**| 18/11/2025 |18/11/2025 ||
| 4   | - Tham gia **Secure Your Applications: AWS Perimeter Protection Workshop**: Học thêm về **CloudFront** và **WAF** và được giới thiệu về **CloudFront pricing tier** hoàn toàn mới, đã làm hai **workshop** về **CloudFront** và **WAF** <br> - Học cách thiết lập **API Gateway RestAPIs** để chuẩn bị tích hợp với **dashboard** | 19/11/2025 | 19/11/2025  |[Tóm tắt và Trải nghiệm Sự kiện](../../4-EventParticipated/4.5-Event5)|
| 5   | - Được mời về trường dự Ngày Nhà giáo <br> - Việc gia đình | 20/11/2025 | 20/11/2025      ||
| 6   | - Được mời tham dự Ngày Tốt nghiệp của **FPT** bởi các cử nhân tốt nghiệp <br> - Nghiên cứu về **CDK**: Cách cài đặt, cách sử dụng, cách cấu hình **stacks** để chuẩn bị cho kế hoạch tuần tới | 21/11/2025 | 23/11/2025 | [AWS CDK Github](https://github.com/aws/aws-cdk) <br><br> [AWS CDK Document](https://docs.aws.amazon.com/cdk/v2/guide/home.html) |


### Thành tựu Tuần 11:
* **Tinh chỉnh Kiến trúc và Tối ưu hóa Chi phí**
    * Loại bỏ thành công dịch vụ **Glue Crawler** khỏi kiến trúc bằng cách nâng cấp các **ETL Lambdas** để trực tiếp tạo **Glue Catalog Tables**.
        * Đã nâng cấp **GuardDuty ETL Lambda** và hỗ trợ nâng cấp **CloudWatch ETL Lambda** để tạo **table** mà không cần **Crawler**.
    * Thêm **SQS (Simple Queue Service)** giữa **EventBridge** và **Step Functions** để cải thiện độ tin cậy và sự tách rời của quy trình làm việc.
    * Xác định chi phí tiềm năng cao liên quan đến các cuộc gọi **S3 API GET** do việc xử lý tất cả **CloudTrail logs** và ghi nhận để cập nhật chi phí tương ứng.
* **Phát triển Ứng phó Sự cố (IR) và Dashboard**
    * Thành viên nhóm đã đạt được việc **cách ly EC2 (EC2 isolation)** thành công trong môi trường kiểm thử, xác nhận một chức năng **IR** quan trọng.
    * Cập nhật **dashboard overview** để bao gồm nhiều trường chi tiết và hiển thị ban đầu hơn.
    * Học cách thiết lập **API Gateway RestAPIs** để chuẩn bị tích hợp với **custom dashboard**.
* **Tham gia Sự kiện**:
    * Đã tham gia **AWS Cloud Mastery Series #2 - DevOps on AWS**.
    * Đã tham gia **Secure Your Applications: AWS Perimeter Protection Workshop**, hoàn thành hai **workshop** về **CloudFront** và **WAF**.