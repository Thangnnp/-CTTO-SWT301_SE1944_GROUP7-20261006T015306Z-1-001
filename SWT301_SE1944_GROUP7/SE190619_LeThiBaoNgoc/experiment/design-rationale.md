# **Experiment Design Rationale — LLM Unit Test Case Generation (REVISED)**

Ngày: 2026-06-09 | GAP source: SLR/gap-analysis.md

---

## **Bảng Quyết Định**

| Quyết định | Giá trị | Nguồn gốc |
| ----- | ----- | ----- |
| **LLM/Tool** | GPT-4o-mini (`gpt-4o-mini-2024-07-18`), Gemini-1.5-Flash (`gemini-1.5-flash-002`), DeepSeek-V2-Chat (`deepseek-chat`), Llama-3.1-8B (Ollama local `llama3.1:8b`) | GAP-T: 4 free/open-source models chưa được so sánh hệ thống; tất cả $0 |
| **Dataset** | Defects4J v2.0 — 3 projects × 10 focal methods \= **30 cases** (Lang × 10, Math × 10, Chart × 10\) | GAP-S: 30/54 papers nêu "limited benchmark" → downscope có cơ sở; Defects4J public GitHub |
| **Metric chính** | Line Coverage (%) — JaCoCo 0.8.11 | Coverage là nhóm metric phổ biến nhất (Line: 20 papers, Branch: 19 papers); JaCoCo chuẩn Java, free |
| **Metric phụ 1** | Branch Coverage (%) — JaCoCo 0.8.11 | HITS'24 dùng Line+Branch trên Defects4J — evaluation paradigm gần nhất |
| **Metric phụ 2** | Mutation Score (%) — PIT 1.15.0 *(đo nếu kịp thời gian)* | Human baseline \= 40.4% (TABLE IV); AgoneTest'25; chỉ đo nếu còn thời gian sau ngày 4 |
| **Metric phụ 3** | Test Smell Density — tsDetect v1.0 (free, GitHub) | GAP-M: Ouedraogo 2024 duy nhất đo smell; tsDetect static analysis, không cần execute |
| **Metric phụ 4** | Compilability Rate (%) — javac 21 | Gate đầu tiên; ChatTester'24 baseline \= 34.3% |
| **Baseline type** | Comparative: GPT-4o-mini là anchor (nhiều nhất trong free tier category); EvoSuite 1.2.0 là lower bound | Claim type \= comparative; GPT family dominant trong evidence table |
| **Threshold RQ1 (Line Coverage)** | ≥ 60% | Case 2: floor LLM \= 55.4% (Gemini-1.5-Pro zero-shot, TABLE IV); threshold \= 60% làm tròn lên 5% |
| **Threshold RQ2 (Branch Coverage)** | ≥ 45% | Case 2: floor human \= 48.7% (human-written tests, TABLE IV); threshold \= 45% ngang human |
| **Threshold RQ3 (Mutation Score)** | ≥ 40% | Case 2: floor human \= 40.4% (TABLE IV); threshold cũ 65% không thực tế vì human chỉ 40.4% |
| **Threshold RQ4 (Compilability)** | ≥ 34% | Case 2: floor \= 34.3% (ChatTester'24, FSE) — conservative lower bound |
| **Pipeline base** | HITS: High-Coverage via Method Slicing (2024, ASE) | Score 3/3: Defects4J \+ Line/Branch \+ multi-model; evaluation paradigm gần nhất |
| **Prompt strategy** | Zero-shot \+ Few-shot (3 examples từ Lang project) | HITS'24 và Kang'23 LIBRO dùng few-shot trên Defects4J |
| **Temperature** | 0 (tất cả LLMs) | Reproducibility — standard trong empirical SE |
| **Statistical test** | Kruskal-Wallis \+ Dunn/Bonferroni \+ Cliff's delta | 4 nhóm độc lập, output liên tục, non-normal |

---

## **Lý giải Threshold**

**Threshold Line Coverage ≥ 60% — Case 2 — floor \= 55.4% từ Gemini-1.5-Pro zero-shot (TABLE IV):** Trong evidence table, line coverage tuyệt đối dao động từ 55.4% (Gemini-1.5-Pro zero-shot, TABLE IV) đến 94% (IntUT'25). Human-written tests đạt 73.2% (TABLE IV). Chọn floor \= 55.4% và làm tròn lên threshold \= 60% vì: (1) đây là kết quả thấp nhất của LLM trên benchmark tương tự; (2) threshold 60% nằm giữa floor LLM (55.4%) và human baseline (73.2%) — mức tối thiểu có ý nghĩa thực tế; (3) không tự đặt mà derive từ kết quả thực nghiệm. *Ghi rõ: "floor=55.4% từ Gemini-1.5-Pro zero-shot (TABLE IV), threshold=60%"*

**Threshold Branch Coverage ≥ 45% — Case 2 — floor human \= 48.7% từ TABLE IV:** Branch coverage trong TABLE IV dao động từ 22.6% (Gemini zero-shot) đến 79.8% (Llama few-shot); human tests đạt 48.7%. Chọn human baseline làm reference vì: (1) floor LLM zero-shot (22.6%) quá thấp, không phản ánh capability thực; (2) ngang human là mức chấp nhận được trong thực tế. Threshold \= 45% (làm tròn xuống từ 48.7%). *Ghi rõ: "floor human=48.7% từ TABLE IV, threshold=45%"*

**Threshold Mutation Score ≥ 40% — Case 2 — floor human \= 40.4% từ TABLE IV:** Mutation score trong TABLE IV: Gemini zero-shot 30.1%, GPT-4o-mini zero-shot 44.5%, human 40.4%. Threshold cũ 65% không thực tế: (1) human chỉ đạt 40.4% — không có lý do đặt bar cao hơn human; (2) Gemini zero-shot 30.1% — threshold 65% loại bỏ gần hết zero-shot conditions. Threshold mới \= 40% ngang human baseline. *Ghi rõ: "floor human=40.4% từ TABLE IV, threshold=40%"*

**Threshold Compilability ≥ 34% — Case 2 — floor \= 34.3% từ ChatTester'24 (FSE):** Compilability trong evidence table dao động từ 34.3% (ChatTester'24) đến 70% (ASTER'24). Floor \= 34.3% là conservative lower bound: LLM nào không đạt 34% tệ hơn ChatGPT 2023, không đủ điều kiện đánh giá coverage. *Ghi rõ: "floor=34.3% từ ChatTester'24 (FSE), threshold=34%"*

---

## **Chi tiết Pipeline ($0 implementation)**

INPUT

  Defects4J v2.0 focal method

  (30 methods: Lang×10, Math×10, Chart×10)

  \+ class context (imports, fields, constructor)

  \+ test class skeleton (package \+ imports)

          ↓

PROMPT LAYER — 2 conditions per method

  \[C1\] Zero-shot:

       "Generate a JUnit 5 unit test for the following

        Java method. Only output the test code."

  \[C2\] Few-shot (3 examples từ Lang project):

       "Here are 3 examples of Java unit tests.

        Generate a similar test for the method below."

  Temperature \= 0 | Max tokens \= 1024

          ↓

4 LLMs — parallel API calls ($0)

  ├── GPT-4o-mini  (OpenAI free tier)          \[ANCHOR BASELINE\]

  ├── Gemini-1.5-Flash  (Google free: 1500/day)

  ├── DeepSeek-V2-Chat  (DeepSeek free tier)

  └── Llama-3.1-8B  (Ollama local — 100% free)

          ↓

COMPILE CHECK

  javac 21 \+ Defects4J project classpath

  → Compilability Rate per LLM (%)

          ↓  (chỉ test compile được tiếp tục)

COVERAGE MEASUREMENT

  JaCoCo 0.8.11 (Maven plugin, free)

  → Line Coverage (%), Branch Coverage (%)

          ↓  (nếu còn thời gian sau ngày 4\)

MUTATION TESTING

  PIT 1.15.0 (Maven plugin, free)

  Mutators: CONDITIONALS\_BOUNDARY, NEGATE\_CONDITIONALS,

            MATH, INCREMENTS

  → Mutation Score (%)

          ↓  (song song với coverage, static analysis)

TEST SMELL DETECTION

  tsDetect v1.0 (static analysis, free, GitHub)

  Smells tracked: Assertion Roulette, Empty Test,

                  Eager Test, Magic Number Test,

                  Redundant Assertion

  → Smell Density per LLM (smells/test)

          ↓

STATISTICAL ANALYSIS

  RQ1-RQ3: Kruskal-Wallis (4 groups, α=0.05)

           \+ post-hoc Dunn (Bonferroni correction)

           \+ Cliff's delta (effect size)

  RQ4:     Wilcoxon signed-rank (paired, zero vs few-shot)

           \+ Cliff's delta

  Tools: Python 3.11

         scipy.stats (Kruskal-Wallis, Wilcoxon)

         scikit\_posthocs (Dunn/Bonferroni)

         numpy, pandas, matplotlib (boxplots)

---

## **Lý giải Chọn 4 LLMs ($0)**

| LLM | Version | Cost | Lý do chọn | Đại diện |
| ----- | ----- | ----- | ----- | ----- |
| **GPT-4o-mini** | gpt-4o-mini-2024-07-18 | Free tier (OpenAI) | GPT family dominant trong literature (9 papers); free tier accessible | Commercial small model |
| **Gemini-1.5-Flash** | gemini-1.5-flash-002 | Free: 1,500 req/day | Google model, chỉ 3 papers trong evidence table; flash variant \= free | Commercial fast model |
| **DeepSeek-V2-Chat** | deepseek-chat | Free tier (deepseek.com) | Chỉ 2 papers; open-weights; Cabral 2025 so với ChatGPT nhưng không với Gemini/Llama | Open-weights commercial |
| **Llama-3.1-8B** | llama3.1:8b (Ollama) | $0 hoàn toàn | Chỉ 1 paper trong evidence table (Mathews'24); đại diện fully open-source; chạy local | Fully open-source |

**Lý do không chọn Claude/GPT-4o:** Cần trả tiền → vi phạm zero-cost constraint. Claude chỉ có free tier rất hạn chế, không đủ cho 240 API calls.

**Lý do không chọn Llama-3.1-70B:** Cần GPU 40GB+ → vi phạm compute constraint. Llama-3.1-8B chạy được trên laptop 8GB RAM.

---

## **Lý giải Chọn Dataset — Defects4J v2.0, 30 methods**

**Tại sao Defects4J:**

* Benchmark chuẩn Java, public GitHub (github.com/rjust/defects4j)  
* Dùng trong 4 papers có PDF: HITS'24, MocklessTester'26, TestWars'25, EvoGPT'25  
* Có ground truth sẵn — không cần annotation  
* Có Maven build system — JaCoCo/PIT tích hợp dễ

**Tại sao chỉ 30 methods (không phải 100):**

* GAP-S: 30/54 papers (55.6%) nêu "limited dataset" — downscope có precedent trong literature  
* 30 methods × 4 LLMs × 2 conditions \= 240 API calls → Gemini free tier xử lý trong \< 1 ngày  
* Đủ statistical power cho Kruskal-Wallis (n=30 per group \> ngưỡng n=20 thường dùng)  
* Nếu pipeline ổn ngày 3 → mở rộng lên 60 methods (6 projects × 10\)

**3 projects được chọn:**

* **Lang** (Apache Commons Lang) — string/utility methods, dễ understand  
* **Math** (Apache Commons Math) — algorithmic methods, test oracle rõ ràng  
* **Chart** (JFreeChart) — GUI logic, phức tạp hơn → diversity

---

## **Lý giải Chọn Statistical Test**

**Kruskal-Wallis cho RQ1 (so sánh 4 LLMs):**

* 4 nhóm độc lập (4 LLMs khác nhau)  
* Output liên tục (0–100%) nhưng phân phối không đảm bảo normal với n=30  
* Non-parametric → an toàn hơn ANOVA với n nhỏ  
* Nguồn: Arcuri & Briand (2011) "A Practical Guide for Statistical Tests in SE" — ICSE'11

**Post-hoc Dunn \+ Bonferroni:**

* Kruskal-Wallis chỉ nói "có khác biệt ở đâu đó" → Dunn test so từng cặp  
* C(4,2) \= 6 cặp → Bonferroni correction để kiểm soát Type I error  
* α adjusted \= 0.05/6 \= 0.0083 per pair

**Cliff's delta (effect size):**

* d \< 0.147: negligible | 0.147–0.33: small | 0.33–0.474: medium | \> 0.474: large  
* Quan trọng vì n=30 nhỏ — p-value có thể không significant dù difference lớn  
* Báo cáo cả statistical significance VÀ practical significance

**Wilcoxon signed-rank cho RQ2 (zero-shot vs few-shot):**

* Zero-shot và few-shot trên CÙNG 30 focal methods → paired samples  
* Non-parametric, paired → Wilcoxon (không phải Mann-Whitney)

---

## **Threats to Validity (dự kiến)**

| Loại | Threat | Mitigation |
| ----- | ----- | ----- |
| Internal | Temperature=0 có thể không đại diện use case thực | Report rõ temperature=0; ghi là limitation |
| Internal | Prompt template ảnh hưởng kết quả | So sánh zero-shot vs few-shot (2 conditions) |
| Internal | Llama-3.1-8B chạy local — latency khác nhau | Record response time; không ảnh hưởng quality metric |
| External | Chỉ 3 Java projects, 30 methods | GAP-S justification; mở rộng nếu kịp |
| External | Free tier rate limits có thể thay đổi | Lưu exact API call date \+ model version |
| Construct | JaCoCo không đo semantic correctness | Bổ sung Mutation Score (PIT) nếu có thời gian |
| Construct | tsDetect có thể miss custom smell patterns | Dùng 5 smell types được validate trong Ouedraogo 2024 |

