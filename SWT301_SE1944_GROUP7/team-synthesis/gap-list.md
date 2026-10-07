# Gap List — LLM-Based Automated Unit Test Generation (Nhóm 7)

**Nhóm:** Group 7 — SWT301_SE1944 
**Nguồn tổng hợp:** evidence-table-merged.md (N = 54 papers)
**Ngày:** 2026-06-20

---

## Bảng tổng hợp GAP

| Mã | Loại | Phát biểu GAP | Bằng chứng chính (từ 54 papers) | Mức độ | Thành viên phụ trách |
|-----|------|---------------|----------------------------------|--------|----------------------|
| **GAP-T** | Technology | Chưa có nghiên cứu so sánh ≥3 LLM **free/open-source** trên cùng benchmark với cùng điều kiện; đa số chỉ dùng 1 model đơn lẻ hoặc so 2 model. | Multi-LLM Chaining (2025) dùng GPT-4o+Gemini+Claude nhưng là *pipeline chaining*, không phải so sánh độc lập. Cabral 2025 so DeepSeek vs ChatGPT nhưng chỉ 2 model. | **Chính (Primary)** | Lê Thị Bảo Ngọc (SE190619) |
| **GAP-M** | Metric | Test Smell Density mới chỉ đo trên họ GPT-3.5/GPT-4 (Ouedraogo 2024); Gemini, DeepSeek, Llama chưa được đo. | Chỉ 1/54 paper đo smell density; Mutation 27 papers, Line Coverage 20 papers, Branch 19 papers. | **Phụ (Secondary)** | Lê Thị Bảo Ngọc (SE190619) |
| **GAP-D** | Dataset | Dữ liệu thử nghiệm cô lập trong benchmark học thuật (Defects4J, QuixBugs); ít đánh giá trên hệ thống doanh nghiệp. | 41/54 papers dùng Java; ASTER 2024 đã cover Java+Python nên đóng góp ít rõ ràng. | Không chọn làm primary (1 tuần) | — |
| **GAP-S** | Scope/Justification | 30/54 papers (55.6%) nêu giới hạn "small dataset / limited benchmark" → là justification hợp lệ để dùng subset nhỏ mà vẫn có giá trị. | 30/54 papers nêu giới hạn dataset nhỏ. | Bổ trợ | — |

---

## Quyết định của nhóm

- **GAP chính:** GAP-T (so sánh các LLM free cho sinh unit test trên Java/Defects4J).
- **GAP phụ:** GAP-M (đo Test Smell Density mở rộng cho nhiều LLM).
- GAP-D và GAP-S dùng làm bối cảnh / justification, không chọn làm mục tiêu chính vì ràng buộc thời gian (1 tuần / 3 người / $0 chi phí).

> Chi tiết chốt GAP + RQ tương ứng: xem `gap-final.md` và `rq-final.md`.
