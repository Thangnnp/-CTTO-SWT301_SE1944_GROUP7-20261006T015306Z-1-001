\# Research Proposal: Comparative Evaluation of Free LLMs for Unit Test Case Generation on Java Benchmarks

\*\*Nhóm:\*\* Group 7    
\*\*Thành viên:\*\*  [ Lê Thị Bảo Ngọc (SE190619), Đặng Trần Phúc (SE196673), Phùng Thanh Nhân (SE183107)]

\*\*Topic code:\*\* RT-SWT-00X    
\*\*Ngày nộp:\*\* 2026-06-20   
\*\*Version:\*\* 1.1 — Cập nhật lineup LLM mới + nhóm còn 3 thành viên (Lý Minh Khôi đã rời nhóm; phần thực nghiệm/LLM Runner do Lê Thị Bảo Ngọc phụ trách)    
\*\*Trạng thái:\*\* Đang chờ phê duyệt

\---

\#\# 2\. Research Problem Statement

\#\#\# 2.1 Bối cảnh & Tầm quan trọng

Sinh unit test tự động là một trong những ứng dụng nổi bật nhất của Large Language Models (LLMs) trong Software Engineering. Tuy nhiên, phần lớn nghiên cứu hiện tại tập trung vào các model thương mại đắt tiền như GPT-4 hay Claude, tạo ra rào cản chi phí đáng kể cho cộng đồng nghiên cứu học thuật. Nghiên cứu của Wang et al. — \*"Software Testing with Large Language Models: Survey, Landscape, and Vision"\* (2024, TSE) chỉ ra rằng \*"LLMs rarely evaluated comparatively across models"\* — một khoảng trống nghiêm trọng khi researcher cần quyết định model nào phù hợp với ngân sách hạn chế. Cabral et al. — \*"Evaluating LLM-Generated Unit Tests with Mutation Testing: ChatGPT vs DeepSeek"\* (2025, SBQS) xác nhận rằng các LLM khác nhau thực sự cho kết quả mutation score khác nhau rõ rệt, nhưng chỉ so sánh 2 models.

\#\#\# 2.2 State of the Art

Các nghiên cứu gần nhất về LLM-based unit test generation cho thấy kết quả đa dạng: Wang et al. — \*"HITS: High-coverage LLM-based Unit Test Generation via Method Slicing"\* (2024, ASE) đạt 82.3% statement coverage trên Defects4J bằng GPT-3.5; Xu et al. — \*"LLM-based Mockless Unit Test Generation for Java"\* (2026, arXiv) nâng line coverage từ 68.83% lên 88.82% trên Defects4J; Kumar et al. — \*"AI-Powered Unit Test Generation via Multi-LLM Chaining"\* (2025, IEEE Access) đạt \~81% line coverage với chuỗi GPT-4o+Gemini+Claude-3.5; Cabral et al. — \*"Evaluating LLM-Generated Unit Tests with Mutation Testing: ChatGPT vs DeepSeek"\* (2025, SBQS) — DeepSeek cho kết quả ổn định hơn ChatGPT về mutation score. Tuy nhiên, không có nghiên cứu nào so sánh độc lập các free-tier models trên cùng benchmark chuẩn.

\#\#\# 2.3 GAP

\*\*GAP-T (Primary):\*\* Trong 54 nghiên cứu được khảo sát, không có nghiên cứu nào so sánh hệ thống các LLM miễn phí/mã nguồn mở (Gemini-2.5-Flash, DeepSeek-V4-Flash, Llama-4-Scout) cùng với GPT-4o-mini trên benchmark Java chuẩn (Defects4J) dưới cùng điều kiện thực nghiệm — cùng prompt template, cùng metric đo lường. Loại GAP: GAP-T. N paper support: 54 papers, 0 paper phản chứng trực tiếp.

\*\*GAP-M (Secondary):\*\* Ouedraogo et al. — \*"On the Diffusion of Test Smells in LLM-Generated Unit Tests"\* (2024, SPLC) là nghiên cứu duy nhất đo test smell density của LLM-generated tests, nhưng chỉ so sánh GPT-3.5 và GPT-4. Gemini, DeepSeek, Llama chưa được đo smell density. Loại GAP: GAP-M. N paper support: 1/54 papers đo smell.

\#\#\# 2.4 Motivation

Nếu không giải quyết GAP này, researchers tại các trường không có budget OpenAI/Anthropic không biết model nào nên dùng và kỳ vọng kết quả ra sao. Cụ thể: Gemini-2.5-Flash (free tier) hay DeepSeek-V4-Flash (free tier) có đủ tốt để thay thế GPT-4o-mini không? Nếu có — tiết kiệm đáng kể chi phí cho toàn cộng đồng SE research.

\---

\#\# 3\. Related Work

\#\#\# 3.1 Overview

| Paper | Tool/LLM | Dataset (size) | Metric | Best result | Hạn chế chính |  
|-------|----------|---------------|--------|-------------|---------------|  
| Wang et al. — \*HITS: High-coverage LLM-based Unit Test Generation via Method Slicing\* (2024, ASE) | GPT-3.5 / StarCoder | Defects4J / N/A | Line / Branch Coverage | 82.3% statement, 90.6% branch | Slicing algorithm limitations |  
| Xu et al. — \*LLM-based Mockless Unit Test Generation for Java\* (2026, arXiv) | LLM \+ context mining | Defects4J \+ Deps4J | Line / Branch / Mutation | 88.82% line, 83.74% branch | Multi-module projects |  
| Kumar et al. — \*AI-Powered Unit Test Generation via Multi-LLM Chaining\* (2025, IEEE Access) | GPT-4o \+ Gemini \+ Claude-3.5 | Enterprise Java | Line / Branch / Mutation | \~81% line coverage | Chaining cost; Java enterprise only |  
| Cabral et al. — \*Evaluating LLM-Generated Unit Tests with Mutation Testing: ChatGPT vs DeepSeek\* (2025, SBQS) | DeepSeek / ChatGPT | Java classes | Mutation Score | DeepSeek \> ChatGPT stability | Chỉ 2 models; limited diversity |  
| Kang et al. — \*Large Language Models are Few-shot Testers: Exploring LLM-based General Bug Reproduction\* (2023, ICSE) | Codex (few-shot) | Defects4J / 751 bugs | Bug Reproduction Rate | 33.5% of 751 bugs | Few-shot quality dependency |  
| Ouedraogo et al. — \*On the Diffusion of Test Smells in LLM-Generated Unit Tests\* (2024, SPLC) | GPT-3.5 / GPT-4 | 1,500 tests | Test Smell Density | \~34% smell density | Chỉ GPT family; không có Gemini/Llama |  
| Guilherme et al. — \*An Initial Investigation of ChatGPT Unit Test Generation Capability\* (2023, SBST) | ChatGPT (GPT-3.5) | Java methods | Line / Mutation / Build | Outperforms traditional tools | Training data cutoff |  
| Konstantinou et al. — \*How well LLM-based test generation techniques perform with newer LLM versions?\* (2026, arXiv) | Plain LLM (GPT versions) | Java projects | Line / Branch / Mutation | \+17.72% line vs augmented | Model names không công bố |  
| Lops et al. — \*LLMs for Automated Unit Test Generation and Assessment in Java: The AgoneTest Framework\* (2025, ASE) | Multiple LLMs | Java libs / N/A | Line / Branch / Mutation | Coverage \>65% compilable subset | Temperature sensitivity; results vary |  
| Hossain et al. — \*TOGLL: Correct and Strong Test Oracle Generation with LLMs\* (2025, ICSE) | 7 code LLMs | Java libs \+ Defects4J | Oracle Correctness / Mutation Kill | 3.8× more correct oracles than TOGA | Oracle types limited; assertion only |

\#\#\# 3.2 Pattern Analysis

Nhìn chung, \*\*coverage-based metrics\*\* (line, branch, mutation) thể hiện qua phần lớn papers (Line: 20, Branch: 19, Mutation: 27/54), cho thấy cộng đồng đã chốt bộ metrics cốt lõi. Nhìn chung, \*\*Defects4J\*\* là benchmark Java được tin cậy nhất, xuất hiện trong 4+ papers với full-text PDF. Nhìn chung, \*\*so sánh đa model\*\* vẫn còn thiếu — phần lớn papers dùng 1 model duy nhất, và các paper dùng nhiều models đều có giới hạn (chaining hoặc chỉ 2 models).

\#\#\# 3.3 GAP Mapping

| GAP | Evidence (số paper support) | Status |  
|-----|----------------------------|--------|  
| GAP-T: Free LLM comparison chưa có | 54 papers không có systematic comparison free models | Confirmed |  
| GAP-M: Smell density chưa so sánh đa-LLM | 1/54 papers đo smell (GPT-3.5/GPT-4 only) | Confirmed |  
| GAP-D: JS/TS domain thiếu | 0/54 papers cover JS/TS | Confirmed-Deferred (future work) |  
| GAP-S: Limited benchmark | 30/54 papers nêu limitation này | Confirmed — justifies downscope |

\---

\#\# 4\. Research Questions

\> \*\*Chốt tại đây. Sau khi GV phê duyệt, không được thay đổi RQ, metric, hay threshold.\*\*

\> \*\*RQ1:\*\* \[P: 30 Defects4J v2.0 focal methods (Lang×10, Math×10, Chart×10)\] \+ \[I: GPT-4o-mini, Gemini-2.5-Flash, DeepSeek-V4-Flash, Llama-4-Scout — zero-shot, temperature=0\] có đạt \[O: Line Coverage ≥ 60% (JaCoCo 0.8.11)\] và có sự khác biệt có ý nghĩa thống kê giữa các models \[C: so sánh lẫn nhau\] không?

\> \*\*RQ2:\*\* \[P: same\] \+ \[I: same\] có đạt \[O: Branch Coverage ≥ 45% (JaCoCo 0.8.11)\] và có sự khác biệt có ý nghĩa thống kê \[C: so sánh lẫn nhau\] không?

\> \*\*RQ3:\*\* \[P: same\] \+ \[I: same\] có sự khác biệt có ý nghĩa thống kê về \[O: Test Smell Density (tsDetect v1.0)\] không?

\> \*\*RQ4:\*\* \[I: Few-shot, 2 cross-project examples: Lang-1 \+ Time-24\] có cải thiện có ý nghĩa thống kê \[O: Line Coverage\] so với \[C: zero-shot\] cho từng LLM trên \[P: same\] không?

\*\*Loại claim:\*\* Comparative (so sánh giữa các hệ thống)

\*\*H0₁:\*\* GPT-4o-mini, Gemini-2.5-Flash, DeepSeek-V4-Flash và Llama-4-Scout KHÔNG có sự khác biệt có ý nghĩa thống kê về Line Coverage khi sinh unit test (zero-shot, temperature=0) trên 30 Defects4J focal methods (Kruskal-Wallis, α=0.05).    
\*\*H1₁:\*\* Ít nhất một LLM đạt Line Coverage khác biệt có ý nghĩa thống kê so với ít nhất một LLM khác.    
\*\*Metric:\*\* Line Coverage (%) — JaCoCo 0.8.11    
\*\*Ngưỡng:\*\* ≥ 60% — Case 2: floor LLM \= 55.4% (Gemini-1.5-Pro zero-shot, TABLE IV benchmark paper); threshold \= 60% làm tròn lên 5% gần nhất    
\*\*Statistical test:\*\* Kruskal-Wallis (α \= 0.05)

\*\*H0₂:\*\* 4 LLMs KHÔNG có sự khác biệt có ý nghĩa thống kê về Branch Coverage (Kruskal-Wallis, α=0.05).    
\*\*H1₂:\*\* Ít nhất một LLM khác biệt có ý nghĩa thống kê.    
\*\*Metric:\*\* Branch Coverage (%) — JaCoCo 0.8.11    
\*\*Ngưỡng:\*\* ≥ 45% — Case 2: floor human \= 48.7% (human-written tests, TABLE IV); threshold \= 45% làm tròn xuống    
\*\*Statistical test:\*\* Kruskal-Wallis (α \= 0.05)

\*\*H0₃:\*\* 4 LLMs KHÔNG có sự khác biệt có ý nghĩa thống kê về Test Smell Density (Kruskal-Wallis, α=0.05).    
\*\*H1₃:\*\* Ít nhất một LLM tạo smell density khác biệt có ý nghĩa thống kê.    
\*\*Metric:\*\* Smell Density (smells/test) — tsDetect v1.0    
\*\*Ngưỡng:\*\* So sánh tương đối; baseline \= \~34% (Ouedraogo et al. — \*On the Diffusion of Test Smells in LLM-Generated Unit Tests\* (2024, SPLC))    
\*\*Statistical test:\*\* Kruskal-Wallis (α \= 0.05)

\*\*H0₄:\*\* Few-shot KHÔNG cải thiện có ý nghĩa thống kê Line Coverage so với zero-shot cho bất kỳ LLM nào (Wilcoxon signed-rank, α=0.05).    
\*\*H1₄:\*\* Few-shot cải thiện có ý nghĩa thống kê Line Coverage cho ít nhất 1 LLM.    
\*\*Metric:\*\* Line Coverage (%) — JaCoCo 0.8.11    
\*\*Ngưỡng:\*\* ≥ 60% (Case 2: same as RQ1)    
\*\*Statistical test:\*\* Wilcoxon signed-rank (α \= 0.05)

\---

\#\# 5\. Experiment Protocol

\#\#\# 5.1 Pipeline tổng quan

1\. \*\*Checkout\*\* 30 focal methods từ Defects4J v2.0 (Lang-1→10, Math-1→10, Chart-1→10)  
2\. \*\*Build context\*\* cho từng method: class imports \+ fields \+ constructor \+ focal method code  
3\. \*\*Generate tests\*\* — gọi 4 LLM APIs song song, 2 conditions (zero-shot \+ few-shot), temperature=0  
4\. \*\*Compile check\*\* — javac 21 \+ Defects4J project classpath; ghi compilability rate  
5\. \*\*Measure coverage\*\* — JaCoCo 0.8.11 via Maven plugin trên compilable tests  
6\. \*\*Detect smells\*\* — tsDetect v1.0 static analysis trên tất cả generated tests (kể cả không compile)  
7\. \*\*Mutation testing\*\* — PIT 1.15.0 (nếu kịp sau ngày 4); mutators: CONDITIONALS\_BOUNDARY, NEGATE\_CONDITIONALS, MATH  
8\. \*\*Statistical analysis\*\* — Kruskal-Wallis \+ Dunn/Bonferroni \+ Cliff's delta (Python: scipy \+ scikit\_posthocs)

\#\#\# 5.2 Dataset

| | Chi tiết |  
|---|---|  
| \*\*Tên dataset\*\* | Defects4J v2.0 |  
| \*\*Nguồn (URL)\*\* | https://github.com/rjust/defects4j |  
| \*\*Quy mô (N)\*\* | 30 focal methods (Lang×10, Math×10, Chart×10) |  
| \*\*Domain\*\* | Java open-source libraries |  
| \*\*Preprocessing\*\* | Checkout từng bug version; extract focal method \+ class context tự động |  
| \*\*Sampling strategy\*\* | Bug ID 1–10 cho mỗi project (oldest bugs — stable, well-studied) |  
| \*\*Lý do chọn\*\* | Benchmark chuẩn Java; public GitHub; dùng trong HITS'24, MocklessTester'26, LIBRO'23, EvoGPT'25; ground truth sẵn có; không cần annotation |

\#\#\# 5.3 LLM/Tool Configuration

| Model | Version chính xác | Cost |  
|-------|------------------|------|  
| GPT-4o-mini | \`gpt-4o-mini-2024-07-18\` | Free tier (OpenAI) |  
| Gemini-2.5-Flash | \`gemini-2.5-flash\` | Free (Google AI Studio) |  
| DeepSeek-V4-Flash | \`deepseek-v4-flash\` | Free tier (platform.deepseek.com) |  
| Llama-4-Scout | \`meta-llama/llama-4-scout\` (OpenRouter) | Free (OpenRouter) |

\*\*Hyperparameters:\*\*  
\- temperature \= 0 (tất cả models)  
\- top\_p \= 1.0  
\- max\_tokens \= 1024  
\- n \= 1 (single generation per call)

\*\*Prompting strategy:\*\* Zero-shot (C1) \+ Few-shot k=2 (C2)

\*\*Prompt template C1 — Zero-shot (nguyên văn):\*\*  
\`\`\`  
Generate a JUnit 5 unit test for the following Java method.  
Only output the test class code. Do not include any explanation.

\[CLASS CONTEXT\]  
{imports}  
{class\_declaration}  
{fields}  
{constructor}

\[FOCAL METHOD\]  
{focal\_method\_code}

\[TEST CLASS SKELETON\]  
package {package};  
import org.junit.jupiter.api.\*;  
import static org.junit.jupiter.api.Assertions.\*;  
public class {ClassName}Test {  
\`\`\`

\*\*Prompt template C2 — Few-shot k=2 (nguyên văn):\*\*  
\`\`\`  
Here are 2 examples of Java unit tests for similar methods.

\[EXAMPLE 1 — Lang-1\]  
Method: {lang1\_focal\_method}  
Test: {lang1\_test}

\[EXAMPLE 2 — Time-24\]  
Method: {time24\_focal\_method}  
Test: {time24\_test}

Now generate a JUnit 5 unit test for the method below.  
Only output the test class code.

\[FOCAL METHOD\]  
{focal\_method\_code}  
\`\`\`

\*Nguồn few-shot examples: Kang et al. — \*Large Language Models are Few-shot Testers\* (ICSE 2023\) Section III-A — "two handpicked report-test pairs (Time-24, Lang-1) throughout all projects" cho kết quả tốt nhất (251/750 bugs reproduced).\*

\*\*Lý do cấu hình:\*\* temperature=0 đảm bảo reproducibility — standard trong empirical SE (Arcuri & Briand, ICSE 2011). Design-rationale.md §Pipeline.

\#\#\# 5.4 Measurement

| Metric | Tool \+ version | Ground truth source | Ghi chú |  
|--------|---------------|---------------------|---------|  
| Line Coverage | JaCoCo 0.8.11 (Maven plugin) | Defects4J source code | instrument via \`jacoco:prepare-agent\` |  
| Branch Coverage | JaCoCo 0.8.11 | Defects4J source code | cùng report với Line |  
| Test Smell Density | tsDetect v1.0 (static analysis) | N/A — automated detection | 5 smell types: AR, ET, EaT, MNT, RA |  
| Compilability Rate | javac 21 \+ subprocess | N/A — compile success/fail | gate trước mọi RQ khác |  
| Mutation Score | PIT 1.15.0 (Maven plugin) | Defects4J source code | chỉ đo nếu kịp sau ngày 4 |

\#\#\# 5.5 Baseline

\*\*Anchor baseline:\*\* GPT-4o-mini — GPT family xuất hiện nhiều nhất trong 54 papers (9 papers); mọi paper đều compare với GPT → results comparable với literature.

\*\*Lower bound:\*\* EvoSuite 1.2.0 — traditional SBST tool, xuất hiện trong 5/54 papers; HITS'24 báo cáo EvoSuite đạt 68.0% statement coverage trên Defects4J → sanity check: LLM phải beat EvoSuite mới có practical value.

\*\*Cấu hình EvoSuite đủ để reproduce:\*\*  
\`\`\`  
evosuite \-class {focal\_class} \-projectCP {defects4j\_classpath}  
         \-Dsearch\_budget=60 \-Dcriterion=LINE:BRANCH:MUTATION  
         \-seed=42  
\`\`\`

\#\#\# 5.6 Statistical Analysis Plan

\*\*RQ1 & RQ2 (4 groups độc lập, output liên tục):\*\*  
\- Test: Kruskal-Wallis — one-tailed không áp dụng (so sánh nhiều chiều) — α \= 0.05  
\- Post-hoc: Dunn test với Bonferroni correction; α adjusted \= 0.05/6 \= 0.0083 per pair  
\- Effect size: Cliff's delta (d); thresholds: negligible \< 0.147, small 0.147–0.33, medium 0.33–0.474, large \> 0.474  
\- Lý do chọn test: non-parametric vì coverage % không đảm bảo normal với n=30; 4 nhóm độc lập  
\- N \= 30 per group; power ≥ 0.80 — theo Arcuri & Briand (ICSE 2011\) n=30 đủ cho Kruskal-Wallis

\*\*RQ3 (Smell Density, 4 groups):\*\*  
\- Test: Kruskal-Wallis — α \= 0.05  
\- Post-hoc: Dunn/Bonferroni \+ Cliff's delta  
\- Smell Density là ratio liên tục → cùng loại output như coverage

\*\*RQ4 (Few-shot vs Zero-shot, paired):\*\*  
\- Test: Wilcoxon signed-rank — one-tailed (H1: few-shot \> zero-shot) — α \= 0.05  
\- Effect size: Cliff's delta per LLM (4 tests → Bonferroni: α \= 0.05/4 \= 0.0125)  
\- Lý do Wilcoxon: cùng 30 methods → paired samples; non-normal → Wilcoxon không phải paired t-test

\*\*Tools:\*\* Python 3.11 — \`scipy.stats.kruskal\`, \`scikit\_posthocs.posthoc\_dunn\`, custom Cliff's delta

\---

\#\# 6\. Evaluation Plan

\#\#\# 6.1 Bảng tiêu chí đánh giá

| RQ | Metric | Ngưỡng | Test | H0 bị reject khi... | Kết quả âm tính có ý nghĩa? |  
|----|--------|--------|------|--------------------|-----------------------------|  
| RQ1 | Line Coverage | ≥ 60% | Kruskal-Wallis | p \< 0.05 \+ Cliff's δ ≥ small | ✅ Có — nghĩa là free LLMs tương đương nhau |  
| RQ2 | Branch Coverage | ≥ 45% | Kruskal-Wallis | p \< 0.05 \+ Cliff's δ ≥ small | ✅ Có — cùng kết luận |  
| RQ3 | Test Smell Density | So với 34% baseline | Kruskal-Wallis | p \< 0.05 | ✅ Có — LLMs tạo smell như nhau |  
| RQ4 | Line Coverage (paired) | ≥ 60% | Wilcoxon | p \< 0.0125 per LLM | ✅ Có — few-shot không giúp ích |

\#\#\# 6.2 Diễn giải tổ hợp kết quả

\*\*Double positive\*\* (H1 được chấp nhận cả RQ1 \+ RQ2): Có LLM vượt trội rõ ràng → recommend model cụ thể cho researchers không có budget. Contribution mạnh nhất.

\*\*Mixed\*\* (H1 RQ1 nhưng H0 RQ2, hoặc ngược lại): Khác biệt phụ thuộc loại coverage → recommend model khác nhau tùy mục tiêu (line vs branch). Cần discuss trade-off.

\*\*Double negative\*\* (H0 không bị bác bỏ cả RQ1 \+ RQ2): Free LLMs cho kết quả tương đương → kết luận: \*"Chọn Gemini-2.5-Flash vì free tier cao nhất và kết quả không kém GPT-4o-mini"\*. Vẫn là valid contribution — tiết kiệm effort cho cộng đồng.

\#\#\# 6.3 Sub-group analysis

Điều kiện: n\_group ≥ 10 per project (có 10 methods × 3 projects) — quyết định TRƯỚC khi có data.

Sub-group analysis theo project (Lang / Math / Chart): nếu một project cho kết quả outlier → ghi vào limitations, không loại khỏi analysis chính.

\---

\#\# 7\. Threats to Validity

\#\#\# 7.1 Internal Validity

\*\*Threat 1:\*\* Model version drift — OpenAI và Google có thể silent-update API mà không thông báo, khiến kết quả không reproducible.    
\*\*Mitigation:\*\* Pin exact version string (\`gpt-4o-mini-2024-07-18\`, \`gemini-2.5-flash\`, \`deepseek-v4-flash\`, \`meta-llama/llama-4-scout\`); log timestamp của mỗi API call; lưu tất cả raw responses vào file JSON có hash.

\*\*Threat 2:\*\* Temperature=0 không đại diện cho use case thực tế (developers thường dùng temperature \> 0).    
\*\*Mitigation:\*\* Ghi rõ trong limitations; report là controlled experiment; để temperature \> 0 cho future work.

\#\#\# 7.2 External Validity

\*\*Threat 1:\*\* Chỉ 3 Java projects (Lang, Math, Chart) từ Defects4J — không đại diện cho toàn bộ Java ecosystem.    
\*\*Mitigation:\*\* Chọn 3 projects có domain khác nhau (string utils, math, charting); acknowledge limitation; mở rộng lên 6 projects nếu pipeline ổn ngày 3\.

\*\*Threat 2:\*\* Chỉ Java — kết quả không generalize sang Python, JavaScript, Rust.    
\*\*Mitigation:\*\* Scope rõ ràng trong title và abstract; GAP-D (JS/TS) để làm future work.

\#\#\# 7.3 Construct Validity

\*\*Threat 1:\*\* Line/Branch Coverage không đo semantic correctness — test có thể đạt 100% coverage nhưng không có assertion nào catch bug.    
\*\*Mitigation:\*\* Bổ sung Mutation Score (PIT) để đo fault-detection capability; nếu không kịp → ghi là limitation.

\*\*Threat 2:\*\* tsDetect có thể miss custom smell patterns không có trong tool's ruleset.    
\*\*Mitigation:\*\* Dùng đúng 5 smell types được validate trong Ouedraogo et al. — \*On the Diffusion of Test Smells in LLM-Generated Unit Tests\* (2024, SPLC) — (AR, ET, EaT, MNT, RA); không tự thêm rules.

\#\#\# 7.4 Conclusion Validity

\*\*Threat 1:\*\* N \= 30 per group có thể không đủ statistical power cho tất cả sub-group analyses.    
\*\*Mitigation:\*\* Power analysis: Kruskal-Wallis với n=30 per group, effect size medium (δ=0.33) → power ≈ 0.82 (theo G\*Power 3.1) — đủ. Nếu chỉ detect small effect → ghi vào limitations.

\*\*Threat 2:\*\* Multiple comparisons (6 cặp trong post-hoc) tăng Type I error.    
\*\*Mitigation:\*\* Bonferroni correction: α adjusted \= 0.05/6 \= 0.0083 per pair — standard practice trong SE empirical studies.

\---

\#\# 8\. Timeline & Resources

\#\#\# Timeline 1 tuần

\> Ghi chú: Nhóm còn 3 thành viên (Lý Minh Khôi đã rời nhóm). Vai trò \*\*LR (LLM Runner / thực nghiệm)\*\* do \*\*Lê Thị Bảo Ngọc\*\* kiêm nhiệm cùng vai trò PL.

| Ngày | PL \+ LR (Ngọc) | DG (Phúc) | MS (Nhân) | RW |  
|------|----------------|-----------|-----------|-----|  
| \*\*1\*\* | Kickoff, assign tasks, verify Defects4J accessible; setup API 4 LLMs (Llama-4-Scout via OpenRouter, Gemini/DeepSeek/GPT keys) | Clone Defects4J; checkout Lang/Math/Chart; extract 30 focal methods | Setup Python env (scipy, scikit\_posthocs, pandas) | Outline §1, §2, §3 |  
| \*\*2\*\* | Review pipeline design; viết unified API caller (4 LLMs, retry logic, rate limit handler) | Build class context extractor (imports \+ fields \+ constructor) | Viết JaCoCo \+ tsDetect result parser | Viết §3 Related Work |  
| \*\*3\*\* | Monitor pipeline; run API calls: 30 methods × 4 LLMs × 2 conditions \= 240 calls; log chi phí \+ raw responses | Run compile check trên 240 generated tests | Chạy JaCoCo coverage measurement; chạy tsDetect | Draft §4 RQ |  
| \*\*4\*\* | Review intermediate results; run PIT mutation testing nếu kịp | Verify compile rates; fix classpath issues nếu có | Collect data; run Kruskal-Wallis \+ Dunn \+ Cliff's delta | Draft §5 Protocol |  
| \*\*5\*\* | Review statistical results; fix any remaining pipeline issues | Verify data quality; cross-check with results | Vẽ boxplots; diễn giải results; viết §6 Evaluation | Draft §7 Threats |  
| \*\*6\*\* | Review full draft | Hỗ trợ RW format §3 | Viết §6 chi tiết \+ §8 | Tích hợp tất cả sections |  
| \*\*7\*\* | Final review; submit | — | — | Format \+ proofread final |

\#\#\# Resources & Chi phí

| Resource | Chi phí | Ghi chú |  
|----------|---------|---------|  
| Gemini-2.5-Flash API | \*\*$0\*\* | Free tier (Google AI Studio) — đủ cho 240 calls |  
| DeepSeek-V4-Flash API | \*\*$0\*\* | Free tier tại platform.deepseek.com (5M free tokens) |  
| Llama-4-Scout (OpenRouter) | \*\*$0\*\* | Free tier qua OpenRouter |  
| GPT-4o-mini API | \*\*\~$0.01\*\* | Free tier / low cost; hoặc dùng DeepSeek làm backup |  
| Defects4J v2.0 | \*\*$0\*\* | Public GitHub |  
| JaCoCo 0.8.11 | \*\*$0\*\* | Apache License 2.0 |  
| PIT 1.15.0 | \*\*$0\*\* | Apache License 2.0 |  
| tsDetect v1.0 | \*\*$0\*\* | GitHub open-source |  
| \*\*Tổng\*\* | \*\*≈ $0\*\* | |

\#\#\# Contingency Plan

| Risk | Xác suất | Mitigation hành động |  
|------|----------|---------------------|  
| Defects4J build fail | 30% | Dùng Docker image \`rjust/defects4j\`; DG chịu trách nhiệm ngày 1 |  
| Gemini rate limit | 20% | Stagger calls; DeepSeek làm backup full |  
| Llama-4-Scout rate limit (OpenRouter) | 40% | Dùng provider backup trên OpenRouter; hoặc Groq API free tier |  
| PIT timeout | 35% | Giảm xuống 3 mutators; chạy parallel nhiều máy |  
| Compilability \< 10% | 25% | Thêm 1-shot repair step (ChatTester'24 approach) |

\#\#\# Phân công Roles

| Thành viên | Role | Deliverable tuần này |  
|------------|------|---------------------|  
| \[Lê Thị Bảo Ngọc\] | PL \+ LR \+ RW | Điều phối tiến độ; review; submit GV; xử lý blockers; \*\*phụ trách toàn bộ thực nghiệm\*\*: setup API 4 LLMs, viết unified API caller, batch-process 240 calls, log chi phí \+ raw responses; coordinate §1 §5 §7 §8 |  
| \[Đặng Trần Phúc\] | DG \+ RW | Clone Defects4J; extract 30 focal methods; viết §3 Related Work; hỗ trợ format document cuối |  
| \[Phùng Thanh Nhân\] | MS \+ RW | Implement JaCoCo \+ tsDetect \+ PIT; chạy stats; vẽ boxplots; viết §4 §6; diễn giải kết quả; làm slide |

