# Phát Biểu Giả Thuyết & Thiết Kế Kiểm Định Thống Kê (Hypotheses & Statistical Tests)
**Thành viên:** Phùng Thanh Nhân
**Đề tài:** LLM for Automated Acceptance Test Case & Unit Test Case Generation

---

## 1. Topic 1 – Acceptance Test Case Generation

### 1.1. Cặp Giả Thuyết cho Chỉ Số Semantic Similarity ($S$)
* **Giả thuyết Không ($H_{01}$):** Độ tương đồng ngữ nghĩa trung vị giữa kịch bản Acceptance Test Case do GPT-4o zero-shot sinh ra và kịch bản do expert viết tay **nhỏ hơn 0.85**.
  $$H_{01}: \text{Median}(S) < 0.85$$
* **Giả thuyết Nghiên cứu ($H_{11}$):** Độ tương đồng ngữ nghĩa trung vị giữa kịch bản Acceptance Test Case do GPT-4o zero-shot sinh ra và kịch bản do expert viết tay **lên tới hoặc vượt quá 0.85**.
  $$H_{11}: \text{Median}(S) \ge 0.85$$

### 1.2. Kiểm Định Thống Kê Ánh Xạ
* **Test thống kê áp dụng:** **One-sample Wilcoxon signed-rank test** (Kiểm định phi tham số).
* **Mức ý nghĩa:** $\alpha = 0.05$. Nếu $p\text{-value} < \alpha$, bác bỏ $H_{01}$ và chấp nhận $H_{11}$.

---

## 2. Topic 2 – Unit Test Case Generation

### 2.1. Cặp Giả Thuyết cho Chỉ Số Branch Coverage ($BC$)
* **Giả thuyết Không ($H_{02}$):** Độ phủ nhánh trung vị của các bộ unit test do GPT-4 tự động sinh ra **nhỏ hơn 80%**.
  $$H_{02}: \text{Median}(BC_{\text{LLM}}) < 80\%$$
* **Giả thuyết Nghiên cứu ($H_{12}$):** Độ phủ nhánh trung vị của các bộ unit test do GPT-4 tự động sinh ra **lớn hơn hoặc bằng 80%**.
  $$H_{12}: \text{Median}(BC_{\text{LLM}}) \ge 80\%$$

### 2.2. Cặp Giả Thuyết cho Chỉ Số Mutation Score ($MS$)
* **Giả thuyết Không ($H_{03}$):** Điểm đột biến trung vị của các bộ unit test do GPT-4 tự động sinh ra **nhỏ hơn 60%**.
  $$H_{03}: \text{Median}(MS_{\text{LLM}}) < 60\%$$
* **Giả thuyết Nghiên cứu ($H_{13}$):** Điểm đột biến trung vị của các bộ unit test do GPT-4 tự động sinh ra **lớn hơn hoặc bằng 60%**.
  $$H_{13}: \text{Median}(MS_{\text{LLM}}) \ge 60\%$$

### 2.3. Cặp Giả Thuyết So Sánh Trực Tiếp Khả Năng Sinh Test (LLM vs Human)
* **Giả thuyết Không ($H_{04}$):** Bộ unit test do GPT-4 sinh ra có hiệu năng trung vị **không vượt trội hoặc kém hơn** so với bộ test do sinh viên viết tay.
  $$H_{04}: \text{Median}(\text{Performance}_{\text{LLM}} - \text{Performance}_{\text{Human}}) \le 0$$
* **Giả thuyết Nghiên cứu ($H_{14}$):** Bộ unit test do GPT-4 sinh ra có hiệu năng trung vị **vượt trội hơn một cách có ý nghĩa thống kê** so với bộ test do sinh viên viết tay.
  $$H_{14}: \text{Median}(\text{Performance}_{\text{LLM}} - \text{Performance}_{\text{Human}}) > 0$$

### 2.4. Kiểm Định Thống Kê Ánh Xạ
* **Test thống kê áp dụng:** **Paired Wilcoxon signed-rank test** (cho giả thuyết so sánh cặp) và **One-sample Wilcoxon signed-rank test** (so sánh với giá trị hằng số hằng định).
* **Mức ý nghĩa:** $\alpha = 0.05$. Kiểm định một đuôi (One-tailed).