---
title: "Nhật ký Công việc Tuần 10"
date: "2025-11-10"
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu Tuần 10:
* Nghiên cứu và kiểm thử đầy đủ tất cả các thành phần và sẵn sàng kết hợp để xây dựng **workshop**

### Các nhiệm vụ được thực hiện trong tuần này:
| Ngày | Nhiệm vụ | Ngày Bắt đầu | Ngày Hoàn thành | Tài liệu Tham khảo |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Hỗ trợ xây dựng **ETL Pipeline** cho **CloudWatch logs** cùng thành viên nhóm <br> -  Cập nhật đề xuất:<br>&emsp; + Bao gồm Kiến trúc và Dịch vụ đã cập nhật <br>&emsp; + Tính toán lại chi phí | 10/11/2025 | 10/11/2025      ||
| 3   | - Hoàn thành xây dựng **ETL Pipeline** cho **CloudWatch logs** <br> - Sửa **ETL Pipeline** cho **CloudTrail logs**: **Logs** được xử lý từ các ngày khác nhau gây lỗi **schema** do thứ tự trường ngẫu nhiên trong kiểu dữ liệu **struct** <br> - Sử dụng **AWS SSM** thành công để lấy **EC2 system logs** sau các Phản hồi **IR** <br> - Tích hợp thành công các **chatbot** thông báo mối đe dọa trong **Slack** và **Telegram** <br> - Hiển thị thành công các thông báo được định dạng dựa trên **live threat findings** <br> Bị gửi hơn 1000 **emails** vì thành viên nhóm đã kích hoạt tất cả **GuardDuty sample findings** kết hợp với nhiều lần kiểm thử **SNS** <br> - Thành viên nhóm đề xuất thêm **SES (Simple Email Service)** để định dạng và gửi **emails**| 11/11/2025 | 11/11/2025 ||
| 4   |- Nghiên cứu **CloudTrail Lake**: Tốt cho việc sử dụng trong tương lai cụ thể là để phân tích **CloudTrail log** chuyên sâu, bị coi là không cần thiết cho dự án hiện tại do nó chỉ dành riêng cho **CloudTrail** <br> - Cập nhật **CloudTrail ETL Lambda**: **promote fields** trong **request parameters** thành các cột để truy vấn tốt hơn và ít lỗi **schema crawling** hơn => **Crawl** dữ liệu đã xử lý giữa các ngày một cách đáng tin cậy <br> - Các thành viên nhóm bắt đầu thiết kế trang **dashboard**, đề xuất tích hợp **Grafana** <br> - Thành viên nhóm hoàn thành **Lambda IR Functions** <br> - Bắt đầu cập nhật đề xuất sang định dạng mới| 12/11/2025 | 12/11/2025      ||
| 5   | - Kiểm thử thành công việc sử dụng **Lambda** để truy vấn với **Athena** nhằm chuẩn bị cho **API Gateway** cho **Dashboard** <br> - Việc gia đình | 13/11/2025 | 13/11/2025      | [Lambda Athena Query Guide](https://www.youtube.com/watch?v=a_Og1t3ULOI)|
| 6   | - Việc **crawling raw GuardDuty exported logs** cho thấy là một ý tưởng tồi, một số lượng lớn lỗi **schema** <br> - Xây dựng một **Lambda ETL Pipeline** cho **GuardDuty logs** <br> - Sửa đổi kiến trúc: <br>&emsp; + Định hướng **log** từ **GuardDuty** đến **Raw Log S3 Bucket** để trải qua **ETL Pipeline** <br>&emsp; Thêm **SES** theo đề xuất của thành viên nhóm <br> - Nghiên cứu các kiến trúc thay thế: Chúng tôi có thể loại bỏ hoàn toàn **Crawler**, do **custom Lambda ETL pipeline** mà chúng tôi đã tạo, chúng tôi đã thực hiện hầu hết các dịch vụ của **Crawler**. **Crawler** chủ yếu được sử dụng cho số lượng lớn **logs** với nhiều loại dữ liệu khác nhau, ngoại trừ kiểu dữ liệu **struct** dường như, mà **CloudWatch, CloudTrail** và **GuardDuty logs** có rất nhiều. Sau khi định dạng **logs** thành **Parquet** bằng **custom Lambda ETL**, mục đích của **Crawler** bây giờ là biến nó thành một **Catalog Table**, mà thay vào đó có thể được thực hiện bằng **Lambda**. Sẽ kiểm thử phương pháp thay thế này. <br> - Cập nhật thành công **CloudTrail ETL Pipeline** để trực tiếp gọi **Glue API** tạo **table** mà không cần sử dụng **Crawler** <br> - Đưa việc sử dụng **KMS** vào dự án do tính chất nhạy cảm của các **security logs** <br> - Tham gia **AWS Cloud Mastery Series #1 - AI/ML/GenAI on AWS** | 14/11/2025 | 16/11/2025 |[Tóm tắt và Trải nghiệm Sự kiện](../../4-EventParticipated/4.3-Event3)|


### Thành tựu Tuần 10:

* **Phát triển và Tối ưu hóa ETL Pipeline Nâng cao**
    * Hoàn thành thành công việc xây dựng **ETL pipeline** cho **CloudWatch logs**.
    * Đã giải quyết các lỗi **schema** nghiêm trọng trong **CloudTrail ETL pipeline** để đảm bảo xử lý dữ liệu đáng tin cậy giữa các ngày khác nhau.
    * Xây dựng một **custom Lambda ETL pipeline** cho **GuardDuty logs** để giải quyết các vấn đề **schema** gặp phải với việc **export raw log**.
    * Tinh chỉnh quy trình **CloudTrail ETL** để bỏ qua **Glue Crawler** bằng cách để hàm **Lambda** trực tiếp gọi **Glue API** tạo **Catalog Table**.
* **Tích hợp Công cụ Bảo mật và Thông báo**
    * Triển khai thành công **AWS Systems Manager (SSM)** để lấy **EC2 system logs** cho việc ứng phó sự cố (**incident response**).
    * Tích hợp và kiểm thử các **chatbot** thông báo mối đe dọa trong cả **Slack** và **Telegram**, hiển thị thành công các thông báo được định dạng dựa trên **live threat findings**.
    * Thêm **Amazon Simple Email Service (SES)** vào kiến trúc dự án để định dạng và phân phối **email** chuyên nghiệp.
* **Kiến trúc Dự án, Tài liệu và Bảo mật**
    * Cập nhật đề xuất dự án, bao gồm kiến trúc đã sửa đổi, danh sách dịch vụ và tính toán lại chi phí.
    * Tích hợp **Key Management Service (KMS)** vào dự án để bảo mật các **security logs** nhạy cảm.
* **Phát triển Backend Dashboard**
    * Kiểm thử thành công một hàm **Lambda** để truy vấn với **Athena**, chuẩn bị cho việc tích hợp **API Gateway** cho **dashboard**.
    * Đóng góp vào thiết kế **dashboard**, đề xuất tích hợp **Grafana**.
* **Tham gia Sự kiện**
    * Đã tham gia **AWS Cloud Mastery Series #1 - AI/ML/GenAI on AWS**