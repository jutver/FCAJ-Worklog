---
title: "Sự kiện 3"
date: "2026-04-13"
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# "AWS Kubernetes, Elixir, và Cơ sở hạ tầng dưới dạng Mã nguồn với Terraform"

### Mục tiêu Sự kiện

- Giới thiệu về điều phối container với Kubernetes và cách AWS EKS đơn giản hóa việc chạy các khối lượng công việc ở quy mô lớn trên đám mây.
- Khám phá Elixir và máy ảo BEAM như một giải pháp hợp nhất, chịu lỗi tốt cho cơ sở hạ tầng DevOps.
- Trình bày các nguyên tắc của Cơ sở hạ tầng dưới dạng Mã nguồn (IaC) sử dụng AWS CloudFormation, AWS CDK và Terraform.
- Cung cấp hướng dẫn thực tế về công cụ, quy trình làm việc và các thực tiễn tốt nhất để phát triển ứng dụng đám mây (cloud-native) hiện đại.

### Diễn giả

- **Bảo Huỳnh** – Lập trình viên Cloud Native Junior tại Endava Vietnam | Người sáng lập & Trưởng nhóm ITea Lab | Trọng tâm: Thiết kế Kiến trúc Đám mây với Kubernetes
- **Nguyễn Tạ Minh Triết** – Thành viên R&D tại ITea Lab, Swinburne Vietnam | Thực tập sinh Lập trình viên SAP tại Bosch GSV | Trọng tâm: Elixir cho Cơ sở hạ tầng DevOps Chịu lỗi và Đồng thời Cao
- **Thịnh Nguyễn (Khánh Phúc Thịnh Nguyễn)** – Thực tập sinh Kỹ sư Đám mây FCAJ | Đội ngũ Vận hành ITea Lab | Trọng tâm: Cơ sở hạ tầng dưới dạng Mã nguồn với Terraform trên AWS

---

### Những điểm nhấn chính

#### Phiên 1: Thiết kế Kiến trúc Đám mây với Kubernetes

##### Những thách thức trong Điều phối Container

- **Docker & Docker Compose** → Đóng gói ứng dụng vào các container để dễ dàng di chuyển; Compose giúp chạy các ngăn xếp nhiều container chỉ với một lệnh.
- **Vấn đề Mở rộng quy mô** → Việc chạy thủ công vài container là có thể quản lý được, nhưng khối lượng công việc thực tế (production) trải rộng trên nhiều máy và cần sự tự động hóa.
- **Điều phối (Orchestration) giải quyết vấn đề gì?**:
  - Tự phục hồi (tự động khôi phục sau sự cố)
  - Khả năng mở rộng (tăng hoặc giảm dung lượng dựa trên nhu cầu)
  - Cập nhật và khôi phục phiên bản (rollback) với thời gian downtime tối thiểu
- **Các công cụ Điều phối phổ biến** → Docker Swarm, Kubernetes (K8s), K3S, và AWS ECS.

##### Giới thiệu về Kubernetes

- **Kubernetes là gì?** → Một nền tảng mã nguồn mở (còn gọi là K8S) để chạy các container ở quy mô lớn trên một cụm (cluster) các máy chủ.
- **Các tính năng cốt lõi** → Lập lịch (Scheduling), tự phục hồi (self-healing), tự động mở rộng (auto-scaling), cập nhật cuốn chiếu (rolling updates), và khả năng tùy chỉnh sâu.

##### Kiến trúc Kubernetes

- **Control Plane (Bộ não của Cụm)**:
  - `etcd` — kho lưu trữ khóa-giá trị phân tán chứa toàn bộ trạng thái của cụm.
  - `kube-apiserver` — điểm truy cập API duy nhất cho tất cả các hoạt động của cụm.
  - `kube-scheduler` — quyết định Pod nào sẽ chạy trên worker node nào.
  - `kube-controller-manager` — liên tục đối chiếu trạng thái thực tế với trạng thái mong muốn.
  - `cloud-controller-manager` — xử lý các tích hợp dành riêng cho nhà cung cấp đám mây (ví dụ: bộ cân bằng tải trên AWS).

- **Worker Node (Nút làm việc)**:
  - Chạy các container ứng dụng thực tế thông qua một container runtime (ví dụ: containerd).
  - `kubelet` — tác nhân quản lý các Pod trên mỗi node.
  - `kube-proxy` — xử lý định tuyến mạng và chuyển tiếp lưu lượng đến các Pod.

##### Các Đối tượng K8S Chính

- **Pod** → Đơn vị nhỏ nhất có thể triển khai; thường chứa một container, tất cả các container trong một Pod dùng chung IP và có thể dùng chung storage volumes.
- **ReplicaSet** → Giữ cho một số lượng Pod giống hệt nhau luôn chạy; thay thế bất kỳ Pod nào bị lỗi (tự phục hồi).
- **Deployment** → Cách tiêu chuẩn để quản lý ứng dụng trong K8S — bao bọc một ReplicaSet và thêm khả năng cập nhật cuốn chiếu và rollback.
- **ConfigMap** → Lưu trữ cấu hình không nhạy cảm dưới dạng cặp khóa-giá trị, được đưa vào Pod dưới dạng biến môi trường hoặc file mount.
- **Secret** → Lưu trữ các giá trị nhạy cảm (mật khẩu, token) tương tự như ConfigMap, nhưng được mã hóa Base64; quyền truy cập bị giới hạn chỉ cho các Pod cần nó.
- **Job** → Chạy một tác vụ một lần (ví dụ: sao lưu cơ sở dữ liệu hoặc xử lý hàng loạt); K8S sẽ thử lại Pod nếu nó thất bại.

##### Manifest, kubectl & Bắt đầu

- Các đối tượng Kubernetes được định nghĩa trong các **file YAML manifest** và được áp dụng bằng `kubectl` — công cụ CLI chính để tương tác với một cụm.
- **Môi trường Học tập Cục bộ**:
  - **Minikube** → Chạy một cụm K8S cục bộ trên một máy duy nhất; lý tưởng cho người mới bắt đầu.
  - **K3S** → Một bản phân phối K8S nhẹ, dễ cài đặt và tiết kiệm tài nguyên.
  - **K3D** → Chạy K3S bên trong Docker; tạo và xóa cụm nhanh chóng, rất tốt để thử nghiệm trên laptop.
- **Tài nguyên học tập được đề xuất** → LFS158 (Giới thiệu về Kubernetes), tài liệu chính thức của Kubernetes.io, và *Kubernetes the Hard Way* của Kelsey Hightower để hiểu sâu hơn.

##### EKS — Kubernetes trên AWS

- **EKS là gì?** → Amazon Elastic Kubernetes Service; AWS quản lý control plane để các nhóm tập trung vào ứng dụng thay vì cơ sở hạ tầng cụm.
- **Tại sao lại dùng EKS?** → Giảm thiểu thiết lập thủ công, tích hợp tự nhiên với các dịch vụ AWS (IAM, VPC, Load Balancers, ECR), và đơn giản hóa việc chạy K8S cấp production trên đám mây.

##### Các công cụ bổ sung

- **Helm** → Trình quản lý gói cho K8S; đóng gói ứng dụng thành các Chart có thể tái sử dụng, có phiên bản với file `values.yaml` có thể cấu hình cho các môi trường dev, staging và production.
- **K9S** → Một giao diện người dùng dựa trên terminal giúp dễ dàng trực quan hóa các pod, services và log trên toàn cụm mà không cần nhớ các lệnh kubectl.

---

#### Phiên 2: Elixir như một Giải pháp Hợp nhất cho Cơ sở hạ tầng DevOps Chịu lỗi và Đồng thời Cao

##### Giới thiệu về Elixir

- **Elixir là gì?** → Một ngôn ngữ lập trình hàm, đồng thời, chạy trên máy ảo BEAM — cùng một runtime ban đầu được xây dựng cho Erlang.
- **Dòng dõi Ngôn ngữ**:
  - Dựa trên Erlang; chạy trên cùng máy ảo BEAM.
  - Cú pháp lấy cảm hứng từ Ruby (quen thuộc và dễ đọc).
  - Biên dịch thành BEAM bytecode, tương tự như cách Java nhắm mục tiêu đến JVM.
  - Mô hình lập trình hàm (giống Haskell) với dữ liệu bất biến (immutable) và khớp mẫu (pattern matching).

##### BEAM Processes & Đồng thời

- **Mô hình BEAM Process** → Mỗi chương trình Elixir chạy như một tiến trình OS (OS process) duy nhất, nhưng BEAM runtime tạo ra hàng ngàn process nội bộ nhẹ — mỗi process bị cô lập và không chia sẻ bộ nhớ.
- **Hai loại Process**:
  - **Worker** → Thực hiện một tác vụ cụ thể.
  - **Supervisor** → Giám sát và khởi động lại các worker khi chúng gặp lỗi.
- **Quy mô** → The Phoenix Framework đã benchmark được **2 triệu kết nối WebSocket đồng thời** trên một máy chủ duy nhất — một minh chứng cho mô hình đồng thời của BEAM.

##### Đạt được Khả năng Chịu lỗi với OTP

- **Lightweight Processes (Process nhẹ)** → BEAM có thể duy trì hàng triệu process đồng thời, mỗi process xử lý một đơn vị công việc nhỏ, cô lập.
- **Giám sát Process** → Thay vì lập trình phòng thủ `try/catch`, các process được giám sát chỉ đơn giản là được phép "crash" (đóng/lỗi) và được supervisor của chúng tự động khởi động lại — giúp xử lý lỗi nhất quán và dễ đoán hơn.
- **Triết lý "Let It Crash"** → Chấp nhận thất bại như một sự kiện bình thường; cây giám sát đảm bảo hệ thống phục hồi một cách mượt mà mà không cần can thiệp thủ công.
- **Nâng cấp mã nguồn nóng (Hot Code Upgrades)** → BEAM (kế thừa từ Erlang) hỗ trợ nâng cấp các hệ thống đang chạy mà không bị downtime, mặc dù các bản triển khai blue-green hiện đại ngày nay thường được ưa chuộng hơn trong thực tế.

##### Elixir trong Quy trình DevOps

- **Công cụ tích hợp** → Các công cụ tích hợp của Elixir (`Mix` để build/test/quản lý dependency, `IEx` để phát triển tương tác) làm giảm sự cần thiết phải mở rộng thêm các công cụ bên ngoài.
- **Giải pháp Hợp nhất** → Một stack duy nhất dựa trên BEAM có thể xử lý việc phục vụ web, các tác vụ chạy nền, giao tiếp thời gian thực, luồng dữ liệu, và giám sát — loại bỏ sự ma sát khi phải tích hợp nhiều ngôn ngữ và runtime khác nhau.
- **Lợi ích cho Dev & Ops** → Ít thành phần di chuyển hơn, các artifact triển khai nhất quán, và một ngôn ngữ chung cho cả logic ứng dụng và cơ sở hạ tầng.

##### Nghiên cứu điển hình thực tế — Từ Serverless sang Elixir

- Một dịch vụ ban đầu được xây dựng trên **AWS API Gateway + Lambda (Node.js)** để thu thập các luồng sự kiện trình duyệt đã được viết lại bằng Elixir.
- **So sánh chi phí**:
  - API Gateway với 5 triệu request/giờ → **$12.600/tháng**
  - Elixir ở mức cấu hình thấp (0.5 CPU) → **$59/tháng**
  - Elixir ở mức cấu hình cao (2 CPU) → **$397/tháng**
- Việc viết lại này chứng minh rằng đối với các kết nối có thông lượng cao, tồn tại lâu dài, một ứng dụng BEAM được tối ưu tốt sẽ vượt trội hơn hẳn một kiến trúc serverless về cả chi phí và độ phức tạp vận hành.

---

#### Phiên 3: Cơ sở hạ tầng dưới dạng Mã nguồn (IaC) với Terraform trên AWS

##### Tại sao lại dùng IaC? Vấn đề với ClickOps

- **ClickOps** → Cung cấp cơ sở hạ tầng theo cách thủ công thông qua AWS Console; rất tốt để học hỏi, nhưng có vấn đề ở quy mô lớn.
- **Hạn chế của ClickOps**:
  - **Chậm** — các bước thủ công lặp đi lặp lại cho mỗi môi trường.
  - **Lỗi của con người** — cấu hình không nhất quán giữa các lần triển khai.
  - **Thiếu nhất quán** — không đảm bảo sự tương đương giữa dev, staging, và production.
  - **Vấn đề Hợp tác** — không có lịch sử phiên bản hoặc đánh giá ngang hàng (peer review) cho các thay đổi cơ sở hạ tầng.
- **Giải pháp IaC** → Sử dụng mã nguồn (chứ không phải những cú click chuột) để tự động tạo, cập nhật, và xóa cơ sở hạ tầng; cho phép tự động hóa, khả năng tái tạo, khả năng mở rộng, và hợp tác.

##### AWS CloudFormation

- **Nó là gì?** → Công cụ IaC bản địa của AWS; cơ sở hạ tầng được mô tả trong các template YAML hoặc JSON mà CloudFormation sẽ tự động cấp phát.
- **CloudFormation Stack** → Một tập hợp các tài nguyên AWS được đặt tên và quản lý như một đơn vị duy nhất; triển khai, cập nhật, hoặc xóa tất cả tài nguyên cùng nhau từ một template.
- **Cấu trúc Template** → Một file YAML/JSON định nghĩa trạng thái mong muốn của cơ sở hạ tầng — tài nguyên (resources), tham số (parameters), đầu ra (outputs), và điều kiện (conditions).
- **Quy trình làm việc** → Viết template → lưu trữ trên S3 hoặc cục bộ → tạo stack → CloudFormation cấp phát tất cả các tài nguyên được chỉ định.
- **Trôi dạt cấu hình (Configuration Drift)** → Khi các tài nguyên bị thay đổi thủ công bên ngoài CloudFormation, chúng sẽ lệch khỏi template. Tính năng phát hiện drift của CloudFormation xác định những gì đã thay đổi, mặc dù nó không tự động sửa; người vận hành phải cập nhật stack hoặc hoàn tác (revert) thay đổi đó.

##### AWS Cloud Development Kit (CDK)

- **Nó là gì?** → Một framework mã nguồn mở cho phép các lập trình viên định nghĩa cơ sở hạ tầng AWS bằng các ngôn ngữ lập trình thực sự: TypeScript, JavaScript, Python, Java, C#, và Go — sau đó tự động biên dịch (synthesize) thành các template CloudFormation ở phía dưới.
- **Constructs** → Các khối xây dựng cơ bản của CDK, với ba cấp độ trừu tượng:
  - **L1 (CfnXxx)** → Ánh xạ trực tiếp 1:1 tới các tài nguyên CloudFormation; kiểm soát thủ công hoàn toàn, mức độ trừu tượng thấp nhất.
  - **L2** → Cấp độ cao hơn, thân thiện với lập trình viên với các giá trị mặc định hợp lý và các helper method; là cấp độ được sử dụng phổ biến nhất.
  - **L3** → Hoàn thiện các mẫu kiến trúc (nhiều tài nguyên hoạt động cùng nhau); con đường nhanh nhất để triển khai các kịch bản phổ biến.
- **Hệ thống phân cấp CDK** → `App` (cấp cao nhất) → `Stack` (đơn vị triển khai) → `Construct` (các tài nguyên hoặc pattern riêng lẻ).
- **Các lệnh CLI chính** → `cdk init`, `cdk bootstrap`, `cdk synth`, `cdk deploy`, `cdk diff`, `cdk destroy`, `cdk drift`, và `cdk doctor`.

##### Terraform

- **Nó là gì?** → Một công cụ IaC mã nguồn mở của HashiCorp sử dụng **HCL (HashiCorp Configuration Language)** để cấp phát cơ sở hạ tầng trên AWS, Azure, Google Cloud, và nhiều hơn nữa — tất cả từ một công cụ duy nhất.
- **Điểm mạnh cốt lõi**:
  - **Hỗ trợ Multi-Cloud** → Hoạt động trên tất cả các nhà cung cấp lớn với một quy trình làm việc nhất quán.
  - **Theo dõi trạng thái (State Tracking)** → Duy trì một file `terraform.tfstate` ghi lại trạng thái thực tế của tất cả các tài nguyên được quản lý.
  - **Cấu hình Đơn giản** → HCL dễ đọc và có tính khai báo (declarative), làm giảm rào cản học tập.
- **Cấu trúc thư mục**:
  - Cơ bản: `main.tf`, `variables.tf`, `outputs.tf`, `providers.tf`, `.tfvars`
  - Nâng cao: Được tổ chức thành `bootstrap/`, `environment/` (dev/staging/prod), và các `modules/` có thể tái sử dụng (networking, ec2, s3).
- **Quy trình làm việc CLI chính**:
  - `terraform init` → Khởi tạo dự án và tải xuống các provider.
  - `terraform validate` → Kiểm tra lỗi cú pháp và cấu hình.
  - `terraform plan` → Xem trước những gì sẽ được tạo (+), thay đổi (~), hoặc xóa (-).
  - `terraform apply` → Thực thi các thay đổi đã được lập kế hoạch.
  - `terraform destroy` → Xóa tất cả cơ sở hạ tầng được quản lý.
  - `terraform state` → Kiểm tra và quản lý file state.

##### Chọn đúng công cụ IaC

Ba câu hỏi để định hướng quyết định:
1. **Một Đám mây hay Nhiều?** → Terraform xuất sắc cho multi-cloud; CloudFormation/CDK là tối ưu cho các thiết lập chỉ sử dụng AWS.
2. **Dev hay Ops?** → CDK phù hợp với các nhóm dev thoải mái với code; CloudFormation và Terraform thân thiện với Ops hơn.
3. **Hỗ trợ Đám mây & Hệ sinh thái** → Xem xét những công cụ, module, và tài nguyên cộng đồng nào có sẵn.
- **Các công cụ đáng chú ý khác** → OpenTofu (bản fork mã nguồn mở của Terraform) và Pulumi (IaC đa ngôn ngữ, multi-cloud).

---

### Những bài học chính rút ra

#### Kubernetes là Tiêu chuẩn Công nghiệp cho Điều phối Container

- Hiểu được kiến trúc phân lớp của K8S — Control Plane, Worker Nodes, Pods, Deployments, Services — là điều cần thiết đối với bất kỳ ai làm việc trong lĩnh vực hạ tầng cloud-native.
- EKS gỡ bỏ gánh nặng vận hành của việc quản lý control plane, cho phép các nhóm tập trung vào việc phân phối ứng dụng thay vì bảo trì cụm.

#### Elixir cung cấp một sự thay thế hấp dẫn cho Cơ sở hạ tầng Thông lượng cao

- Mô hình lightweight process của BEAM và triết lý giám sát "Let It Crash" khiến Elixir thực sự phù hợp để xây dựng các công cụ DevOps phục hồi nhanh, tính đồng thời cao.
- Nghiên cứu điển hình về chi phí minh họa rằng việc lựa chọn đúng ngôn ngữ và runtime có thể mang lại sự giảm thiểu chi phí cơ sở hạ tầng theo cấp số nhân.

#### IaC là một Thực tiễn Bắt buộc cho Vận hành Đám mây có khả năng Mở rộng

- Quản lý cơ sở hạ tầng thủ công không có khả năng mở rộng; IaC mang đến khả năng kiểm soát phiên bản (versioning), tính lặp lại (repeatability), và sự hợp tác vào việc cấp phát tài nguyên đám mây.
- CloudFormation và CDK rất tuyệt vời cho các dự án thuần AWS; Terraform là lựa chọn hàng đầu để tiêu chuẩn hóa trên multi-cloud hoặc toàn tổ chức.

---

### Áp dụng vào Công việc

- **Kubernetes**:
  - Bắt đầu với Minikube hoặc K3D trên máy cục bộ để làm quen thực tế trước khi chuyển sang EKS.
  - Áp dụng Helm để đóng gói và triển khai ứng dụng qua các môi trường, và K9S cho việc theo dõi cụm hàng ngày.

- **Elixir**:
  - Đánh giá các giải pháp dựa trên BEAM cho các dịch vụ đòi hỏi tính đồng thời cao, kết nối liên tục (persistent connections), hoặc xử lý chạy nền phức tạp.
  - Xem xét triết lý "Let It Crash" như một giải pháp thay thế cho các mẫu xử lý lỗi dài dòng trong các hệ thống hiện tại.

- **IaC & Terraform**:
  - Đưa tất cả các định nghĩa cơ sở hạ tầng vào hệ thống quản lý phiên bản (version control) và bắt buộc đánh giá ngang hàng thông qua các Pull Request — coi cơ sở hạ tầng giống hệt như mã nguồn ứng dụng.
  - Sử dụng quy trình `plan → apply` như một cánh cổng an toàn trước bất kỳ thay đổi production nào, và tận dụng các module cho các cấu hình có thể tái sử dụng, dành riêng cho từng môi trường.

---

### Trải nghiệm Sự kiện

Tham gia các phiên họp về **AWS Kubernetes, Elixir, và IaC với Terraform** đã mang đến một cái nhìn tổng quan phong phú về bộ công cụ DevOps hiện đại — từ điều phối container, lựa chọn ngôn ngữ lập trình cho đến tự động hóa cơ sở hạ tầng trên quy mô lớn.

#### Xây dựng Trực giác Cloud-Native

- Phiên họp về Kubernetes đã thiết lập một mô hình tư duy rõ ràng về cách các khối lượng công việc được container hóa được quản lý trong production, tiến triển một cách tự nhiên từ các khái niệm cơ bản của Docker cho đến tận kiến trúc EKS.
- Việc phân tích các thành phần Pods, ReplicaSets, Deployments, ConfigMaps, và Secrets — và cách chúng kết hợp với nhau — đã cung cấp nền tảng khái niệm cần thiết để đọc và viết các manifest K8S thực tế.

#### Một Góc nhìn Bất ngờ về Ngôn ngữ DevOps

- Phiên họp về Elixir là một điểm nhấn nhờ góc nhìn mới mẻ: thay vì trình bày thêm một dịch vụ đám mây khác, nó đã đưa ra một lập luận thuyết phục về việc tư duy lại runtime và chính ngôn ngữ lập trình như là một phần của chiến lược cơ sở hạ tầng.
- Sự so sánh chi phí trong thế giới thực — từ hàng ngàn đô la mỗi tháng cho serverless Lambda xuống dưới 400 đô la trên một máy chủ Elixir duy nhất — đã làm cho một lập luận kỹ thuật trừu tượng trở nên cụ thể và đáng nhớ.

#### Giải mã Cơ sở hạ tầng dưới dạng Mã nguồn (IaC)

- Việc thấy CloudFormation, CDK, và Terraform được trình bày cạnh nhau trong cùng một phiên giúp dễ hiểu hơn về việc mỗi công cụ phù hợp ở đâu, thay vì coi chúng là những lựa chọn cạnh tranh.
- Các cấp độ construct thiết thực của CDK (L1/L2/L3) và quy trình làm việc `plan → apply` của Terraform đã cung cấp các pattern có thể hành động ngay lập tức cho bất kỳ ai bắt đầu hành trình IaC của mình.

#### Kết nối các điểm giữa các Phiên

- Ba phiên họp đã bổ sung cho nhau rất tốt: Kubernetes giải quyết *cách ứng dụng chạy*, Elixir định hình *cách dịch vụ được xây dựng*, và Terraform chi phối *cách cơ sở hạ tầng được cấp phát* — cùng nhau tạo thành một bức tranh mạch lạc về văn hóa kỹ thuật cloud-native hiện đại.

#### Bài học rút ra

- Điều phối container không chỉ là về cú pháp Kubernetes — mà là về việc hiểu triết lý tự phục hồi, mang tính khai báo (declarative) làm nền tảng cho toàn bộ hệ thống.
- Lựa chọn ngôn ngữ lập trình cho công cụ hạ tầng là một quyết định kiến trúc chính đáng, chứ không phải là điều được nghĩ đến sau cùng.
- Công cụ IaC tốt nhất không phải lúc nào cũng là công cụ nhiều tính năng nhất; đó là công cụ phù hợp nhất với kỹ năng của nhóm, chiến lược đám mây, và bối cảnh vận hành.