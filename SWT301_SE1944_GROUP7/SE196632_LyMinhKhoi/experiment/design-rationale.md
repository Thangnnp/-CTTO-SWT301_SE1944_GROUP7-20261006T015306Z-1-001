# Experiment Design Rationale – DeepSeek-V3 Test Generation
Ngày: 2026-06-08 | GAP source: Jack/SLR/gap-analysis.md

## Bảng Quyết Định

| Quyết định | Giá trị | Nguồn gốc |
| :--- | :--- | :--- |
| **LLM/Tool** | DeepSeek-V3 (API) vs GPT-4o | GAP-T – kế thừa và mở rộng từ nhóm paper dùng GPT-4 (EASE 2025) và DeepSeek (SBQS 2025). |
| **Dataset** | Defects4J (5 Java projects chọn lọc) | Kế thừa benchmark chuẩn từ các bài báo (ICSE 2023 Libro, ISSTA 2024, ASE 2024 HITS). |
| **Metric chính** | Mutation Score (Tỷ lệ diệt mutant) | GAP-M – Lấy từ paper (SBQS 2025) và (ICST 2024 MOTIF). |
| **Metric phụ** | Redundant Assertion Density (%) | Phân tích Test Smell theo định nghĩa của paper (SPLC 2024) và (ISSREW 2025). |
| **Baseline type** | system / threshold | So sánh trực tiếp hệ thống (DeepSeek vs GPT-4o) dựa trên một ngưỡng cố định (Threshold). |
| **Threshold RQ1** | Mutation Score >= 61.2% | **Case 1:** Lấy chính xác ngưỡng hiệu năng của ChatGPT từ kết quả thực nghiệm của paper *Evaluating LLM-Generated Tests with Mutation Testing (SBQS 2025)* làm mốc đối chứng. |
| **Threshold RQ2** | Redundant Assertion <= 42% | **Case 1:** Lấy từ kết quả nghiên cứu của paper *An Evaluation Framework for LLM-Generated Tests (ISSREW 2025)*. |
| **Pipeline base** | Pipeline sinh test lặp lại (Iterative Feedback) | Dựa trên kiến trúc của *TestForge: Feedback-Driven Generation (arXiv 2025)*, tinh chỉnh bằng cách chèn thêm bước kiểm tra lỗi biên dịch tự động. |

## Lý giải threshold
* **Threshold 1 (Mutation Score >= 61.2%):** Áp dụng **Case 1**. Bài báo của nhóm tác giả tại SBQS 2025 chỉ ra rằng ChatGPT đạt trung bình 61.2% mutation score trên các Java mutants. Nhóm chọn mốc này làm Baseline ngưỡng tối thiểu để chứng minh một mô hình open-source như DeepSeek-V3 có thể thay thế hoặc vượt trội hơn mô hình thương mại đóng đời cũ trong tác vụ bảo trì phần mềm hay không.
* **Threshold 2 (Redundant Assertion <=  42%):** Áp dụng **Case 1**. Theo thống kê thực nghiệm của ISSREW 2025, các framework LLM sinh test tự động tạo ra trung bình 42% khẳng định bị thừa (redundant assertions). Chúng em đặt mục tiêu pipeline tối ưu hóa prompt của mình phải kéo tỷ lệ lỗi này xuống thấp hơn mốc 42%.