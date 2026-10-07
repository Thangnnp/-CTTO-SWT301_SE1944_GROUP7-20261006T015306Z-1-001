# Hypotheses – GPT-4 Automated Unit Test Generation
**Thành viên:** Đặng Trần Phúc
**MSSV:** SE196673

---

## RQ1: Branch Coverage của GPT-4-generated tests trên hàm CC 5–15

**H0:** GPT-4-generated tests KHÔNG đạt branch coverage ≥ 80% trên tập hàm Java/Python có CC 5–15.
**H1:** GPT-4-generated tests ĐẠT branch coverage ≥ 80% trên tập hàm Java/Python có CC 5–15.

**Statistical test dự kiến:** Wilcoxon signed-rank test (kiểm định một mẫu so với ngưỡng 80%; one-sample test trên phân phối coverage).
**Ngưỡng suy giảm hiệu suất:** Xác định bằng cách vẽ biểu đồ branch coverage theo từng mức CC (5, 6, 7, ..., 15) và tìm điểm gãy (breakpoint) mà tại đó coverage giảm xuống dưới 80%.

---

## RQ2: Mutation Score của GPT-4-generated tests so với Student-written và Randoop

**H0:** Mutation score của GPT-4-generated tests KHÔNG đạt ≥ 60% VÀ KHÔNG có sự khác biệt có ý nghĩa thống kê (p ≥ 0.05) so với student-written tests và Randoop-generated tests.
**H1:** Mutation score của GPT-4-generated tests ĐẠT ≥ 60% VÀ có sự khác biệt có ý nghĩa thống kê (p < 0.05) so với student-written tests và Randoop-generated tests.

**Statistical test dự kiến:** Mann-Whitney U test (non-parametric, không giả định phân phối chuẩn; so sánh độc lập giữa GPT-4 vs Student và GPT-4 vs Randoop trên cùng tập hàm).
**Mức ý nghĩa:** alpha = 0.05.

---

## RQ3: Tương quan giữa Cyclomatic Complexity và chất lượng test của GPT-4

**H0:** Không có tương quan âm có ý nghĩa thống kê giữa CC và chất lượng test GPT-4 (coverage + mutation score) trên Java và Python.
**H1:** Có tương quan âm có ý nghĩa thống kê giữa CC và chất lượng test GPT-4 (coverage + mutation score) trên Java và Python.

**Statistical test dự kiến:** Spearman rank correlation (non-parametric; đo tương quan giữa CC và coverage/mutation score).
**Mức ý nghĩa:** alpha = 0.05.
