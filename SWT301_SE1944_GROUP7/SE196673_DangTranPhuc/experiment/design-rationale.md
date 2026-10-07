# Experiment Design Rationale – LLM for Unit Test Case Generation
Ngày: 2026-06-08 | GAP source: SLR/gap-analysis.md

---

## Bảng Quyết Định

| Quyết định | Giá trị | Nguồn gốc |
|-----------|---------|-----------|
| LLM/Tool | GPT-4o (OpenAI, temperature=0) | GAP-T: cột Tool/LLM — GPT-4 là LLM phổ biến nhất trong evidence table |
| Dataset | Java/Python functions từ GitHub public repos, CC 5–15 đo bằng Lizard, N ≥ 50 hàm | GAP-D: chưa có dataset kiểm soát CC 5–15 |
| Metric chính | Branch coverage (JaCoCo cho Java, Coverage.py cho Python) + Mutation score (PIT cho Java, pytest-mutagen cho Python) | GAP-M: cột Metric — branch coverage và mutation score là hai metric phổ biến nhất |
| Metric phụ | Cyclomatic Complexity (Lizard) | GAP-T: cần đo CC để phân tích RQ3 |
| Baseline type | Comparative: GPT-4 vs Student-written vs Randoop | Claim type của RQ — so sánh 3 hệ thống độc lập |
| Threshold RQ1 | Branch coverage ≥ 80% | Case 1 — Huang 2025 đạt >80% coverage trên real-world functions; floor=80% |
| Threshold RQ2 | Mutation score ≥ 60% | Case 2 — Dakhel 2023: floor≈55–60%, threshold=60% |
| Pipeline base | HITS (Wang 2024) + Code-Aware Prompting (Ryan 2024) | Paper có evaluation paradigm gần nhất với RQ — đo coverage + so sánh tool |

---

## Lý giải threshold (ghi 1 đoạn cho mỗi threshold)

**Threshold RQ1 — Branch coverage ≥ 80%:**
Case 1 — Huang 2025 (Benchmarking LLMs) đề xuất ngưỡng 80% là mức đạt yêu cầu cho unit test chất lượng cao trên real-world Python functions. Lý luận: ngưỡng này đủ cao để đảm bảo test có ý nghĩa nhưng không quá khắt khe cho hàm CC 5–15.

**Threshold RQ2 — Mutation score ≥ 60%:**
Case 2 — Dakhel 2023 (Effective Test Generation) báo cáo mutation score của LLM-generated tests đạt 55–65% trên Java; floor=55%, threshold=60% (làm tròn). Lý luận: 60% là mức tối thiểu để test được xem là có khả năng phát hiện lỗi đáng tin cậy.

---

## Pipeline chi tiết

| Thành phần | Ghi rõ | Nguồn |
|-----------|--------|-------|
| LLM/Tool | GPT-4o, temperature=0, zero-shot prompting | GAP-T |
| Prompt strategy | Zero-shot: "Generate unit tests for the following Java/Python function" | Ryan 2024 |
| Temperature | 0 (reproducibility) | Standard practice |
| Metric tool (coverage) | JaCoCo 0.8.x (Java), Coverage.py 7.x (Python) | GAP-M |
| Metric tool (mutation) | PIT 1.x (Java), pytest-mutagen 1.x (Python) | GAP-M |
| CC measurement | Lizard (latest) | GAP-T |
| Baseline type | Comparative — GPT-4o vs Student vs Randoop | Claim type RQ |
