# **Hypotheses Draft —  LLM Unit Test Case Generation** 

Ngày: 2026-06-09 

## **RQ1 — Line Coverage**

**H0₁:** Không có sự khác biệt có ý nghĩa thống kê về Line Coverage (JaCoCo 0.8.11) giữa GPT-4o-mini, Gemini-1.5-Flash, DeepSeek-V2-Chat và Llama-3.1-8B khi sinh unit test (zero-shot, temperature=0) trên 30 Defects4J focal methods (Kruskal-Wallis, α=0.05).

**H1₁:** Ít nhất một LLM đạt Line Coverage khác biệt có ý nghĩa thống kê so với ít nhất một LLM khác (Kruskal-Wallis p \< 0.05; post-hoc Dunn với Bonferroni correction; α adjusted \= 0.05/6 \= 0.0083 per pair).

**Statistical test dự kiến:** Kruskal-Wallis (4 nhóm độc lập, output liên tục) \+ Dunn/Bonferroni (post-hoc 6 cặp) \+ Cliff's delta (effect size) | α \= 0.05

*Lý do Kruskal-Wallis: 4 nhóm độc lập; Line Coverage là output liên tục (0–100%); phân phối không đảm bảo normal với n=30 mỗi nhóm; non-parametric an toàn hơn ANOVA (Arcuri & Briand, ICSE'11).*

*Cliff's delta thresholds: negligible \< 0.147 | small 0.147–0.33 | medium 0.33–0.474 | large \> 0.474*

## **RQ2 — Branch Coverage**

**H0₂:** Không có sự khác biệt có ý nghĩa thống kê về Branch Coverage (JaCoCo 0.8.11) giữa GPT-4o-mini, Gemini-1.5-Flash, DeepSeek-V2-Chat và Llama-3.1-8B khi sinh unit test (zero-shot, temperature=0) trên 30 Defects4J focal methods (Kruskal-Wallis, α=0.05).

**H1₂:** Ít nhất một LLM đạt Branch Coverage khác biệt có ý nghĩa thống kê so với ít nhất một LLM khác (Kruskal-Wallis p \< 0.05; post-hoc Dunn với Bonferroni correction).

**Statistical test dự kiến:** Kruskal-Wallis \+ Dunn/Bonferroni \+ Cliff's delta | α \= 0.05

*Lý do giống RQ1: Branch Coverage cũng là output liên tục, 4 nhóm độc lập. Branch coverage đòi hỏi cao hơn Line Coverage — test phải cover cả true và false condition của mỗi if/else.*

## **RQ3 — Test Smell Density**

**H0₃:** Không có sự khác biệt có ý nghĩa thống kê về Test Smell Density (số smells / số tests, đo bằng tsDetect v1.0) giữa GPT-4o-mini, Gemini-1.5-Flash, DeepSeek-V2-Chat và Llama-3.1-8B khi sinh unit test (zero-shot, temperature=0) trên 30 Defects4J focal methods (Kruskal-Wallis, α=0.05).

**H1₃:** Ít nhất một LLM tạo ra Test Smell Density khác biệt có ý nghĩa thống kê so với ít nhất một LLM khác.

**Statistical test dự kiến:** Kruskal-Wallis \+ Dunn/Bonferroni \+ Cliff's delta | α \= 0.05

*Lý do: Smell Density là output liên tục (ratio), 4 nhóm độc lập. tsDetect là static analysis — không cần execute test, chạy nhanh song song với coverage measurement. Baseline: Ouedraogo 2024 báo cáo \~34% smell density với GPT-3.5/GPT-4.*

*5 smell types được track: Assertion Roulette, Empty Test, Eager Test, Magic Number Test, Redundant Assertion — validated trong Ouedraogo 2024\.*

## **RQ4 — Few-shot vs Zero-shot**

**H0₄:** Few-shot prompting (3 examples) không cải thiện có ý nghĩa thống kê Line Coverage so với zero-shot prompting cho bất kỳ LLM nào trong 4 LLMs trên 30 Defects4J focal methods (Wilcoxon signed-rank, α=0.05).

**H1₄:** Few-shot prompting cải thiện có ý nghĩa thống kê Line Coverage so với zero-shot prompting cho ít nhất một LLM (Wilcoxon signed-rank, p \< 0.05).

**Statistical test dự kiến:** Wilcoxon signed-rank test (paired — cùng 30 focal methods, 2 conditions) \+ Cliff's delta | α \= 0.05

*Lý do Wilcoxon signed-rank: Zero-shot và few-shot được chạy trên CÙNG 30 focal methods → paired/matched samples. Output liên tục, non-normal → Wilcoxon thay vì paired t-test. Test riêng cho từng LLM (4 tests) → áp dụng Bonferroni: α adjusted \= 0.05/4 \= 0.0125.*

## **RQ5 — Mutation Score *(đo nếu kịp sau ngày 4\)***

**H0₅:** Không có sự khác biệt có ý nghĩa thống kê về Mutation Score (PIT 1.15.0) giữa GPT-4o-mini, Gemini-1.5-Flash, DeepSeek-V2-Chat và Llama-3.1-8B khi sinh unit test (zero-shot, temperature=0) trên compilable tests từ 30 Defects4J focal methods (Kruskal-Wallis, α=0.05).

**H1₅:** Ít nhất một LLM đạt Mutation Score khác biệt có ý nghĩa thống kê so với ít nhất một LLM khác.

**Statistical test dự kiến:** Kruskal-Wallis \+ Dunn/Bonferroni \+ Cliff's delta | α \= 0.05

*Lưu ý: Chỉ tính Mutation Score trên các tests compile được. Nếu compilability rate \< 34% cho một LLM → loại LLM đó khỏi RQ5, ghi vào limitations. PIT runtime \~3h cho 30 methods — chỉ chạy nếu còn buffer sau ngày 4\.*

