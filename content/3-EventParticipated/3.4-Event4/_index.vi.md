---
title: "Sự kiện 4"
date: "2025-11-17"
weight: 4
chapter: false
pre: " <b> 3.4. </b> "
---

# "Mạng AWS, Quản lý danh tính và truy cập (IAM), và Bảo mật"

### Mục tiêu Sự kiện

- Giới thiệu các khái niệm nền tảng về Mạng AWS và cách cấu trúc cũng như bảo mật các Đám mây riêng ảo (Virtual Private Clouds).
- Giải thích Quản lý danh tính và truy cập (IAM) như là xương sống của việc kiểm soát truy cập an toàn, quyền hạn tối thiểu trên AWS.
- Trình bày các công cụ bảo vệ mạng và ứng dụng thực tế trên AWS bao gồm WAF, Shield và Network Firewall.
- Cung cấp các hướng dẫn có thể áp dụng thực tế để xây dựng cơ sở hạ tầng đám mây an toàn, kiến trúc tốt trên AWS.

### Diễn giả

- **Lâm An Thịnh** – Thực tập sinh Kỹ sư Bảo mật tại DataXight | Chủ tịch ITea Lab | Trọng tâm: Mạng AWS
- **Nguyễn Phan Quốc Việt** – Trọng tâm: Mạng AWS
- **Huỳnh Hoàng Long** – Đại sứ Kỹ sư Đám mây FCAJ | Trọng tâm: Quản lý Danh tính & Truy cập (IAM)
- **Đặng Thị Minh Thư** – Đại sứ Kỹ sư Đám mây FCAJ | Trọng tâm: Quản lý Danh tính & Truy cập (IAM)
- **Lâm Tuấn Kiệt** – Kỹ sư DevOps | Trọng tâm: Bảo vệ Mạng & Ứng dụng AWS

---

### Những điểm nhấn chính

#### Phiên 1: Mạng AWS

##### VPC & Kiến trúc Mạng cốt lõi

- **VPC (Virtual Private Cloud - Đám mây riêng ảo)** → Một mạng riêng biệt bị cách ly bên trong AWS, nơi lưu trữ tất cả các tài nguyên đám mây.
- **CIDR (Classless Inter-Domain Routing)** → Xác định dải địa chỉ IP cho VPC của bạn, kiểm soát tổng không gian địa chỉ khả dụng.
- **Khái niệm Bán kính ảnh hưởng (Blast Radius)** → Việc phân đoạn mạng kém có nghĩa là một cấu hình sai duy nhất (ví dụ: mở cổng 22 cho `0.0.0.0/0`) có thể phơi bày toàn bộ môi trường.

##### Mạng con (Subnets), Bảng định tuyến (Route Tables) & Cổng Internet (Internet Gateway)

- **Subnets** → Các phân khu của một VPC dùng để chia các tài nguyên thành các nhóm logic (công khai vs. riêng tư).
- **Elastic IP** → Một địa chỉ IPv4 công khai tĩnh được liên kết với một EC2 instance để có quyền truy cập nhất quán từ bên ngoài.
- **Route Tables** → Xác định cách lưu lượng được định tuyến bên trong VPC và đến/từ thế giới bên ngoài.
- **Internet Gateway (IGW)** → Kết nối một VPC với internet công cộng; được gắn ở cấp độ VPC cho việc định tuyến subnet công khai.
- **Định tuyến đi ra (Egress Routing)** → Kiểm soát các đường dẫn lưu lượng chỉ theo chiều đi ra cho các tài nguyên riêng tư.

##### NAT Gateway

- **Mục đích** → Cho phép các tài nguyên trong subnet riêng tư truy cập internet (ví dụ: để cập nhật phần mềm) trong khi ngăn chặn các kết nối đến không mong muốn.
- **Cơ chế**:
  - **SNAT (Source NAT - NAT Nguồn)**: Thay thế IP riêng của EC2 instance bằng IP công khai của NAT Gateway cho lưu lượng đi ra.
  - **PAT (Port Address Translation - Dịch địa chỉ cổng)**: Sử dụng các cổng nguồn duy nhất để phân biệt các phiên từ nhiều EC2 instances khác nhau.
  - **Bảng trạng thái (State Table)**: Theo dõi các phiên đang hoạt động và loại bỏ bất kỳ gói tin đến nào không khớp với một mục hiện có.
- **Tùy chọn triển khai** → Zonal (Theo vùng sẵn sàng) vs. Regional (Theo khu vực) NAT Gateway — cân bằng giữa tính sẵn sàng với chi phí và hiệu suất.

##### Nhóm bảo mật (Security Group)

- **Vai trò** → Lớp phòng thủ chính cho từng tài nguyên AWS riêng lẻ, hoạt động ở cấp độ ENI (Giao diện Mạng Đàn hồi).
- **Cơ chế có trạng thái (Stateful)** → Tự động cho phép lưu lượng phản hồi cho bất kỳ kết nối đến nào được phép; không cần cấu hình quy tắc đi ra một cách riêng biệt.
- **Triết lý Zero Trust (Không tin cậy)** → Tất cả lưu lượng đến đều bị từ chối ngầm định theo mặc định; chỉ hỗ trợ các quy tắc "Cho phép" (Allow) rõ ràng — không có quy tắc "Từ chối" (Deny).
- **Vi phân đoạn (Micro-segmentation)** → Các chính sách bảo mật đi theo instance bất kể nó ở subnet nào, cho phép kiểm soát truy cập chi tiết.

##### Danh sách kiểm soát truy cập mạng (Network ACL - NACL)

- **Vai trò** → Một tường lửa ở cấp độ subnet hoạt động như lớp phòng thủ thứ hai, bổ sung cho các Nhóm bảo mật.
- **Cơ chế không trạng thái (Stateless)** → NACL đánh giá từng gói tin một cách độc lập; cả hai quy tắc chiều đến và chiều đi đều phải được cấu hình rõ ràng, bao gồm cả các cổng tạm thời (ephemeral ports) (1024–65535).
- **Đánh giá quy tắc** → Các quy tắc được xử lý theo thứ tự số (số nhỏ nhất xử lý trước); quy tắc khớp đầu tiên sẽ được áp dụng và quy tắc mặc định dấu sao (`*`) "Từ chối tất cả" sẽ đóng mọi NACL.
- **Ưu điểm chính so với Nhóm bảo mật** → Hỗ trợ các quy tắc **TỪ CHỐI (DENY)** rõ ràng, cho phép chủ động chặn các dải IP hoặc các mẫu lưu lượng cụ thể.

---

#### Phiên 2: AWS IAM — Quản lý Danh tính & Truy cập

##### IAM là gì?

- **Chức năng cốt lõi** → Dịch vụ của AWS để quản lý xác thực (bạn là ai) và phân quyền (bạn có thể làm gì) trên toàn bộ các tài nguyên đám mây.
- **Quản lý** → Người dùng (Users), nhóm (groups), vai trò (roles), và chính sách (policies) trong một khuôn khổ kiểm soát truy cập thống nhất.
- **Nhóm IAM (IAM Groups)** → Đơn giản hóa việc quản lý quyền bằng cách gán chính sách cho một nhóm thay vì cho từng người dùng riêng lẻ.

##### Các thực tiễn tốt nhất với IAM

- Áp dụng **Nguyên tắc Quyền hạn tối thiểu (Least Privilege)** — chỉ cấp các quyền cần thiết, tuyệt đối không cấp dư.
- **Xóa các khóa truy cập root (root access keys)** ngay sau khi tạo tài khoản; sử dụng người dùng hoặc vai trò IAM cho mọi hoạt động hàng ngày.
- Tránh sử dụng dấu sao `"*"` trong `Actions` (Hành động) hoặc `Resources` (Tài nguyên) trong các chính sách IAM, vì điều này cấp quyền quá rộng.
- **Bật MFA (Xác thực đa yếu tố)** cho tất cả người dùng, đặc biệt là những người có quyền hạn cao.
- **Luân phiên mật khẩu và thông tin xác thực** theo lịch trình thường xuyên để giảm thiểu rủi ro khi bị lộ khóa.

##### SSO — Đăng nhập một lần (Single Sign-On)

- **Khái niệm** → Một thông tin đăng nhập cấp quyền truy cập vào nhiều tài khoản và ứng dụng AWS, đơn giản hóa trải nghiệm người dùng.
- **Tích hợp Đa tài khoản** → Tích hợp với AWS Organizations để quản lý tập trung quyền truy cập xuyên suốt các bộ phận Tài chính, Pháp lý, Sản xuất, Kiểm thử, và các phòng ban khác dưới một tài khoản gốc duy nhất.
- **Quản lý Truy cập Tập trung** → Các chính sách và quyền hạn được quản trị từ một nơi, giảm thiểu chi phí quản lý hành chính và nguy cơ cấu hình sai.

##### SCPs & Ranh giới Quyền hạn

- **Chính sách kiểm soát dịch vụ (SCPs - Service Control Policies)**:
  - Một loại chính sách cấp tổ chức được gắn thông qua AWS Organizations.
  - Kiểm soát **quyền hạn tối đa** có sẵn trên tất cả các tài khoản trong tổ chức.
  - SCPs không bao giờ cấp quyền — chúng chỉ lọc hoặc hạn chế những gì đã được cho phép.

- **Ranh giới Quyền hạn (Permission Boundaries)**:
  - Một tính năng IAM nâng cao nhằm thiết lập **quyền hạn tối đa** mà một chính sách dựa trên danh tính có thể cấp cho một Người dùng hoặc Vai trò IAM cụ thể.
  - Khác với SCPs (áp dụng trên toàn tổ chức), Ranh giới quyền hạn được giới hạn trong phạm vi người dùng hoặc vai trò riêng lẻ trong một tài khoản duy nhất.
  - Hữu ích cho việc ủy quyền quản lý IAM một cách an toàn mà không cho phép leo thang đặc quyền.

##### Quản lý Thông tin xác thực & Công cụ phân tích truy cập

- **Phân loại Thông tin xác thực**:
  - **Dài hạn**: Khóa truy cập của Người dùng IAM — mặc định không hết hạn; nên tránh sử dụng.
  - **Ngắn hạn**: Được tạo bởi AWS STS (Security Token Service) — tự động hết hạn từ 15 phút đến 36 giờ.
- **Khuyến nghị** → Sử dụng AWS IAM Identity Center để đăng nhập, vì nó cung cấp thông tin xác thực ngắn hạn ẩn ở nền.
- **IAM Access Analyzer (Công cụ phân tích truy cập)** → Tự động gắn cờ các chính sách có cấu hình quá nới lỏng như `"Principal: *"`, giúp xác định các quyền truy cập công khai ngoài ý muốn.

---

#### Phiên 3: Bảo mật AWS — Bảo vệ Mạng & Ứng dụng

##### AWS WAF (Web Application Firewall)

- **Mục đích** → Bảo vệ các ứng dụng web khỏi các cuộc tấn công khai thác phổ biến bằng cách lọc và giám sát các yêu cầu HTTP/HTTPS.
- **Ngăn chặn** → SQL injection, cross-site scripting (XSS), và các mối đe dọa khác trong OWASP Top 10.
- **Tích hợp** → Được triển khai phía trước CloudFront, ALB, API Gateway hoặc AppSync để kiểm tra các yêu cầu trước khi chúng tiếp cận ứng dụng.

##### AWS Shield

- **Mục đích** → Cung cấp khả năng bảo vệ có quản lý chống lại DDoS (Tấn công từ chối dịch vụ phân tán) cho các khối lượng công việc trên AWS.
- **Hai cấp độ**:
  - **Standard (Tiêu chuẩn)** → Được áp dụng tự động cho tất cả khách hàng AWS mà không mất thêm phí; bảo vệ khỏi các cuộc tấn công lưu lượng phổ biến.
  - **Advanced (Nâng cao)** → Cấp độ trả phí cung cấp khả năng bảo vệ nâng cao, khả năng hiển thị cuộc tấn công theo thời gian thực, hỗ trợ từ đội phản ứng DDoS 24/7 và bảo vệ chi phí.

##### AWS Network Firewall (Tường lửa Mạng)

- **Mục đích** → Một dịch vụ có quản lý nhằm triển khai các ranh giới bảo mật trong VPC để kiểm tra lưu lượng sâu hơn.
- **Khả năng**:
  - Lọc lưu lượng có trạng thái (stateful) và không trạng thái (stateless).
  - Phát hiện và ngăn chặn xâm nhập (IDS/IPS).
  - Lọc dựa trên miền và kiểm tra TLS.
- **Trường hợp sử dụng** → Thực thi các chính sách bảo mật mạng chi tiết, nhất quán trên tất cả lưu lượng chảy qua một VPC.

##### AWS Firewall Manager

- **Mục đích** → Quản lý bảo mật tập trung trên nhiều tài khoản AWS và nhiều khu vực (regions).
- **Tự động hóa** → Triển khai quy tắc cho WAF, Shield Advanced, Network Firewall và Nhóm bảo mật trên quy mô lớn.
- **Phù hợp nhất cho** → Các tổ chức sử dụng AWS Organizations cần thực thi chính sách nhất quán trên hàng chục hoặc hàng trăm tài khoản.

---

### Những bài học chính rút ra

#### Bảo mật nhiều lớp là điều cần thiết

- Mạng AWS được xây dựng xung quanh một mô hình phòng thủ nhiều lớp: Nhóm bảo mật (Security Groups) bảo vệ các tài nguyên riêng lẻ, NACL bảo vệ các mạng con (subnets), và NAT Gateway kiểm soát quyền truy cập internet cho các khối lượng công việc riêng tư.
- Hiểu cách các lớp này tương tác với nhau — đặc biệt là sự khác biệt giữa stateful (có trạng thái) và stateless (không trạng thái) — là điều rất quan trọng để thiết kế các kiến trúc an toàn.

#### IAM là Nền tảng của Bảo mật Đám mây

- Mọi vấn đề bảo mật đám mây cuối cùng đều có thể bắt nguồn từ các quyền hạn. Việc thực hiện IAM đúng cách — với quyền hạn tối thiểu, MFA, thông tin xác thực ngắn hạn và SCPs — sẽ làm giảm đáng kể bề mặt tấn công.
- Sự chuyển đổi từ các khóa IAM dài hạn sang thông tin xác thực ngắn hạn dựa trên Identity Center là một trong những cải tiến bảo mật có tác động mạnh mẽ nhất mà một tổ chức có thể thực hiện.

#### Bảo vệ lớp ứng dụng hoàn thiện bức tranh toàn cảnh

- Các kiểm soát ở cấp độ mạng thôi là chưa đủ. AWS WAF và Shield cung cấp khả năng bảo vệ chống lại các mối đe dọa lớp ứng dụng và các cuộc tấn công thay đổi lưu lượng có thể vượt qua các quy tắc tường lửa truyền thống.
- AWS Firewall Manager giúp việc thực thi các tiêu chuẩn bảo mật một cách nhất quán trên quy mô lớn trở nên khả thi về mặt vận hành, đặc biệt là trong các môi trường đa tài khoản.

---

### Áp dụng vào Công việc

- **Thiết kế Mạng**:
  - Luôn tách biệt các subnet công khai và riêng tư; định tuyến lưu lượng truy cập ra internet từ các tài nguyên riêng tư thông qua NAT Gateway.
  - Sử dụng Nhóm bảo mật (Security Groups) làm cơ chế kiểm soát truy cập chính và xếp lớp NACL cho các quy tắc từ chối trên toàn bộ subnet khi cần thiết.

- **Quản lý chặt chẽ IAM (IAM Hygiene)**:
  - Kiểm toán (Audit) các chính sách IAM hiện tại xem có ký tự đại diện `"*"` hay không và thay thế bằng các quyền hạn có phạm vi cụ thể.
  - Bắt buộc áp dụng MFA trên toàn tổ chức và chuyển đổi sang các quy trình thông tin xác thực ngắn hạn.

- **Bảo vệ Ứng dụng & Mạng**:
  - Triển khai AWS WAF trên tất cả các endpoint hướng ra internet để chống lại các cuộc tấn công web phổ biến.
  - Sử dụng AWS Firewall Manager để tập trung hóa việc thực thi chính sách bảo mật nếu bạn quản lý nhiều tài khoản AWS.

---

### Trải nghiệm Sự kiện

Tham gia các phiên họp về **Mạng AWS, IAM và Bảo mật** đã mang lại cái nhìn sâu sắc và toàn diện về các khối xây dựng bảo mật của nền tảng AWS — từ kiến trúc mạng vật lý cho đến bảo vệ lớp ứng dụng.

#### Xây dựng mô hình tư duy về Bảo mật AWS

- Các phiên họp diễn ra một cách tự nhiên từ cơ sở hạ tầng mạng (VPC, subnets, gateways) đến kiểm soát truy cập (IAM) và cuối cùng là bảo vệ trước các mối đe dọa (WAF, Shield, Network Firewall), vẽ nên một bức tranh hoàn chỉnh về kiến trúc đám mây an toàn.
- Sự tương phản giữa các Nhóm bảo mật có trạng thái (stateful) và NACL không trạng thái (stateless) — được minh họa qua các sơ đồ luồng gói tin từng bước — đã biến một chủ đề thường gây bối rối trở nên trực quan và dễ nhớ.

#### Làm rõ các khái niệm IAM trong thực tế

- Sự phân biệt giữa SCPs (giới hạn tối đa toàn tổ chức) và Ranh giới quyền hạn (giới hạn tối đa cho từng người dùng/vai trò) đã làm rõ một điểm thường gây nhầm lẫn trong các môi trường AWS đa tài khoản.
- Việc nhấn mạnh vào "vệ sinh" thông tin xác thực — tránh sử dụng khóa dài hạn, luân phiên thay đổi thường xuyên, và sử dụng IAM Identity Center — đã cung cấp hướng dẫn có thể hành động ngay lập tức.

#### Hiểu về Bảo vệ trước Mối đe dọa trên Quy mô lớn

- Quá trình phát triển từ WAF (lọc yêu cầu) → Shield (bảo vệ DDoS) → Network Firewall (kiểm tra gói tin sâu) → Firewall Manager (quản trị tập trung) minh họa cách các dịch vụ bảo vệ của AWS được xếp chồng lên nhau.
- Việc thấy được cách Firewall Manager có thể tự động hóa việc triển khai chính sách trên toàn bộ AWS Organization đã làm nổi bật tầm quan trọng của tư duy "bảo mật như là mã" (security-as-code) ở cấp độ doanh nghiệp.

#### Bài học rút ra

- Bảo mật trên AWS không phải là một công tắc tắt/mở đơn lẻ — nó là một chuỗi các quyết định có tính toán, nhiều lớp, được thực hiện ở các cấp độ mạng, danh tính và ứng dụng.
- Sự khác biệt giữa một kiến trúc an toàn và không an toàn thường xuất phát từ những mặc định nhỏ: một quy tắc nhóm bảo mật bị mở, thiếu chính sách MFA, hoặc một hành động IAM quá nới lỏng.
- Đầu tư thời gian vào việc hiểu các nguyên tắc cơ bản — CIDR, lọc stateful vs. stateless, quyền hạn tối thiểu — sẽ mang lại lợi ích lớn khi gỡ lỗi các sự cố trong thế giới thực hoặc khi thiết kế các hệ thống mới.