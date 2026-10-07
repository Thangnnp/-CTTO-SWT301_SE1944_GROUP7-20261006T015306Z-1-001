# IE Criteria - LLM for Unit Test Case Generation
**Thành viên:** Lý Minh Khôi
**RQ:** "Đối với Java/Python functions ở cyclomatic complexity trung bình (P), GPT-4 tự động sinh unit test cases (I) so với test cases viết thủ công bởi sinh viên (C) có đạt branch coverage >=80% và mutation score >=60% không (O)?"
**PICO:** - **P (Population):** Java/Python functions có độ phức tạp vòng cung (Cyclomatic Complexity) trung bình từ 5-15.
- **I (Intervention):** GPT-4 tự động sinh unit test cases (Automated unit test generation).
- **C (Comparison):** Test cases do sinh viên viết tay thủ công hoặc sinh tự động bằng công cụ truyền thống (Randoop/EvoSuite).
- **O (Outcome):** Độ bao phủ nhánh (Branch coverage) đạt >= 80% và điểm kiểm thử đột biến (Mutation score) đạt >= 60%.

---

## ## Inclusion Criteria (IC) – Paper PHẢI có đủ tất cả các điều kiện sau:
* **IC-L:** Paper phải được viết bằng tiếng Anh.
* **IC-Y:** Xuất bản từ năm 2020 đến nay (Giai đoạn bùng nổ của Large Language Models - LLMs). Lý do: GPT-3+ bắt đầu phổ biến từ 2020, GPT-4 xuất hiện từ 2023.
* **IC-T:** Đăng trên các hội nghị (Conference) hoặc tạp chí (Journal) khoa học uy tín về Software Engineering (như ICSE, ASE, ISSTA, FSE...) hoặc các kho lưu trữ học thuật chính thức.
* **IC-P:** Về task cụ thể: Tập trung vào việc sinh unit test tự động (Unit test generation) cho các hàm hoặc mã nguồn phần mềm.
* **IC-I:** Dùng kỹ thuật cụ thể: Sử dụng các mô hình ngôn ngữ lớn (LLM như GPT-4, GPT-3.5, Codex, Llama...) để sinh test.
* **IC-E:** Có ít nhất 1 con số kết quả cụ thể (được trình bày trong Table hoặc Figure của paper gốc) thể hiện các chỉ số đo lường như Test Coverage (Branch/Line coverage) hoặc Mutation Score.

---

## ## Exclusion Criteria (EC) – Loại ngay nếu BẤT KỲ điều kiện nào sau đây đúng:
* **EC-D:** Trùng lặp (Duplicate) với các paper đã được thành viên khác trong nhóm chọn hoặc đã quét ở database trước.
* **EC-A:** Không truy cập được nội dung đầy đủ (Không có full-text, bị dính paywall không tải được kể cả khi dùng các nguồn hỗ trợ).
* **EC-S:** Paper quá ngắn (Dưới 4 trang, thuộc dạng extended abstract, poster, hoặc short paper).
* **EC-N:** Không có nghiên cứu thực nghiệm (Thuộc dạng position paper, vision paper, bài hướng dẫn tutorial hoặc tổng quan lý thuyết không có số liệu chạy thử).
* **EC-O:** Không đúng trọng tâm chủ đề (Không về topic): Tập trung vào test giao diện (UI Testing), test hệ thống (System Testing), sửa lỗi code (Bug fixing) hoặc sinh code tổng quát (Code generation) mà không đánh giá trực tiếp việc sinh Unit Test.