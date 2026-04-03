---
title: "Nhật ký Công việc Tuần 4"
date: "2025-09-29"
weight: 04
chapter: false
pre: " <b> 1.4. </b> "
---



### Mục tiêu Tuần 4:
- Hoàn thành Module 6
- Bắt đầu đề xuất dự án

### Các nhiệm vụ được thực hiện trong tuần này:
| Ngày | Nhiệm vụ | Ngày Bắt đầu | Ngày Hoàn thành | Tài liệu Tham khảo |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   |- Module 6: Ôn tập Khái niệm Cơ sở Dữ liệu:<br> &emsp; + **Database** (Cơ sở dữ liệu) <br> &emsp; + **Session** (Phiên) <br> &emsp; + **Primary/Foreign Key** (Khóa chính/Khóa ngoại) <br> &emsp; + **Index** (Chỉ mục) <br> &emsp; + **Partitions** (Phân vùng) <br> &emsp; + **Execution/Query Plan** (Kế hoạch Thực thi/Truy vấn) <br> &emsp; + **Log & Buffer** (Nhật ký & Bộ đệm) <br> &emsp; + **RDBMS** (**Relational Database Management System** - Hệ thống Quản lý Cơ sở Dữ liệu Quan hệ) <br> &emsp; + **NOSQL** <br> ![Database](/images/1-Worklog/Database.png) <br> &emsp; + **OLTP** (**Online Transaction Processing**): Dùng cho thanh toán, giao dịch <br> &emsp; + **OLAP** (**Online Analytical Processing**): Phân tích dữ liệu, dự đoán xu hướng và mô hình <br> - **AWS RDS** (**Relational Database Service**): Bao gồm **Aurora, MySQL, PostgreSQL, MSSQL, Oracle, MariaDB** <br> &emsp; + Sao lưu tự động (**Automatic backup**) <br> &emsp; + Tạo **read replica** (bản sao chỉ đọc) <br> &emsp; + **Read replica** có thể được chuyển thành **primary node** <br> &emsp; + Tự động chuyển đổi dự phòng/Đa **AZ** (**Auto Failover/Multi AZ**) (Sao lưu trên nhiều **AZ**) <br> &emsp; + Thường được sử dụng cho **OLTP** <br> &emsp; + Mã hóa dữ liệu khi nghỉ (**at rest**)/đang truyền (**in transit**) <br> &emsp; + Được bảo vệ bởi **Security Group** và **NACL** <br> &emsp; + Có thể thay đổi kích thước **instance** <br> &emsp; + Tự động mở rộng lưu trữ (**Storage Auto Scaling**) <br> - **Amazon Aurora**: Cơ sở hạ tầng lưu trữ cơ bản được tối ưu hóa, sử dụng **MySQL** và **PostgreSQL** <br> &emsp; + **Backtrack**: hoàn nguyên về trạng thái trước đó <br> &emsp; + **Clone** (Sao chép) <br> &emsp; + **Global Database** (Đa **Region**) <br> &emsp; + **Multi Master**: Nhiều Cơ sở Dữ liệu **Master** <br> - **Amazon Redshift**: Dịch vụ kho dữ liệu (**Data warehouse service**): **core PostgreSQL**, được tối ưu hóa cho **OLAP** <br> &emsp; + Sử dụng **MPP Database**: dữ liệu được phân vùng và lưu tại các **compute nodes**, một **Leader node** được sử dụng để phối hợp và biên dịch các truy vấn <br> &emsp; + Lưu trữ dữ liệu ở định dạng lưu trữ cột (**columnar storage format**), hữu ích cho các ứng dụng **OLAP** <br> ![Columnar](/images/1-Worklog/Columnar.png) <br> &emsp; + Sử dụng **SQL** và các **driver** như **JDBC** và **ODBC** <br> &emsp; + Cung cấp các dịch vụ tiết kiệm chi phí (**Transient Cluster/Redshift Spectrum**) <br> - **Amazon ElastiCache**: Tạo Công cụ **Caching Cluster** (**Redis/Memcached**) <br> &emsp; + Phát hiện và thay thế các **nodes** bị lỗi <br> &emsp; + Đặt trước lớp **CSDL** để lưu vào bộ đệm dữ liệu <br> &emsp; + Khuyến nghị sử dụng **Redis** cho các khối lượng công việc mới <br> &emsp; + Sử dụng **ElastiCache** yêu cầu logic lưu vào bộ đệm trên các ứng dụng, không khuyến nghị sử dụng lưu vào bộ đệm hệ thống mặc định <br> - Xây dựng đề xuất **workshop** với đồng đội <br> - Môn học ở trường: <br> &emsp; + **KS57**: Hoàn thành **Quản trị dữ liệu và an toàn thông tin** | 29/09/2025 | 29/09/2025| [Quản trị dữ liệu và an toàn thông tin](https://www.coursera.org/account/accomplishments/verify/JA236L8TZGD7) |
| 3   |- Lab 43: Hướng dẫn bị hỏng, liên kết không dẫn đến đâu, làm theo video <br> &emsp; + Tải xuống **Schema Conversion Tool** <br> &emsp; + Tải xuống **MSSQL** trong **EC2 Instance** <br> &emsp; + Không có **SQL script** nào được cung cấp, thử với **custom basic MSSQL Database** <br> &emsp; + Không có **CloudFormation Stack** nào được cung cấp, bỏ qua kết nối **Oracle Database** <br> &emsp; + Cài đặt **MySQL** trên **EC2 Instance** <br> &emsp; + Di chuyển **custom MSSQL Database** sang **MySQL Database** bằng **AWS Schema Conversion Tool** <br> &emsp; + Tạo **custom RDS** để kiểm thử tác vụ di chuyển <br> &emsp; + Cố gắng di chuyển từ máy cục bộ sang **RDS** <br> &emsp; + Thử sử dụng **AWS Replication Agent**: Không thành công do nó chỉ được tạo cho **Windows/Linux server**, không phải **OS X** <br> &emsp; + Cố gắng **port forward PC** để được sử dụng làm **endpoint** <br> &emsp; + **Port forwarding** thất bại, không được phép bởi **ISP** | 30/09/2025 | 30/09/2025      | [Lab 43](https://000043.awsstudygroup.com/) <br><br> [Application Migration Service Guide](https://docs.aws.amazon.com/mgn/latest/ug/what-is-application-migration-service.html) |
| 4   |- Phát hiện **credits** tài khoản **AWS** đã hết hạn do làm **lab** 12 <br> - Viết **support case** <br> - Tạm dừng các **lab** <br> - Tập trung nghiên cứu về đề xuất của nhóm| 01/10/2025 | 01/10/2025 <br> - Môn học ở trường: <br> &emsp; + **ENW439c**: Hoàn thành **Research Methodologies** | [Research Methodologies](https://www.coursera.org/account/accomplishments/verify/M3368Q4AAMNB) |
| 5   |- Tiếp tục làm **lab** bằng cách nhận sự trợ giúp từ thành viên nhóm: Tạo một **IAM User** với quyền **admin** để tôi đăng nhập và sử dụng tài khoản của họ <br> - Dịch **blog** đầu tiên| 02/10/2025 | 02/10/2025      | [Blog 1](../../3-BlogsTranslated/3.1-Blog1) |
| 6   |- Tham gia sự kiện **AI-Driven Development Life Cycle: Reimagining Software Engineering** <br> - Dịch **blog** thứ hai và thứ ba| 03/10/2025 | 04/10/2025 | [Blog 2](../../3-BlogsTranslated/3.2-Blog2) <br><br> [Blog 3](../../3-BlogsTranslated/3.3-Blog3) | 


### Thành tựu Tuần 4:

* Hoàn thành một đánh giá toàn diện về các khái niệm cơ sở dữ liệu cốt lõi bao gồm **RDBMS**, **keys**, **indexes**, **partitioning**, **OLTP/OLAP**, và các dịch vụ cơ sở dữ liệu dành riêng cho **AWS**.

* Đạt được kiến thức lý thuyết về các tính năng và trường hợp sử dụng của **AWS RDS**, **Amazon Aurora** (ví dụ: **Backtrack**, **Global Database**), **Amazon Redshift** (**Data Warehouse** cho **OLAP**), và **Amazon ElastiCache** (**caching** với **Redis/Memcached**).

* **Di chuyển Cơ sở Dữ liệu**: Thử nghiệm một **lab** di chuyển cơ sở dữ liệu phức tạp, thể hiện sự tháo vát bằng cách:

  *  Tìm kiếm **custom MSSQL Database** và cài đặt các dịch vụ cần thiết trên **EC2 instance** do hướng dẫn **lab** bị hỏng.

  *  Di chuyển thành công **custom MSSQL database** sang **MySQL Database** bằng **AWS Schema Conversion Tool (SCT)**.

* Xác định và giải quyết vấn đề **credits AWS** đã hết hạn bằng cách gửi **support case**.

* Đảm bảo tiếp tục công việc **lab** bằng cách thiết lập một **IAM User** với đặc quyền **admin** trên tài khoản của thành viên nhóm.

* Xây dựng đề xuất cho **workshop** sắp tới của nhóm.

* Hoàn thành việc dịch ba **blog**.

* Đã tham dự sự kiện **AI-Driven Development Life Cycle: Reimagining Software Engineering**.