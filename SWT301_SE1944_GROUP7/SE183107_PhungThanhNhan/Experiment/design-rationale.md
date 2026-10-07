# Thiết Kế Chi Tiết Thực Nghiệm (Experiment Design Rationale)
**Thành viên:** Phùng Thanh Nhân
**Đề tài:** LLM for Automated Acceptance Test Case & Unit Test Case Generation

---

## 1. Yếu Tố Đối Tượng Nghiên Cứu (Dataset)
* **Thành phần:** Bộ dữ liệu tích hợp gồm 2 phần ánh xạ 1-1 trên cùng một codebase:
  1. **Topic 1:** Tập hợp các User Stories được viết chuẩn hóa theo định dạng Connextra (`As a <role>, I want <feature>, So that <benefit>`).
  2. **Topic 2:** Tập hợp các hàm mã nguồn (Java và Python) tương ứng trực tiếp với các User Stories trên, được lọc để đảm bảo có **độ phức tạp vòng (Cyclomatic Complexity) ở mức trung bình (từ 3 đến 7)**.
* **Quy mẫu mẫu:** Tối thiểu 50 cặp (User Story - Function) để đảm bảo đủ lực lượng kiểm định thống kê.

---

## 2. Thiết Kế Pipeline Thực Nghiệm (Pipeline Configuration)
Cấu hình hệ thống sinh tự động được quy định nghiêm ngặt để đảm bảo tính nhất quán:
* **LLM Engines:**
  * *Topic 1 (Acceptance Test):* `gpt-4o` (phiên bản cố định `gpt-4o-2024-05-13`).
  * *Topic 2 (Unit Test):* `gpt-4` (phiên bản cố định `gpt-4-turbo`).
* **Prompting Strategy:** Sử dụng kỹ thuật **Zero-shot Prompting** kèm chỉ định nghiêm ngặt về định dạng đầu ra (System prompt ép xuất ra định dạng bảng kịch bản kiểm thử tiêu chuẩn và mã nguồn test sạch, không kèm văn bản giải thích tự do).
* **Hyperparameters:** Thiết lập mức **Temperature = 0** để triệt tiêu tính ngẫu nhiên của mô hình.

---

## 3. Xác Định Nhóm Đối Chứng (Baseline)
* **Baseline cho Topic 1:** Kịch bản Acceptance Test Case truyền thống được thiết kế thủ công bởi các Chuyên gia (Experts) có kinh nghiệm trên 3 năm trong môi trường công nghiệp.
* **Baseline cho Topic 2:** Bộ mã nguồn unit test được viết tay bởi các Sinh viên năm cuối ngành Công nghệ Phần mềm đã hoàn thành học phần Kiểm thử.

---

## 4. Hệ Thống Chỉ Số Đo Lường (Metrics & Libraries)

### 4.1. Đối với Topic 1 (Acceptance Test Case Generation)
1. **Semantic Similarity (Độ tương đồng ngữ nghĩa):** Đo lường mức độ tương đồng logic nghiệp vụ giữa kịch bản do GPT-4o sinh ra và kịch bản do Expert viết.
   * *Công cụ:* Sử dụng thư viện `sentence-transformers` với mô hình pre-trained `all-MiniLM-L6-v2` tính điểm **Cosine Similarity**.
   * *Biện luận:* Chọn Cosine Similarity thay vì BLEU/METEOR vì cấu trúc câu kiểm thử thường lặp từ nhiều. Điểm tương đồng embedding phản ánh tốt hơn ngữ nghĩa logic hành vi mà không bị phụ thuộc vào việc trùng lặp từ khóa chính xác.
2. **Executable Syntax Rate:** Tỷ lệ cấu trúc test case hợp lệ, rõ ràng, không bị lỗi logic định dạng hoặc thiếu trường bắt buộc.

### 4.2. Đối với Topic 2 (Unit Test Case Generation)
1. **Branch Coverage (Độ phủ nhánh):** Đo lường tỷ lệ các nhánh quyết định trong mã nguồn được thực thi bởi bộ test case.
   * *Công cụ:* `JaCoCo` (cho Java) và `coverage.py` (cho Python).
2. **Mutation Score (Điểm đột biến):** Đo lường năng lực phát hiện lỗi tiềm ẩn của bộ test thông qua việc tiêu diệt các biến thể mã nguồn bị lỗi (mutants).
   * *Công cụ:* `PITest` (Java) và `mutmut` (Python).

---

## 5. Thiết Lập Ngưỡng Chấp Nhận (Threshold Rationale)
* **Ngưỡng Semantic Similarity ($\ge 0.85$):** Giá trị cho thấy văn bản đạt độ tương đồng ngữ nghĩa mức độ cao, đảm bảo tính chính xác về mặt logic nghiệp vụ phần mềm so với chuyên gia.
* **Ngưỡng Branch Coverage ($\ge 80\%$):** Đây là tiêu chuẩn vàng (Industry Golden Standard) được quy định phổ biến trong công nghiệp phần mềm để đảm bảo mã nguồn được rà soát kỹ.
* **Ngưỡng Mutation Score ($\ge 60\%$):** Đạt mức $\ge 60\%$ chứng minh bộ test có khả năng phát hiện lỗi rất sâu và nhạy bén đối với các đột biến logic phức tạp.