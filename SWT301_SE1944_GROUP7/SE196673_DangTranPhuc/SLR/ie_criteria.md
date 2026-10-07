# IE Criteria – LLMs for Automated Unit Test Generation
**Thành viên:** Đặng Trần Phúc
**MSSV:** SE196673
**RQ:** "How effectively does GPT-4 automatic unit test generation achieve branch coverage and fault detection for Java/Python functions at medium cyclomatic complexity (CC 5–15, measured by Lizard), compared to student-written tests and Randoop-generated tests?"
**PICO:** P=[Java/Python functions with medium cyclomatic complexity (CC 5–15)] | I=[GPT-4/GPT-4o automatic unit test generation] | C=[Student-written tests & Randoop-generated tests] | O=[Branch coverage ≥ 80% & Mutation score ≥ 60%]

---

## Inclusion Criteria (IC) – paper PHẢI có đủ tất cả

| Mã | Tiêu chí |
|----|----------|
| **IC-L** | Viết bằng tiếng Anh |
| **IC-Y** | Xuất bản từ năm 2022 đến 2026 – Lý do: Các nghiên cứu ứng dụng LLM/ChatGPT vào kỹ nghệ phần mềm bùng nổ mạnh mẽ và đạt hiệu quả thực tế từ sau khi mô hình GPT-3.5/ChatGPT ra đời cuối năm 2022 |
| **IC-T** | Đăng trên conference hoặc journal – không phải blog, thesis, hay báo cáo kỹ thuật |
| **IC-P** | Về task: Tự động sinh ca kiểm thử đơn vị (Automated Unit Test Case Generation), bảo trì hoặc đánh giá chất lượng bộ test |
| **IC-I** | Dùng kỹ thuật: Mô hình ngôn ngữ lớn (LLMs), trọng tâm là thế hệ GPT-4, hoặc kỹ thuật sinh mã tương đương dựa trên AI |
| **IC-E** | Có ít nhất 1 con số kết quả thực nghiệm về độ bao phủ (coverage) hoặc điểm đột biến (mutation score) trong Table hoặc Figure của paper gốc |

## Exclusion Criteria (EC) – loại nếu BẤT KỲ điều kiện nào đúng

| Mã | Tiêu chí |
|----|----------|
| **EC-D** | Trùng lặp với paper đã có trong danh sách danh mục tìm kiếm |
| **EC-A** | Không truy cập được nội dung toàn văn (full-text) |
| **EC-S** | Dưới 4 trang (thuộc dạng extended abstract, poster, hoặc short paper) |
| **EC-N** | Không có dữ liệu thực nghiệm rõ ràng (position paper, vision paper, tutorial) |
| **EC-O** | Không về topic: Các bài báo chỉ tập trung vào sinh mã nguồn thuần túy (Code Generation), sửa lỗi tự động (Automated Program Repair/Vulnerability Fixing), sinh User Story, hoặc giải bài tập lập trình thi đấu (Olympiad Programming) |
