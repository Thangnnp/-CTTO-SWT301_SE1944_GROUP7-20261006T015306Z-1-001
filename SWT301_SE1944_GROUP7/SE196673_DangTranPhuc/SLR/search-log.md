# Search Log – LLM for Unit Test Case Generation
**Thành viên:** Đặng Trần Phúc
**MSSV:** SE196673
**Ngày thực hiện:** 2026-06-04

---

## Chuỗi tìm kiếm (Query Strings)

### String A
**Query nguyên văn:**
GPT-4 unit test generation branch coverage Java Python

- Database: Semantic Scholar
- Bộ lọc: Has PDF, Year: 2020–2026, Field: Computer Science
- Ngày search: 2026-06-04
- Số kết quả: 39 papers

---

### String B
**Query nguyên văn:**
LLM automated unit test mutation score Randoop comparison Java Python

- Database: Semantic Scholar
- Bộ lọc: Has PDF, Year: 2020–2026, Field: Computer Science
- Ngày search: 2026-06-04
- Số kết quả: 3 papers

---

### String C
**Query nguyên văn:**
LLM unit test generation mutation testing fault detection comparison

- Database: Semantic Scholar
- Bộ lọc: Has PDF, Year: 2020–2026, Field: Computer Science
- Ngày search: 2026-06-04
- Số kết quả: 10 papers

---

### String D
**Query nguyên văn:**
cyclomatic complexity unit test generation large language model quality

- Database: Semantic Scholar
- Bộ lọc: Has PDF, Year: 2020–2026, Field: Computer Science
- Ngày search: 2026-06-04
- Số kết quả: 30 papers

---

## Tổng hợp trước dedup

| Database | String | Kết quả |
|----------|--------|---------|
| Semantic Scholar | String A | 39 |
| Semantic Scholar | String B | 3 |
| Semantic Scholar | String C | 10 |
| Semantic Scholar | String D | 30 |
| Snowballing (CrossRef) | Phần S | 0 |
| **Tổng trước dedup** | | **82** |
| **Sau dedup** | | **65** |
| Số bị loại (trùng lặp) | | **17** |

---

## Phần S – Cross-reference Search (Snowballing)

> Snowballing không có query string – không điền vào mục này như các String A/B/C/D.

**Phương pháp:** Backward snowballing – đọc reference list của các paper đã pass V2 screening
**Thực hiện:** Sau khi có `03_final_included.csv`, đọc reference list của từng paper included → nếu thấy paper mới có vẻ liên quan → lookup trên Semantic Scholar → thêm vào `01_all_records.csv` với `search_strings = "Snowball"`
**Công cụ:** Semantic Scholar để lookup metadata từ DOI
**Ngày thực hiện:** 2026-06-04
**Paper included đã scan:** 22 paper
**Paper mới phát hiện:** 0 paper mới pass IC

---

## Ghi chú

- Thực hiện dedup bằng: Excel
- Paper trùng với Bảo Ngọc (SE190619) bị loại do EC-D: ~12 paper
- Không có file nào "all same row count" mà không có lý do


## Danh sách paper paywalled (không có PDF tự do)

| Title | Authors | Year | DOI | URL |
|-------|---------|------|-----|-----|
| Test Intention Guided LLM-Based Unit Test Generation | Nan, Zifan et al. | 2025 | 10.1109/ICSE655347.2025.00243 | https://ieeexplore.ieee.org/document/11029845 |