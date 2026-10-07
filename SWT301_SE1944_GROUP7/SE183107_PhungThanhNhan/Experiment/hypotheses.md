# Hypotheses – LLM for Automated Acceptance Test Case & Unit Test Case Generation
**Thành viên:** Phùng Thanh Nhân

---\n\n## Topic 1 – Acceptance Test Case Generation

**H0:** GPT-4o zero-shot **KHÔNG đạt** độ tương đồng ngữ nghĩa trung vị $S \ge 0.85$ khi sinh Acceptance Test Case văn bản tự nhiên từ user stories Connextra so với expert viết tay.
$$H_{01}: \text{Median}(S) < 0.85$$

**H1:** GPT-4o zero-shot **ĐẠT** độ tương đồng ngữ nghĩa trung vị $S \ge 0.85$ khi sinh Acceptance Test Case văn bản tự nhiên từ user stories Connextra so với expert viết tay.
$$H_{11}: \text{Median}(S) \ge 0.85$$

| Yếu tố | Dự kiến |
|--------|---------|
| **Test thống kê** | One-sample Wilcoxon signed-rank test |
| **Mức ý nghĩa** | $\alpha = 0.05$ |
| **Biến độc lập** | Phương pháp thiết kế test: GPT-4o zero-shot vs Expert viết tay |
| **Biến phụ thuộc 1** | Điểm số Semantic similarity (Cosine similarity từ mô hình embedding) |
| **Biến phụ thuộc 2** | Executable syntax rate (%) |
| **Ngưỡng chấp nhận H1** | Semantic similarity $\ge 0.85$ VÀ syntax rate cao |
| **Kỳ vọng** | Dựa trên Rathnayake 2026 và Hassani 2025: GPT-4o đạt độ tương đồng ngữ nghĩa cao; kỳ vọng H1 được chấp nhận |

---

## Topic 2 – Unit Test Case Generation

**H0:** GPT-4 tự động sinh unit test cases **KHÔNG đạt** độ phủ nhánh trung vị $BC < 80\%$ hoặc điểm đột biến trung vị $MS < 60\%$ so với test cases viết thủ công bởi sinh viên.
$$H_{02}: \text{Median}(BC_{\text{LLM}}) < 80\%$$
$$H_{03}: \text{Median}(MS_{\text{LLM}}) < 60\%$$

**H1:** GPT-4 tự động sinh unit test cases **ĐẠT** độ phủ nhánh trung vị $BC \ge 80\%$ và điểm đột biến trung vị $MS \ge 60\%$ so với test cases viết thủ công bởi sinh viên.
$$H_{12}: \text{Median}(BC_{\text{LLM}}) \ge 80\%$$
$$H_{13}: \text{Median}(MS_{\text{LLM}}) \ge 60\%$$

| Yếu tố | Dự kiến |
|--------|---------|
| **Test thống kê** | Paired Wilcoxon signed-rank test / One-sample Wilcoxon test |
| **Mức ý nghĩa** | $\alpha = 0.05$ |
| **Biến độc lập** | Phương pháp sinh: GPT-4 vs sinh viên viết tay |
| **Biến phụ thuộc 1** | Branch coverage (%) |
| **Biến phụ thuộc 2** | Mutation score (%) |
| **Ngưỡng chấp nhận H1** | Branch coverage $\ge 80\%$ VÀ Mutation score $\ge 60\%$ |
| **Kỳ vọng** | GPT-4 sẽ đạt độ phủ nhánh cao vượt trội, nhưng sinh viên có thể phát hiện một số lỗi logic sâu tốt hơn; kỳ vọng đạt ngưỡng kiểm định hằng số |