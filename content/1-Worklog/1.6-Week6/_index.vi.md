---
title: "Nhật ký Công việc Tuần 6"
date: "2025-10-13"
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu Tuần 6:

* Nắm bắt các khái niệm đằng sau các công cụ Tích hợp Ứng dụng (Application Integration) của AWS.
* Khám phá cơ chế của các kiến trúc hướng sự kiện (event-driven architectures) trên đám mây.
* Tích lũy kinh nghiệm thực tế trong việc xây dựng các luồng công việc cơ bản bằng cách sử dụng các công cụ nhắn tin và điều phối.

---

### Các công việc đã hoàn thành trong tuần này:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|-----|------|------------|----------------|-------------------|
| 2 | - Nắm bắt các nguyên tắc cơ bản của hàng đợi tin nhắn. <br> - Phân biệt giữa hàng đợi Standard và FIFO. <br> - Thực thi việc gửi và nhận tin nhắn. <br> - Hiểu thấu đáo khái niệm tách rời (decoupling) các vi dịch vụ (microservices). | 02/16/2026 | 02/16/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | - Khám phá mô hình nhắn tin Xuất bản/Đăng ký (Publish/Subscribe). <br> - Cấp phát các chủ đề (topics) và điểm cuối đăng ký (subscriber endpoints). <br> - Xác minh việc phát sóng tin nhắn đến nhiều người nhận khác nhau. | 02/17/2026 | 02/17/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | - Khám phá các cơ chế định tuyến sự kiện. <br> - Thiết lập các quy tắc để khởi tạo hành động dựa trên các sự kiện cụ thể. <br> - Nắm bắt cách các công cụ AWS khác nhau tích hợp thông qua các trình kích hoạt sự kiện. | 02/18/2026 | 02/18/2026 | https://cloudjourney.awsstudygroup.com/ |
| 5 | - Nắm vững việc điều phối các luồng công việc phức tạp. <br> - Phác thảo một máy trạng thái (state machine) thô sơ. <br> - Hiểu rõ trình tự sắp xếp các tác vụ và các cơ chế xử lý lỗi. | 02/19/2026 | 02/19/2026 | https://cloudjourney.awsstudygroup.com/ |
| 6 | Bài tập thực hành: Xây dựng một thiết lập hướng sự kiện cơ bản | 02/20/2026 | 02/20/2026 | https://cloudjourney.awsstudygroup.com/ |

---

### Thành tựu Tuần 6

* Hiểu rõ các công cụ AWS chính dành cho Tích hợp Ứng dụng.
* Xây dựng một khuôn khổ hướng sự kiện bước đầu tận dụng SQS, SNS và EventBridge.
* Triển khai và chạy thành công một máy trạng thái Step Functions.
* Đạt được sự hiểu biết thực tế về giao tiếp không đồng bộ (asynchronous communication) giữa các dịch vụ.
* Nâng cao khả năng kiến trúc các môi trường đám mây tách rời (decoupled) cao.

---

### Suy ngẫm

Những bài học trong tuần này đã làm rõ cách các hạ tầng đám mây quy mô lớn xử lý liên lạc nội bộ thông qua các hệ thống nhắn tin và sự kiện. Tôi học được rằng việc tận dụng các công cụ Tích hợp Ứng dụng của AWS tạo điều kiện cho việc tạo ra các kiến trúc linh hoạt, có khả năng phục hồi và mở rộng cao, thay vì sử dụng các hệ thống liên kết chặt chẽ và cứng nhắc.

---