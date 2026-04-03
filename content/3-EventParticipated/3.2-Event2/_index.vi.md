---
title: "Sự kiện 2"
date: "2025-10-03"
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# Báo cáo Tổng kết: “AI Agents, Prompt Engineering, và các Dự án AIoT trên AWS”

### Mục tiêu Sự kiện

- Giới thiệu ý tưởng cốt lõi của AI Agents và cách chúng mở rộng các khả năng của LLM tiêu chuẩn.
- Trình bày các cách mà prompt engineering nâng cao cả chất lượng và hiệu quả của các phản hồi do AI tạo ra.
- Hiển thị các khuôn khổ AIoT thực tế tích hợp liền mạch phần cứng vật lý với các giải pháp đám mây AWS.
- Cung cấp lời khuyên hữu ích để xây dựng các ứng dụng gốc đám mây được thúc đẩy bởi AI.

### Diễn giả

- **Bánh Cẩm Vinh** – Trọng tâm: Xây dựng AI Agents sử dụng Strands
- **Nguyễn Tuấn Thịnh** – DevOps Engineer tại First Cloud AI Journey | Trọng tâm: Automated Prompt Engineering
- **Aiden Đinh** – Operation Engineer tại Katalon | Trọng tâm: Các sáng kiến AIoT

### Những Điểm Nổi bật Chính

#### Từ LLM đến AI Agents

- LLM thông thường → Bị hạn chế trong việc tạo ra các phản hồi một lần.
- AI Agents → Có khả năng suy luận phức tạp, sử dụng công cụ và đưa ra quyết định nhận thức ngữ cảnh qua nhiều bước.
- Kết nối với các dịch vụ của bên thứ ba → Tạo ra các hệ thống có tính ứng dụng cao và tự quản lý.

#### Xây dựng AI Agents với Strands

- **Các yếu tố nền tảng**: Các hướng dẫn hệ thống, các lệnh gọi công cụ và kho lưu trữ kiến thức.
- **Quy trình hoạt động**: Dữ liệu đầu vào → suy luận logic → áp dụng công cụ → kết quả đầu ra cuối cùng.
- **Lợi ích**: Chu kỳ phát triển được tăng tốc khi so sánh với thiết lập thủ công.

#### Kỹ thuật & Tối ưu hóa Prompt

- **Các thành phần quan trọng**: Chân dung (Persona), mục tiêu, bối cảnh nền tảng, giới hạn và định dạng mong muốn.
- **Các phương pháp được đề xuất**: 
  - Duy trì tính cụ thể và cấu trúc
  - Loại bỏ các hướng dẫn mơ hồ
  - Phân chia rõ ràng các phân đoạn prompt
- **Các phương pháp tinh vi**: Suy luận Chain-of-Thought, RAG (Retrieval-Augmented Generation), và prompting dựa trên chân dung.
- **Tối ưu hóa tài chính**: Các prompt chất lượng cao → giảm mức tiêu thụ token → giảm chi phí.

#### Kiến trúc Hệ thống AIoT

- **Kịch bản ứng dụng**: Hệ thống Quản lý Tủ đồ Tự động.
- **Các thành phần vật lý**: Raspberry Pi, bo mạch Arduino, đầu đọc RFID, cảm biến môi trường và camera.
- **Hạ tầng Đám mây AWS**: 
  - AWS IoT Core để kết nối thiết bị
  - Lambda để xử lý sự kiện
  - DynamoDB để lưu trữ dữ liệu
  - Rekognition để phân tích khuôn mặt
- **Mục tiêu**: Hợp lý hóa các hoạt động hàng ngày và thúc đẩy hiệu suất tổng thể của hệ thống.

#### Ví dụ Ứng dụng Thực tế

- **Ứng dụng Plutus**: Một công cụ theo dõi tài chính và quản lý ngân sách toàn diện.
- Minh họa sự phối hợp mạnh mẽ của điện toán đám mây và AI trong việc giải quyết các thách thức kinh doanh hữu hình.

### Những Bài học Quan trọng

#### Xu hướng Kiến trúc AI

- Bối cảnh AI đang chuyển dịch từ các cơ chế phản hồi - prompt cơ bản sang các hệ sinh thái phức tạp được điều khiển bởi agent.
- Các agent này tạo điều kiện cho quá trình tự động hóa sâu, logic nâng cao và khả năng tương tác hệ thống liền mạch.

#### Tầm quan trọng của Thiết kế Prompt

- Việc tạo prompt đã phát triển thành một chuyên ngành kỹ thuật đặc thù, vượt xa việc tạo văn bản đơn giản.
- Các prompt được thiết kế tỉ mỉ sẽ nâng cao: 
  - Độ chính xác
  - Độ tin cậy
  - Tiết kiệm tài chính

#### Tích hợp Đám mây + AI + IoT

- Nền tảng AWS cung cấp một bộ công cụ toàn diện để kiến trúc các giải pháp AIoT mạnh mẽ.
- Việc kết hợp phần cứng biên với các khả năng của đám mây mở đường cho các kiến trúc có khả năng mở rộng cao.

### Ứng dụng vào Công việc

- **AI Agents**: 
  - Triển khai để tự động hóa các quy trình công việc thông thường (such as analyzing logs and generating reports).
  - Xây dựng các chức năng AI đa giai đoạn tương tác.

- **Prompt Engineering**: 
  - Nâng cao chất lượng của các phản hồi AI trong các bộ công cụ hiện tại.
  - Giảm thiểu các hướng dẫn không rõ ràng và tối đa hóa hiệu quả token.

- **Thiết kế Hệ thống**: 
  - Kết hợp các khái niệm kiến trúc AIoT vào các sáng kiến sắp tới.
  - Hợp nhất các dịch vụ AWS khác nhau thành một nền tảng gắn kết.

### Trải nghiệm Sự kiện

Việc tham gia hội thảo **“AI Agents, Prompt Engineering, và các Dự án AIoT trên AWS”** đã mang lại sự kết hợp giữa kiến thức lý thuyết và các chiến lược có thể hành động liên quan đến các khuôn khổ AI đương đại. Những điểm nổi bật đáng chú ý là:

#### Học hỏi các khái niệm AI hiện đại
- Đạt được sự hiểu biết sâu sắc hơn về cách AI Agents vượt qua những hạn chế của các LLM tiêu chuẩn.
- Khám phá mối tương quan trực tiếp giữa thiết kế prompt chuyên gia, sự xuất sắc của đầu ra và hiệu quả tổng thể của hệ thống.

#### Hiểu về thiết kế hệ thống trong thế giới thực
- Sáng kiến AIoT được giới thiệu đã minh họa một cách hiệu quả việc tích hợp phần cứng vật lý với môi trường đám mây AWS.
- Hỗ trợ trong việc khái niệm hóa việc xây dựng hệ thống từ đầu đến cuối, trải dài từ các thành phần biên đến phân tích dựa trên đám mây.

#### Tiếp xúc với các công cụ và kỹ thuật thực tế
- Khám phá việc sử dụng Strands để triển khai nhanh chóng AI Agents.
- Nắm vững các phương pháp prompting tinh vi, bao gồm Chain-of-Thought và RAG.

#### Kết nối lý thuyết với thực hành
- Các bài thuyết trình trôi chảy một cách hợp lý từ các lý thuyết nền tảng đến các ứng dụng thực hành.
- Vẽ ra một bức tranh toàn diện về sự giao thoa giữa AI, điện toán đám mây và thiết kế kiến trúc.

#### Những bài học kinh nghiệm
- Các triển khai AI hiệu quả đòi hỏi các quy trình công việc có tổ chức chứ không chỉ đơn thuần là ping một mô hình.
- Chất lượng của một prompt có hậu quả trực tiếp đến cả sự thành công trong hoạt động và chi tiêu tài chính.
- Các hệ thống chức năng, thực tế phụ thuộc đáng kể vào sự hợp nhất liền mạch của các yếu tố công nghệ đa dạng.