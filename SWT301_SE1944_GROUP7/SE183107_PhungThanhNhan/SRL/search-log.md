# Search Log – LLM for Automated Acceptance Test Case & Unit Test Case Generation
**Thành viên:** Phùng Thanh Nhân
**Ngày thực hiện:** 2026-06-02

---\n\n## Chuỗi tìm kiếm (Query Strings)

### String A – Topic 1: Acceptance Test Case Generation
**Query nguyên văn:**
```text
"user story" AND ("acceptance test" OR "test case") AND ("LLM" OR "GPT")
- Database: arXiv + Google Scholar
- Bộ lọc: cs.SE, Year 2020-2026
- Ngày search: 2026-06-02 10:00
- Số kết quả: 9 papers (arXiv) + thêm Google Scholar

---

### String B – Topic 2: Unit Test Case Generation
**Query nguyên văn:**
```
("unit test generation") AND ("LLM" OR "GPT-4") AND ("branch coverage" OR "mutation score")
```
- Database: arXiv + Google Scholar
- Bộ lọc: cs.SE, Year 2020-2026
- Ngày search: 2026-06-02 11:00
- Số kết quả: 10 papers (arXiv) + thêm Google Scholar

---

## Tổng hợp trước dedup

| Database | String | Kết quả |
|----------|--------|---------|
| arXiv | String A – Topic 1 | 9 |
| arXiv | String B – Topic 2 | 10 |
| Google Scholar | String A – Topic 1 | 8 |
| Google Scholar | String B – Topic 2 | 8 |
| **Tổng trước dedup** | | **35** |
| **Sau dedup** | | **30** |
| Số bị loại (trùng lặp) | | 5 |

---

## Phần S – Cross-reference Search (Snowballing)

> Snowballing không có query string – không điền vào mục này như các String A/B.

**Phương pháp:** Backward snowballing – đọc reference list của các paper đã pass V2 screening
**Thực hiện:** Đọc reference list từng paper included → nếu thấy paper liên quan → lookup trên arXiv/Semantic Scholar
**Công cụ:** arXiv, Semantic Scholar
**Ngày thực hiện:** 2026-06-02
**Paper included đã scan:** 20 paper
**Paper mới phát hiện:** 0

---

## Ghi chú
- Thực hiện dedup bằng: Excel
- Paper trùng nhau nhiều nhất: paper xuất hiện ở cả arXiv và Google Scholar
- Snowballing: 0 paper mới vì 20 paper đã đủ tiêu chí
