# Gap Statement – LLM for Automated Acceptance Test Case & Unit Test Case Generation
**Thành viên:** Phùng Thanh Nhân
Evidence table: N = 20 papers

## Các khoảng trống phát hiện

### GAP-T (Technology): Thiếu so sánh trực tiếp GPT-4o vs expert viết Acceptance Test Case tay trên user stories Connextra
**Bằng chứng:** Cột Tool/LLM – Ferreira 2025 và Fonseca 2025 so sánh với người dùng thực tế, không phải expert trong môi trường kiểm soát. Hassani 2025 dùng Claude + Llama nhưng domain là pháp lý, không phải user stories phần mềm dạng Connextra.

### GAP-M (Metric): Thiếu đo Đánh giá Ngữ nghĩa Định lượng (Semantic Similarity) trên Văn bản Test Case tự nhiên từ user stories Connextra
**Bằng chứng:** Cột Metric – Hassani 2025 đo định tính; Fonseca 2025 đo syntax rate; Rathnayake 2026 đo semantic similarity nhưng từ các mô tả yêu cầu chung (general requirements), không phải Connextra format chuẩn. Chưa có paper nào đo Cosine Similarity/BLEU trên tài liệu test case sinh ra từ khuôn mẫu Connextra.

### GAP-T2 (Technology – Topic 2): Thiếu so sánh GPT-4 với sinh viên viết unit test thủ công ở quy mô đủ lớn
**Bằng chứng:** Cột Tool/LLM – Díaz-Arrieta 2024 có so sánh LLM vs human nhưng dataset nhỏ, chưa đo mutation score. Wang 2025, Khelladi 2025, Huang 2025 so sánh với EvoSuite/Randoop, không phải người viết tay.

### GAP-D (Dataset): Thiếu dataset tích hợp cả Acceptance Test Case generation và Unit Test generation trên cùng codebase
**Bằng chứng:** Cột Dataset – mỗi paper dùng dataset riêng biệt. Chưa có nghiên cứu đánh giá đồng thời cả 2 task trên cùng project thực tế từ tầng đặc tả yêu cầu đến mã nguồn hàm.

## Phát biểu GAP tổng hợp
Mặc dù LLM đã chứng minh khả năng sinh test case chất lượng cao, vẫn thiếu: (1) đo semantic similarity định lượng trên tài liệu Acceptance Test Case viết bằng ngôn ngữ tự nhiên từ nguồn user stories Connextra, (2) so sánh GPT-4 với sinh viên viết test thủ công quy mô lớn về branch coverage và mutation score, (3) đánh giá đồng thời cả hai tầng kiểm thử này trên cùng một pipeline phát triển phần mềm.