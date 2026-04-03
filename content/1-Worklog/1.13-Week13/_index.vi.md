---
title: "Nhật ký Công việc Tuần 13"
date: "2025-12-01"
weight: 13
chapter: false
pre: " <b> 1.13. </b> "
---
### Mục tiêu Tuần 13:
Hoàn thành dự án và nộp
### Các nhiệm vụ được thực hiện trong tuần này:
| Ngày | Nhiệm vụ | Ngày Bắt đầu | Ngày Hoàn thành | Tài liệu Tham khảo |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Loại bỏ **Map State** để Cách ly **EC2 Instance** trong **Steps Function** <br> - Tạo các **Lambdas** để thêm **policies** vào **EC2 Instance** cho **SSM automation** trong **IR Step Functions** <br> - Cấu hình lại **Quarantine SG**: Thêm **Outbound rule** cho **HTTPS** để kết nối **SSM** <br> - Thay thế **Lambdas** bằng các **States** do **Step Functions** cung cấp: Sử dụng **DescribeIamInstanceProfileAssociation, AttachRolePolicy, DetachRolePolicy** và **StartAutomationExecution** <br> - **CDK**: Tạo **EventBridge** và **Topics** với **subscription emails** được lưu trữ trong **cdk-context** <br> - Họp nhóm: Lập kế hoạch và phân công lại nhiệm vụ để đáp ứng thời hạn mới | 01/12/2025 | 01/12/2025      ||
| 3   | - **CDK**: Thêm cảnh báo **SES** cho **GuardDuty findings** <br> - **CDK**: Thêm **ENI ETL** vào **ETL Pipeline** <br> - Hỗ trợ nâng cấp **dashboard** <br> Cập nhật **Event Participated** và sửa lỗi, cải thiện **Worklog** tổng thể <br> - Nghiên cứu thêm về cách tối ưu hóa **pipeline**, hiện tại **S3 Get Request** cao hơn dự kiến do truy vấn **Athena** kích thước thấp nhưng nhiều đối tượng | 02/12/2025 | 02/12/2025      ||
| 4   | -**CDK**: Nâng cấp Cảnh báo với **Slack** <br> - Kiến trúc: <br> &emsp; + Nghiên cứu và thất bại trong việc sử dụng **SQS** để **pool logs** trước khi gửi đến **Lambda**: **Lambda** vẫn dựa trên sự kiện và vẫn xử lý **log** riêng lẻ thay vì **pooling** <br> &emsp; + Nghiên cứu và thêm **Data Firehose** để hợp nhất **logs** trước khi ghi vào **processed S3** => Giảm số lượng đối tượng được ghi vào **S3** <br> - **IR Step Function** sửa đổi: Loại bỏ các hành động **SSM** do nó yêu cầu kết nối **outbound** sau khi cách ly **EC2** => Thay thế bằng **tagging**, loại bỏ nó khỏi **ASG** và tạo **EBS Snapshot** để phân tích và bảo tồn dữ liệu <br> - Thành viên nhóm cập nhật **CloudWatch ETL** với **Data Firehose** thành công <br> - **CDK**: Cập nhật tất cả **ETL Pipeline** với **Kinesis Firehose** + Đại tu **CloudTrailELT** | 03/12/2025 | 03/12/2025  |  |
| 5   | - Hoàn thành một phần việc viết **Workshop** về tạo **ETL Pipeline** <br> **CDK**: Tạo và cập nhật **Step Functions**: Loại bỏ hoàn toàn **SSM** thay thế bằng **tagging**, bảo vệ chấm dứt (**termination protection**), tách khỏi **ASG** và tạo **snapshot** <br> - Loại bỏ **SQS** giữa **EventBridge** và **StepFunctions** <br> - Cập nhật **Worklog**: **Events**  | 04/12/2025 | 04/12/2025      |  |
| 6   | - Tham gia **BUILDING AGENTIC AI - Context Optimization with Amazon Bedrock Workshop**: Giành được giải thưởng từ **CloudThinker** vì chiến thắng trong **Workshop** <br> - Cập nhật **GuardDuty ETL** và **table** để tối ưu hóa truy vấn <br> - Vẽ lại và cập nhật **Architecture Diagram** <br> Cập nhật **Proposal** sang định dạng mới nhất <br> - Cập nhật **Step Functions States** <br> - Tối ưu hóa cơ sở hạ tầng tổng thể và sửa lỗi | 05/12/2025 | 07/12/2025      | [Tóm tắt và Trải nghiệm Sự kiện](../../4-EventParticipated/4.7-Event7)|


### Thành tựu Tuần 13:
* **Tinh chỉnh và Tối ưu hóa Kiến trúc Cuối cùng**
    * **Tích hợp Kinesis Data Firehose** vào các **ETL pipelines** (bao gồm **CloudWatch** và **CloudTrail**) để hợp nhất **logs** trước khi ghi vào **S3**.
        * Việc thiết kế lại này đã thành công **giảm số lượng đối tượng được ghi vào S3**, tối ưu hóa **pipeline** và giảm chi phí truy vấn **Athena** trong tương lai. 
    * Đại tu **CloudTrail ETL** để hoạt động với cấu hình **Firehose** mới.
    * Thêm **ENI (Elastic Network Interface) ETL** vào **core data processing pipeline**.
    * Hoàn thiện tối ưu hóa cơ sở hạ tầng tổng thể và sửa lỗi trên toàn bộ dự án.
* **Đại tu Quy trình Ứng phó Sự cố (IR)**
    * Hoàn toàn **sửa đổi IR Step Function** để loại bỏ sự phụ thuộc vào các kết nối **outbound** (**SSM**), vốn bị chặn sau khi cách ly.
    * **Workflow** cách ly mới hiện tập trung vào **bảo tồn dữ liệu mạnh mẽ và loại bỏ tài sản** bằng cách:
        * **Tagging** **instance**.
        * Bật bảo vệ chấm dứt (**termination protection**).
        * Tách **instance** khỏi **Auto Scaling Group (ASG)** của nó.
        * Tạo **EBS Snapshot** để phân tích **forensic**.
* **AWS CDK**
    * Hoàn thiện **CDK Stack** cho **IR workflow**, triển khai logic **Step Functions** đã được sửa đổi hoàn toàn.
    * Hoàn thành **CDK deployment** của tất cả các cảnh báo, thêm cả thông báo **SES** và **Slack** cho **GuardDuty findings**.
* **Tài liệu và Tài liệu Workshop**
    * Vẽ lại và cập nhật **Architecture Diagram** để phản ánh tích hợp **Kinesis Firehose** cuối cùng và các thay đổi **IR**.
    * Cập nhật **Proposal** sang định dạng mới nhất và cuối cùng.
    * Hoàn thành một phần việc viết tài liệu **Workshop**.
* **Tham gia Sự kiện**
    * Đã tham gia **BUILDING AGENTIC AI - Context Optimization with Amazon Bedrock Workshop**.
    * Giành được giải thưởng từ **CloudThinker** trong **workshop**.