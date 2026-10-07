# Gap Final — GAP chính & phụ được chốt (Nhóm 7)

**Nhóm:** Group 7 — SWT301_SE1944 
**Ngày chốt:** 2026-06-20
**Version:** 1.1 — Chốt sau khi thống nhất nhóm. Không thay đổi sau khi GV duyệt.
**Nguồn:** gap-list.md + gap-analysis.md + evidence-table-merged.md (N = 54 papers)
---

## 1. GAP chính (Primary) — GAP-T

**Phát biểu:** Hiện chưa có nghiên cứu so sánh **≥3 LLM free/open-source** cho bài toán sinh unit test tự động trên **cùng benchmark (Defects4J v2.0)** với **cùng điều kiện** (cùng prompt, cùng temperature, cùng dataset split).

**Vì sao là khoảng trống thật:**
- Multi-LLM Chaining (2025, IEEE Access) dùng GPT-4o + Gemini + Claude nhưng theo hướng *pipeline chaining* (model A cải thiện output model B), **không phải so sánh độc lập**.
- Cabral 2025 (SBQS) so DeepSeek vs ChatGPT — chỉ 2 model, thiếu Gemini/Llama.
- Phần lớn 54 papers tập trung vào model thương mại đắt tiền (GPT-4, Claude), tạo rào cản chi phí cho cộng đồng học thuật.

**Ý nghĩa:** Giúp researcher/sinh viên ngân sách hạn chế chọn được LLM free phù hợp cho sinh unit test.

---

## 2. GAP phụ (Secondary) — GAP-M

**Phát biểu:** Test Smell Density mới chỉ được đo trên họ GPT-3.5/GPT-4 (Ouedraogo 2024). Gemini, DeepSeek, Llama **chưa được đo** smell density khi sinh unit test.

**Bằng chứng:** Chỉ 1/54 papers đo smell density; các paper còn lại tập trung Coverage/Mutation.

**Ý nghĩa:** Bổ sung chiều đánh giá chất lượng test (không chỉ coverage) cho nhiều LLM khác nhau.

---

## 3. GAP bối cảnh (không chọn làm mục tiêu)

- **GAP-D (Dataset):** Dữ liệu cô lập trong benchmark học thuật; ASTER 2024 đã cover Java+Python nên đóng góp ít rõ ràng → không chọn làm primary trong 1 tuần.
- **GAP-S (Scope):** 30/54 papers (55.6%) nêu giới hạn dataset nhỏ → dùng làm **justification** hợp lệ cho việc chọn subset 30 focal methods.

---

## 4. Ràng buộc & phạm vi chốt

- **Ràng buộc:** 1 tuần / 3 người / $0 chi phí.
- **Dataset:** Defects4J v2.0 — 30 focal methods (Lang×10, Math×10, Chart×10).
- **LLMs (lineup đã chốt — amended):**

  | LLM | Model string | Nguồn |
  |-----|--------------|-------|
  | Llama-4-Scout | `meta-llama/llama-4-scout` | OpenRouter (free) |
  | Gemini-2.5-Flash | `gemini-2.5-flash` | Google AI Studio (free) |
  | DeepSeek-V4-Flash | `deepseek-v4-flash` | DeepSeek API (5M free tokens) |
  | GPT-4o-mini | `gpt-4o-mini` | OpenAI (requires billing) |

> Ánh xạ GAP → RQ: GAP-T → RQ1–RQ3 (so sánh coverage/smell/compilability giữa các LLM); GAP-M → RQ về smell density. Chi tiết: `rq-final.md`.
