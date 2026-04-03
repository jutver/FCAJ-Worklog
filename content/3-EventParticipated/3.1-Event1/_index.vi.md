---
title: "Event 1"
date: "2005-09-18"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Báo cáo Tổng kết: “AWS RE:INVENT 2025 RECAP (VIỆT NAM)”

### Chi tiết Sự kiện
- **Thời gian:** 27/01/2026
- **Địa điểm:** Văn phòng AWS Việt Nam (Tầng 26 & 36), TP. Hồ Chí Minh
- **Vai trò Tham dự:** Người tham dự (Thực tập sinh First Cloud Journey)

### Mục tiêu Sự kiện

- Cập nhật các đợt phát hành sản phẩm lớn và tin tức từ AWS re:Invent 2025 tại Las Vegas.
- Khám phá chuyên sâu về AI Tạo sinh (Generative AI), với trọng tâm đặc biệt vào Amazon Bedrock và Agentic AI.
- Khám phá các cải tiến gần đây về lưu trữ dữ liệu và quản lý hạ tầng, nổi bật là S3 và SageMaker.
- Kết nối và giao lưu với các chuyên gia công nghệ địa phương cùng các Solution Architect của AWS.

### Diễn giả

- **Anh Thi** – Solution Architect (Chủ đề: Agents và AI Tạo sinh)
- **Anh Tùng** – Diễn giả (Chủ đề: Agentic Search và OpenSearch)
- **Nhiều Account Manager và Solution Architect của AWS**

### Những Điểm Nổi bật Chính

#### Phiên 1: AI Tạo sinh & Agents
- **Các Mô hình Amazon Nova**: Tổng quan về các mô hình nền tảng (foundation models) mạnh mẽ mới nhất.
- **Bedrock Agents**: Kiểm tra chi tiết về Flows, Điều phối (Orchestration), và các tính năng Guardrails cùng Bộ nhớ (Memory) mới được giới thiệu.
- **Agentic AI**: Sự chuyển đổi từ các chatbot cơ bản sang các agent độc lập có khả năng xử lý các quy trình phức tạp, đa giai đoạn.

#### Phiên 2: SageMaker Unified Studio & Các cập nhật của S3
- **Unified Studio**: Một môi trường phát triển tích hợp (IDE) hợp nhất các Kỹ sư AI, Nhà khoa học Dữ liệu và Kỹ sư Dữ liệu.
- **S3 Tables**: Hỗ trợ tích hợp sẵn trên S3 cho định dạng bảng mở Apache Iceberg.
- **S3 Vector**: Một khả năng mới cho việc lưu trữ vector nguyên bản trên S3, mang lại sự tiết kiệm chi phí đáng kể.

#### Phiên 3 & 4: Tìm kiếm & AI Đa phương thức (Multimodal)
- **OpenSearch Serverless**: Liên kết Agentic Memory với Model Context Protocol (MCP).
- **Nova Multimodal Embeddings**: Chuyển đổi nội dung hình ảnh và video thành các vector có thể tìm kiếm được.
- **Bedrock Data Automation**: Tối ưu hóa việc trích xuất dữ liệu có giá trị từ các tệp đa phương tiện.

#### Phiên 5: Hạ tầng AI
- **SageMaker HyperPod**: Điều phối tinh vi cho các cụm GPU quy mô lớn.
- **SageMaker MLflow**: Theo dõi và quản lý toàn diện từ đầu đến cuối cho các dự án Học máy (ML).

### Những Bài học Quan trọng

#### Tương lai thuộc về Agentic
- **Luồng công việc Tự trị (Autonomous Workflows)**: Sự tiến hóa từ việc tạo prompt (Prompt Engineering) sang thiết kế agent (Agent Engineering). Các agent nhận thức được ngữ cảnh giờ đây có thể thực hiện các tác vụ phức tạp mà không cần sự giám sát liên tục của con người.
- **Guardrails là thiết yếu**: Sự trỗi dậy của các agent tự trị đòi hỏi các ranh giới bảo mật nghiêm ngặt và chính sách chặt chẽ.

#### Tối ưu hóa Dữ liệu & Điện toán
- **Hiệu quả Chi phí**: S3 Vector thay đổi mạnh mẽ cục diện cho các dự án bị hạn chế về ngân sách nhưng phụ thuộc vào tìm kiếm vector, chẳng hạn như các ứng dụng RAG.
- **Cộng tác**: SageMaker Unified Studio đơn giản hóa quá trình chuyển đổi từ chuẩn bị dữ liệu sang huấn luyện mô hình.

### Ứng dụng vào Công việc

- **Tích hợp Dự án (Nền tảng Bảo mật)**:
    - Đánh giá **Bedrock Agents** để tự động hóa các bài kiểm tra quét lỗ hổng (ví dụ: sử dụng một agent để thực thi quét, phân tích nhật ký và tạo báo cáo).
- Triển khai **S3 Vector** để lưu trữ các chữ ký lỗ hổng và nhật ký một cách tiết kiệm chi phí trong hạ tầng backend.
- **Tinh chỉnh Kiến trúc**: Đánh giá việc tích hợp **Cognito** để xử lý xác thực người dùng, lấy cảm hứng từ các cuộc trò chuyện với các Solution Architect.
- **Thực tiễn tốt nhất**: Áp dụng triết lý "Ưu tiên Serverless" học được trong các phiên thảo luận kết nối.

### Trải nghiệm Sự kiện

Việc tham gia **“AWS re:Invent 2025 Recap”** tại trụ sở AWS Việt Nam đánh dấu một cột mốc quan trọng trong quá trình thực tập của tôi. Những khoảnh khắc nổi bật bao gồm:

#### Mở rộng Tầm nhìn
- Các bài thuyết trình đã làm rõ rằng **Agentic AI** chính là làn sóng lớn tiếp theo. Việc quan sát bản demo của Flow Agent đã khơi nguồn những ý tưởng mới cho tính năng báo cáo của dự án chúng tôi.
- Việc hiểu về **Multimodal RAG** đã mở ra những trường hợp sử dụng tiềm năng vượt ra ngoài văn bản đơn thuần, điều này sẽ rất quan trọng cho các giai đoạn sau của Nền tảng Bảo mật của chúng tôi khi cần đánh giá ảnh chụp màn hình.

#### Xác thực Kỹ thuật
- Việc ra mắt **S3 Vector** đã xác nhận nhu cầu của nhóm chúng tôi về một phương pháp lưu trữ tiết kiệm dành riêng cho việc phân tích nhật ký.
- Việc trao đổi với **Anh Thi** và các Solution Architect khác đã giải tỏa sự nhầm lẫn về các tiêu chuẩn **Serverless** và **IAM Policies** mà tôi đã gặp khó khăn trong Tuần 3.

#### Cộng đồng & Kết nối
- Môi trường tại Văn phòng AWS rất sôi động, tràn ngập các nhà phát triển và kỹ sư trao đổi về các chiến lược giải quyết vấn đề thực tế.
- Tôi đã tận dụng cơ hội này để trò chuyện về **dự án nhóm “TheBois”** với các chuyên gia dày dạn kinh nghiệm, thu được những góc nhìn quan trọng về thiết kế kiến trúc của chúng tôi.