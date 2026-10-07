# IE Criteria – LLM for Automated Acceptance Test Case & Unit Test Case Generation
**Thành viên:** Phùng Thanh Nhân

**RQ:** "GPT-4o zero-shot có sinh được kịch bản Acceptance Test Case truyền thống dạng văn bản tự nhiên từ user stories Connextra đạt semantic similarity $\ge 0.85$ không? GPT-4 có sinh unit test đạt branch coverage $\ge 80\%$ và mutation score $\ge 60\%$ so với sinh viên viết tay không?"

**PICO:** P=User stories Connextra & Java/Python functions | I=GPT-4o zero-shot sinh Acceptance Test Case + GPT-4 sinh unit test | C=Kịch bản Acceptance Test viết tay bởi Expert & Unit test viết thủ công bởi Sinh viên | O=Semantic similarity $\ge 0.85$, branch coverage $\ge 80\%$, mutation score $\ge 60\%$

---\n\n## Inclusion Criteria (IC) – paper PHẢI có đủ tất cả

| Mã | Tiêu chí |
|----|----------|
| **IC-L** | Viết bằng tiếng Anh |
| **IC-Y** | Xuất bản từ 2020 đến nay – Lý do: Các LLM thế hệ mới bùng nổ mạnh mẽ từ giai đoạn này |
| **IC-T** | Đăng trên hội nghị (conference) hoặc tạp chí (journal) uy tín khoa học máy tính |
| **IC-P** | Tập trung vào bài toán: sinh Acceptance Test Case từ yêu cầu phần mềm HOẶC sinh unit test tự động từ mã nguồn |
| **IC-I** | Sử dụng kỹ thuật: LLM, Generative AI, hoặc NLP (GPT, Claude, LLaMA, BERT, T5 và tương đương) |
| **IC-E** | Có dữ liệu thực nghiệm định lượng rõ ràng (Có ít nhất 1 con số kết quả trong Table hoặc Figure của paper gốc) |

## Exclusion Criteria (EC) – loại nếu BẤT KỲ điều kiện nào đúng

| Mã | Tiêu chí |
|----|----------|
| **EC-D** | Trùng lặp nội dung (Duplicate) |
| **EC-A** | Không truy cập được bản full-text |
| **EC-S** | Dưới 4 trang (bài tóm tắt, poster, short paper) |
| **EC-N** | Bài viết dạng tầm nhìn, tổng quan hệ thống hoặc hướng dẫn (no experiment) |
| **EC-O** | Không liên quan đến bài toán sinh test case tự động bằng mô hình ngôn ngữ lớn |