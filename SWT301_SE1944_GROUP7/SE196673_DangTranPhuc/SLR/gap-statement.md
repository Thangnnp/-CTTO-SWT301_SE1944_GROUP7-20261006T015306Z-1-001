# Gap Statement – LLM-based Automated Unit Test Generation
**Thành viên:** Đặng Trần Phúc
**MSSV:** SE196673
Evidence table: N = 22 papers

---

## Các khoảng trống phát hiện

### GAP-T (Technology): Thiếu nghiên cứu đánh giá GPT-4 với hàm mức độ phức tạp cyclomatic trung bình (CC 5–15) đo bằng Lizard
**Bằng chứng:** Các nghiên cứu như *HITS (Wang 2024)* và *ChatGPT vs SBST (Tang 2023)* đo branch coverage nhưng không phân tích theo mức CC cụ thể. Chỉ có *LLMs as Test Generators (Silva 2025)* và *Benchmarking LLMs (Huang 2025)* đề cập đến mối quan hệ CC và chất lượng test, nhưng không kiểm soát dải CC 5–15 một cách có hệ thống và chưa dùng Lizard làm công cụ đo CC chuẩn.

### GAP-M (Metric): Thiếu so sánh đồng thời GPT-4 vs Randoop vs student-written trên cùng dataset
**Bằng chứng:** Đa số các paper (ví dụ: *Code-Aware Prompting 2024*, *Mutation-Guided at Meta 2025*) chỉ so sánh GPT-4 với EvoSuite hoặc baseline prompting. Chưa có paper nào so sánh đầy đủ ba nhóm: GPT-4 sinh test, sinh viên viết test và Randoop trên cùng bộ hàm Java/Python ở CC 5–15. Thiếu nền so sánh ba chiều này làm khó đánh giá toàn diện hiệu quả của GPT-4.

### GAP-D (Dataset): Thiếu dataset Java/Python được kiểm soát ở dải CC 5–15 đo bằng Lizard với ít nhất 50 hàm
**Bằng chứng:** Dữ liệu thử nghiệm chủ yếu dùng Defects4J hoặc các dự án open-source lớn (ví dụ: *HITS 2024*, *Effective Test Generation 2023*) mà không kiểm soát mức độ phức tạp. *LLMs as Test Generators (Silva 2025)* có phân tích CC nhưng không giới hạn hàm ở dải CC 5–15 và không dùng Lizard. Chưa có benchmark nào được xây dựng riêng cho Java/Python functions có CC 5–15 để thử nghiệm khả năng của LLM.

---

## Phát biểu GAP tổng hợp
Các phương pháp hiện tại chủ yếu đánh giá LLM-generated tests trên các Academic Benchmarks hoặc dự án lớn mà không phân tích theo mức độ phức tạp cyclomatic cụ thể. Đặc biệt, chưa có nghiên cứu nào so sánh đồng thời GPT-4, Randoop và student-written tests trên cùng tập hàm Java/Python có CC 5–15 đo bằng Lizard, với các ngưỡng rõ ràng về branch coverage và mutation score. Đây chính là khoảng trống mà nghiên cứu này nhằm lấp đầy.
