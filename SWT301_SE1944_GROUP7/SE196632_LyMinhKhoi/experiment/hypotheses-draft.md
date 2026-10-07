# Hypotheses Draft – DeepSeek-V3 Evaluation
Ngày: 2026-06-08

## RQ1 – Năng lực diệt Mutant (Mutation Score)
* **Cấu trúc RQ:** Liệu mô hình **DeepSeek-V3** sử dụng chiến lược **Few-shot Prompting** áp dụng trên tập dữ liệu **Defects4J** có đạt được **Mutation Score $\ge$ 61.2%** (ngưỡng hiệu năng baseline của ChatGPT theo SBQS'25) hay không?
* **H0:** Chiến lược Few-shot Prompting với DeepSeek-V3 KHÔNG giúp đạt Mutation Score trung bình >= 61.2% trên tập dữ liệu Defects4J.
  $$H_0: \text{Median}(\text{Mutation Score}_{\text{DeepSeek}}) < 61.2\%$$
* **H1:** Chiến lược Few-shot Prompting với DeepSeek-V3 giúp đạt Mutation Score trung bình >= 61.2% trên tập dữ liệu Defects4J.
  $$H_1: \text{Median}(\text{Mutation Score}_{\text{DeepSeek}}) >= 61.2\%$$
* **Statistical test dự kiến:** **Wilcoxon signed-rank test** ($\alpha = 0.05$). 
  * *Lý do chọn:* Output của Mutation Score là một dãy điểm số thập phân/phần trăm liên tục, phân phối không chuẩn (non-parametric), mục tiêu là so sánh giá trị trung vị (median) thực nghiệm với một ngưỡng cố định có sẵn.

---

## RQ2 – Độ tinh gọn của Assertion (Redundant Assertions)
* **Cấu trúc RQ:** Chiến lược **Iterative Feedback Prompting** chạy trên **DeepSeek-V3** có giúp kiểm soát tỷ lệ **Redundant Assertions dưới mức 42%** (theo báo cáo của ISSREW'25) so với mô hình **GPT-4o** thông thường hay không?
* **H0:** Hệ thống sinh test bằng DeepSeek-V3 KHÔNG đạt hiệu quả tốt hơn GPT-4o, tỷ lệ Redundant Assertions vẫn >= GPT-4o (hoặc >= 42%).
  $$H_0: \text{Redundant}_{\text{DeepSeek}} >=\text{Redundant}_{\text{GPT-4o}}$$
* **H1:** Hệ thống sinh test bằng DeepSeek-V3 đạt hiệu quả tốt hơn GPT-4o, giảm tỷ lệ Redundant Assertions xuống thấp hơn hẳn so với GPT-4o.
  $$H_1: \text{Redundant}_{\text{DeepSeek}} < \text{Redundant}_{\text{GPT-4o}}$$
* **Statistical test dự kiến:** **Mann-Whitney U test** ($\alpha = 0.05$).
  * *Lý do chọn:* Đây là bài toán so sánh chất lượng đầu ra của hai hệ thống độc lập với nhau (Hệ thống chạy DeepSeek vs Hệ thống chạy GPT-4o) dựa trên biến số đo lường tỷ lệ test smell liên tục.