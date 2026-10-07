# GAP Analysis – LLM for Unit Test Case Generation
Evidence table: N = 22 papers | Ngày: 2026-06-08

---

## Bảng GAP

| Cột | Phát hiện | Loại GAP | Phân chứng |
|-----|-----------|----------|------------|
| Tool/LLM | Chưa có paper nào kiểm soát CC 5–15 khi dùng GPT-4 sinh unit test và đo bằng Lizard | GAP-T | ✅ Kiểm tra 22 paper |
| Dataset | Chưa có dataset Java/Python ≥ 50 hàm với CC 5–15 được kiểm soát cụ thể | GAP-D | ✅ |
| Metric | Chưa có paper nào so sánh đồng thời GPT-4 vs Randoop vs student-written trên cùng dataset | GAP-M | ✅ |
| Hạn chế | Đa số paper chỉ test 1 ngôn ngữ (Java hoặc Python), không cả hai | GAP-S | ✅ |

---

## GAP Chính: GAP-T
Chưa có nghiên cứu nào đánh giá GPT-4 sinh unit test trên tập hàm Java/Python có cyclomatic complexity trung bình (CC 5–15, đo bằng Lizard) với ngưỡng branch coverage ≥ 80% và mutation score ≥ 60%.

## GAP Secondary: GAP-M
Chưa có paper nào so sánh đồng thời ba baseline: GPT-4, Randoop và student-written tests trên cùng tập hàm Java/Python ở CC 5–15.

---

## Chi tiết kiểm tra phân chứng
[Bảng kiểm tra từng paper cho GAP primary — GAP-T]

| Paper | Đã làm không? | Ghi chú |
|-------|--------------|---------|
| Benchmarking LLMs (Huang 2025) | Không / Có | Có đề cập cyclomatic complexity nhưng không kiểm soát dải CC 5–15 cụ thể, không dùng Lizard |
| LLMs as Test Generators (Silva 2025) | Không / Có | Đo CC và mutation score nhưng không giới hạn CC 5–15, không dùng Lizard |
| ChatGPT vs SBST (Tang 2023) | Không | Không phân tích theo CC |
| HITS (Wang 2024) | Không | Không đo CC |
| Code-Aware Prompting (Ryan 2024) | Không | Không đo CC |
| Test Intention Guided (Nan 2025) | Không | Không đo CC |
| STRUT (Liu 2025) | Không | Không đo CC, C language |
| Navigating Labyrinth (Liao 2025) | Không | Không đo CC |
| LSPAI (Go 2025) | Không | Không đo CC |
| LSPRAG (Go 2025) | Không | Không đo CC |
| GEM (Celik 2026) | Không | Không đo CC |
| Mutation-Guided at Meta (Harman 2025) | Không | Không đo CC |
| Effective Test Gen (Dakhel 2023) | Không | Không đo CC |
| Fastjson2 Bug Detection (Zhong 2024) | Không | Không đo CC |
| Survey LLM Unit Test (Chu 2025) | Không | Survey, không có experiment |
| Mutation Testing Iterative (Straubinger 2025) | Không | Không đo CC |
| Mutation Tools Python (Guerino 2024) | Không | Không LLM |
| Fine-Tuning LLMs (Shang 2024) | Không | Không đo CC |
| Boosting LLMs Mutation (Wang 2026) | Không | Không đo CC |
| Test Oracles (Konstantinou 2024) | Không | Không đo CC |
| MultiFileTest (Wang 2025) | Không | Không đo CC |
| Examination of Code (Beer 2024) | Không | Không đo CC cụ thể |

→ Kết luận: **XÁC NHẬN** GAP-T — không có paper nào đã làm điều này.

---

## Feasibility Check – GAP Chính (GAP-T)

| Tiêu chí | Mức | Ghi chú |
|----------|-----|---------|
| Dataset | ✅ | GitHub public repos có sẵn, có thể lọc hàm theo CC bằng Lizard < 1 tuần |
| Tool/API | ✅ | GPT-4o API free tier đủ cho N sample, đã test API; Randoop open-source |
| Compute | ✅ | CPU đủ hoặc Colab T4 free — JaCoCo + Coverage.py + PIT chạy được |
| Ground truth | ✅ | Không cần, coverage và mutation score đo tự động |
| Skills | ✅ | Java/Python testing, có thư viện sẵn, đã có tutorial |
| Thời gian | ⚠️ | Xong nhưng tight — cần ≥ 50 hàm, đo 3 nhóm test |
| Contribution | ✅ | Là baseline đầu tiên cho GPT-4 + CC 5–15 |

**Kết quả:** ✅ ✅ ✅ ✅ ✅ ⚠️ ✅ → An toàn — tiếp tục với GAP này

---

## Phát biểu GAP cuối cùng
Các nghiên cứu hiện tại chưa đánh giá GPT-4 sinh unit test trên tập hàm Java/Python có cyclomatic complexity trung bình (CC 5–15, đo bằng Lizard), và chưa so sánh đồng thời với Randoop và student-written tests trên cùng dataset. Đây là khoảng trống mà nghiên cứu này nhằm lấp đầy.
