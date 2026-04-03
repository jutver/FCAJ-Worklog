---
title: "Nhật ký Công việc Tuần 7"
date: "2025-10-20"
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu Tuần 7:

* Nắm bắt các nguyên tắc của công nghệ container hóa và các khái niệm cốt lõi của Docker.
* Khám phá các khả năng của AWS trong việc quản lý khối lượng công việc dựa trên container.
* Khởi chạy một ứng dụng được container hóa cơ bản sử dụng các giải pháp container của AWS.

---

### Các công việc đã hoàn thành trong tuần này:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|-----|------|------------|----------------|-------------------|
| 2 | - Nghiên cứu các thành phần cốt lõi của Docker (images, containers, volumes, networking) <br> - Đối chiếu container với Máy ảo (Virtual Machines) tiêu chuẩn. <br> - Khám phá các thành phần cơ bản: <br>&emsp; + Docker Images <br>&emsp; + Docker Containers <br>&emsp; + Dockerfiles <br>&emsp; + Volumes <br>&emsp; + Ánh xạ cổng (Port mapping) | 02/23/2026 | 02/23/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | - Tích lũy kinh nghiệm thực tế trong việc tạo Docker image và thực thi các container cục bộ <br> - Xây dựng và thực thi một container ứng dụng web cơ bản trong môi trường cục bộ. | 02/24/2026 | 02/24/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | - Khám phá Amazon ECR (Elastic Container Registry) <br> - Cấp phát một kho lưu trữ image riêng tư. <br> - Gắn thẻ và tải các Docker image lên ECR. <br> - Nắm bắt các khái niệm về kiểm soát phiên bản cho image và quản lý kho lưu trữ. | 02/25/2026 | 02/25/2026 | https://cloudjourney.awsstudygroup.com/ |
| 5 | - Tìm hiểu các thành phần của Amazon ECS (clusters, task definitions và services) <br> - Phân tích kiến trúc của ECS: <br>&emsp; + Clusters <br>&emsp; + Task Definitions <br>&emsp; + Tasks <br>&emsp; + Services <br> - Phân biệt giữa các chế độ khởi chạy EC2 và Fargate. | 02/26/2026 | 02/26/2026 | https://cloudjourney.awsstudygroup.com/ |
| 6 | Bài tập thực hành: Triển khai một ứng dụng web dựa trên container lên ECS & ECR | 02/27/2026 | 02/27/2026 | https://cloudjourney.awsstudygroup.com/ |

---

### Thành tựu Tuần 7

* Nắm vững các nguyên tắc nền tảng về container và vòng đời Docker tiêu chuẩn.
* Tạo và xác thực thành công một Docker image cục bộ.
* Tải image lên Amazon ECR.
* Cấp phát một ECS Cluster và khởi chạy một dịch vụ container đang hoạt động.
* Lưu trữ một ứng dụng web chạy bằng container có đầy đủ chức năng trên AWS.
* Tích lũy kiến thức thực tế về cách thức hoạt động của việc điều phối container trong các kiến trúc đám mây.

---

### Suy ngẫm

Những bài học trong tuần này đã làm sáng tỏ phương pháp tiếp cận hiện đại để đóng gói và khởi chạy các ứng dụng thông qua container. Bằng cách chuyển đổi khỏi việc quản trị máy chủ thủ công, việc điều phối container tạo điều kiện cho các triển khai có khả năng thích ứng cao, hiệu quả và có thể mở rộng trên đám mây. Việc nắm vững các khái niệm này là một bước đệm quan trọng cho các nỗ lực về Kỹ thuật Đám mây (Cloud Engineering) và DevOps trong tương lai.

---