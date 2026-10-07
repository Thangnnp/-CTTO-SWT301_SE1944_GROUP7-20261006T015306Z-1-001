# **GAP Analysis — LLM-Based Unit Test Case Generation (REVISED)**

Evidence table: N \= 54 papers | Ngày: 2026-06-09  
 **Constraint: 1 tuần / 3 người / $0 chi phí**

---

## **Bảng GAP**

| Cột | Phát hiện từ 54 papers | Loại GAP | Phản chứng |
| ----- | ----- | ----- | ----- |
| Tool/LLM | GPT-3.5/ChatGPT: 9 papers; EvoSuite: 5; Copilot: 4; Gemini: 3; DeepSeek: 2; Claude: 2; LLaMA: 1\. Không có paper nào so sánh hệ thống ≥3 FREE/open-source LLMs trên cùng benchmark với cùng điều kiện. | **GAP-T** | ✅ Multi-LLM Chaining (2025, IEEE Access) dùng GPT-4o+Gemini+Claude-3.5 nhưng là **pipeline chaining** (model A cải thiện output của model B), không phải **independent comparison**. Cabral 2025 so DeepSeek vs ChatGPT nhưng chỉ 2 models, không có Gemini/Llama. → **GAP-T XÁC NHẬN** sau khi scope thành free models. |
| Metric | Test Smell: **chỉ 1 paper** (Ouedraogo 2024 — GPT-3.5/GPT-4 only). Mutation Score: 27 papers; Line Coverage: 20 papers; Branch Coverage: 19 papers. Không có paper nào so sánh **smell density giữa các LLM khác nhau**. | **GAP-M** | ✅ Ouedraogo 2024 là paper duy nhất đo smell — chỉ so GPT-3.5 vs GPT-4. Gemini, DeepSeek, Llama chưa được đo smell density. → **GAP-M XÁC NHẬN** với scope: smell comparison across LLMs. |
| Dataset | 41/54 papers dùng Java; Python: 5; JavaScript: 1; Rust: 1; Golang: 1\. | GAP-D | ⚠️ ASTER (2024) đã cover Java+Python. Contribution ít rõ ràng. **Không chọn làm primary trong 1 tuần.** |
| Hạn chế | "Small dataset / limited benchmark": 30/54 papers (55.6% \> ngưỡng 40%). | **GAP-S** | ✅ 30 papers nêu giới hạn dataset nhỏ/benchmark đơn lẻ → **GAP-S XÁC NHẬN**: đây là justification để dùng subset nhỏ hơn mà vẫn có giá trị. |

---

## **GAP Chính: GAP-T (Revised cho 1 tuần / $0)**

**Phát biểu:**

*"Trong 54 nghiên cứu được khảo sát, không có nghiên cứu nào so sánh hệ thống các LLM miễn phí/mã nguồn mở (Gemini-1.5-Flash, DeepSeek-V2-Chat, Llama-3.1-8B) cùng với GPT-4o-mini trên benchmark Java chuẩn (Defects4J) dưới cùng điều kiện thực nghiệm — cùng prompt template, cùng metric đo lường — để cung cấp baseline chi phí bằng 0 cho cộng đồng nghiên cứu."*

**Tại sao "free LLMs" là contribution mới:**

* Multi-LLM Chaining (2025): dùng GPT-4o+Gemini+Claude nhưng **chaining pipeline**, không independent comparison  
* Cabral 2025: chỉ so DeepSeek vs ChatGPT — **2 models**, thiếu Gemini và Llama  
* Konstantinou 2026: so sánh LLM versions nhưng **không công bố model names** cụ thể, focus vào augmented techniques  
* **Không paper nào** so sánh free-tier accessible models (Gemini free, DeepSeek free, Llama local) — practical value cho researchers không có budget

---

## **GAP Secondary: GAP-M (Test Smell Comparison)**

**Phát biểu:**

*"Ouedraogo et al. (2024) là nghiên cứu duy nhất đo test smell density của LLM-generated tests, nhưng chỉ so sánh GPT-3.5 và GPT-4. Chưa có nghiên cứu nào so sánh smell density giữa Gemini, DeepSeek và Llama — điều này có thể làm secondary metric trong cùng experiment của GAP-T."*

---

## **Chi tiết Kiểm tra Phản chứng — GAP-T**

| Paper | Năm | Có so sánh free LLMs không? | Ghi chú |
| ----- | ----- | ----- | ----- |
| Multi-LLM Chaining (IEEE Access) | 2025 | ❌ Không | Chaining pipeline, không independent; enterprise Java, trả tiền |
| Cabral — Mutation Testing | 2025 | ❌ Không | Chỉ 2 models (DeepSeek vs ChatGPT), không có Gemini/Llama |
| TestWars | 2025 | ❌ Không | So LLM vs SBST, không phải LLM vs LLM |
| Konstantinou | 2026 | ❌ Không | So techniques, không phải models; model names không công bố |
| Haroon | 2026 | ❌ Không | Focus software evolution, không model comparison |
| Walczak | 2025 | ❌ Không | GPT+Claude+Gemini nhưng focus vào docstring context, không systematic comparison |
| Tất cả 48 papers còn lại | — | ❌ Không | Mỗi paper chỉ dùng 1 model |

**→ Kết luận: XÁC NHẬN — Không paper nào so sánh hệ thống free-accessible LLMs trên Defects4J.**

---

## **Feasibility Check — Constraint: 1 tuần / 3 người / $0**

| Tiêu chí | Mức | Ghi chú |
| ----- | ----- | ----- |
| Dataset | ✅ | Defects4J v2.0 — public GitHub, clone miễn phí, dùng trong 4+ papers |
| Tool/API | ✅ | Gemini-1.5-Flash: **free tier 1,500 req/day**; DeepSeek-V2-Chat: **free tier** (deepseek.com); Llama-3.1-8B: **Ollama local, hoàn toàn free**; GPT-4o-mini: free tier (limited) |
| Compute | ✅ | CPU laptop đủ — javac \+ JaCoCo \+ PIT chạy local. Llama via Ollama cần 8GB RAM |
| Ground truth | ✅ | Defects4J có ground truth sẵn, không annotation |
| Skills | ✅ | Maven \+ JaCoCo \+ PIT: có tutorial đầy đủ; API calls: standard HTTP; tsDetect: GitHub README đủ |
| Thời gian | ⚠️ | Feasible với downscope: 3 projects × 10 methods \= 30 focal methods × 4 LLMs × 2 conditions \= 240 calls. Gemini free tier: \~10 phút. PIT trên 120 compilable tests: \~3h. Tổng: 3-4 ngày thực nghiệm |
| Contribution | ✅ | Free-model comparison chưa có trong 54 papers; practical value cao cho researchers |
| Chi phí | ✅ | **$0 tuyệt đối**: Gemini free, DeepSeek free, Llama local, JaCoCo/PIT Apache License |

**Kết quả: 0 ❌ / 1 ⚠️ → AN TOÀN**

*Mitigation ⚠️ Thời gian:* Downscope từ 100 xuống **30 focal methods** (3 projects × 10 methods: Lang-3, Math-5, Chart-2). Nếu pipeline chạy ổn ngày 3 → mở rộng lên 60 methods.

---

## **Downscope so với Design Rationale gốc**

| Yếu tố | Phiên bản gốc | Phiên bản revised (1 tuần/$0) | Lý do |
| ----- | ----- | ----- | ----- |
| LLM 1 | GPT-4o (trả tiền) | **GPT-4o-mini** (free tier) | Cost constraint |
| LLM 2 | Claude-3.5-Sonnet (trả tiền) | **Gemini-1.5-Flash** (free 1500 req/day) | Cost constraint |
| LLM 3 | Gemini-1.5-Pro (rate limited) | **DeepSeek-V2-Chat** (free tier) | Cost \+ availability |
| LLM 4 | DeepSeek-V2 | **Llama-3.1-8B (Ollama local)** | Đại diện open-source |
| Dataset | 100 focal methods | **30 focal methods** (3 projects × 10\) | Time constraint |
| Metric chính | Line Coverage \+ Branch \+ Mutation | **Line Coverage \+ Branch Coverage** (giữ PIT nếu có thời gian) | Time constraint |
| Statistical test | Kruskal-Wallis \+ Dunn \+ Cliff's δ | **Kruskal-Wallis \+ Dunn \+ Cliff's δ** (giữ nguyên — code có sẵn) | Không thay đổi |

