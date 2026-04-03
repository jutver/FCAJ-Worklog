---
title: "Nhật ký Công việc Tuần 3"
date: "2026-01-26"
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu Tuần 3:

* Nắm bắt các nguyên tắc nền tảng về mạng AWS.
* Khám phá quy trình thiết lập VPC cùng với các thành phần liên quan.
* Phân biệt giữa các chức năng của Security Groups và Network ACLs.
* Hiểu rõ cơ chế hoạt động của Internet Gateways và NAT.
* Tích lũy kinh nghiệm thực tế thông qua việc xây dựng cấu trúc mạng đa tầng.

---

### Các công việc đã thực hiện trong tuần này:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2 | - Khám phá các nguyên tắc cơ bản của VPC <br> - Cấp phát và tinh chỉnh một VPC | 01/26/2026 | 01/26/2026 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 3 | - Nghiên cứu Subnets <br> - Xem xét Route Tables <br> - Tìm hiểu các khối CIDR trong một VPC | 01/27/2026 | 01/27/2026 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 4 | - Đối chiếu Security Groups với NACLs <br> - Cấu hình các quy tắc lưu lượng truy cập Inbound và Outbound | 01/28/2026 | 01/28/2026 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 5 | - Xem xét Internet Gateways <br> - Tìm hiểu về NAT Gateways <br> - So sánh các Public và Private Subnets | 01/29/2026 | 01/29/2026 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 6 | - **Bài tập thực hành:** Cấu trúc mạng đa tầng: <br>  + Cấp phát một VPC <br>  + Tạo các public và private subnets <br>  + Thiết lập route tables <br>  + Gắn Internet Gateway <br>  + Triển khai NAT | 01/30/2026 | 01/30/2026 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |

---

### Thành tựu Tuần 3:

* Nắm bắt được mục đích cốt lõi của Amazon VPC và tầm quan trọng của nó trong mạng AWS.

* Phát triển các kỹ năng để cấp phát và tinh chỉnh:
  * VPCs
  * Subnets
  * Route Tables

* Phân biệt rõ ràng sự khác biệt trong hoạt động giữa:
  * Security Groups (lọc có trạng thái - stateful filtering)
  * Network ACLs (lọc phi trạng thái - stateless filtering)

* Nắm vững cơ chế của các thành phần định tuyến quan trọng:
  * Internet Gateways
  * NAT Gateways
  * Phân đoạn Public và Private Subnet

* Triển khai hiệu quả một kiến trúc đa tầng nền tảng, bao gồm:
  * Một public subnet được thiết kế cho các tài nguyên hướng ra internet
  * Một private subnet được bảo mật cho các hệ thống nội bộ
  * Thiết lập cổng kết nối và định tuyến chính xác