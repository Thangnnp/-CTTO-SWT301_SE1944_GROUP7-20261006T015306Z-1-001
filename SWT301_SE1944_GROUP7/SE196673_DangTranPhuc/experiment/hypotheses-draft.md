# Hypotheses Draft – LLM for Unit Test Case Generation
Ngày: 2026-06-08

---

## RQ1 – Branch Coverage của GPT-4 trên hàm CC 5–15

**Cấu trúc RQ:** Liệu **GPT-4o** sử dụng chiến lược **zero-shot prompting** áp dụng trên tập hàm **Java/Python có CC 5–15 (đo bằng Lizard, N ≥ 50)** có đạt được **branch coverage ≥ 80%** (ngưỡng từ Huang 2025) hay không?

**H0:** GPT-4-generated tests KHÔNG đạt branch coverage ≥ 80% trên tập hàm Java/Python có CC 5–15.
> H0: Median(Branch Coverage_GPT-4) < 80%

**H1:** GPT-4-generated tests ĐẠT branch coverage ≥ 80% trên tập hàm Java/Python có CC 5–15.
> H1: Median(Branch Coverage_GPT-4) ≥ 80%

**Statistical test dự kiến:** Wilcoxon signed-rank test (α = 0.05)
- **Lý do chọn:** Output branch coverage là dãy điểm số thập phân liên tục (0–100%), phân phối không chuẩn (non-parametric). Mục tiêu là so sánh giá trị trung vị (median) thực nghiệm với một ngưỡng cố định (80%), không so sánh hai nhóm độc lập → Wilcoxon signed-rank phù hợp hơn Mann-Whitney U.

---

## RQ2 – Mutation Score GPT-4 vs Student vs Randoop

**Cấu trúc RQ:** Liệu **GPT-4o** có đạt **mutation score ≥ 60%** (ngưỡng từ Dakhel 2023) VÀ có sự khác biệt có ý nghĩa thống kê (p < 0.05) so với **student-written tests** và **Randoop-generated tests** trên cùng tập hàm Java/Python CC 5–15 hay không?

**H0:** Mutation score của GPT-4-generated tests KHÔNG đạt ≥ 60% VÀ KHÔNG có sự khác biệt có ý nghĩa thống kê (p ≥ 0.05) so với student-written tests và Randoop-generated tests.
> H0: Median(Mutation Score_GPT-4) < 60% hoặc p ≥ 0.05

**H1:** Mutation score của GPT-4-generated tests ĐẠT ≥ 60% VÀ có sự khác biệt có ý nghĩa thống kê (p < 0.05) so với student-written tests và Randoop-generated tests.
> H1: Median(Mutation Score_GPT-4) ≥ 60% và p < 0.05

**Statistical test dự kiến:** Mann-Whitney U test (α = 0.05)
- **Lý do chọn:** Đây là bài toán so sánh chất lượng đầu ra của hai nhóm độc lập (GPT-4 vs Student, GPT-4 vs Randoop) trên biến số mutation score liên tục, phân phối không chuẩn. Mann-Whitney U phù hợp khi so sánh 2 hệ thống độc lập không giả định phân phối chuẩn — đúng với bảng phân loại output "So sánh 2 hệ thống độc lập" trong hướng dẫn.

---

## RQ3 – Tương quan CC và chất lượng test GPT-4

**Cấu trúc RQ:** Liệu **cyclomatic complexity (CC)** có tương quan âm có ý nghĩa thống kê với **chất lượng test GPT-4** (branch coverage + mutation score) trên Java và Python không?

**H0:** Không có tương quan âm có ý nghĩa thống kê giữa CC và chất lượng test GPT-4 (coverage + mutation score) trên Java và Python.
> H0: ρ ≥ 0 hoặc p ≥ 0.05

**H1:** Có tương quan âm có ý nghĩa thống kê giữa CC và chất lượng test GPT-4 (coverage + mutation score) trên Java và Python.
> H1: ρ < 0 và p < 0.05

**Statistical test dự kiến:** Spearman rank correlation (α = 0.05)
- **Lý do chọn:** CC và quality score đều là biến số thứ tự/liên tục, mối quan hệ có thể không tuyến tính → Spearman phù hợp hơn Pearson vì không yêu cầu phân phối chuẩn và xử lý tốt quan hệ đơn điệu phi tuyến tính.
