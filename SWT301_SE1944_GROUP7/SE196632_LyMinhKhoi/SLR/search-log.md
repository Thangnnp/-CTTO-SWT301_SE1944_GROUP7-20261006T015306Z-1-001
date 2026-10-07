# Search Log - LLM for Unit Test Case Generation
**Thanh vien:** Lý Minh Khôi
**Ngay thuc hien:** 2026-06-02
---

## ## Chuoi tim kiem (Query Strings)

### String A (Giai phap & doi chung)
**Query nguyen van:**
GPT-4 unit test generation branch coverage Java Python

- Database: CORE (core.ac.uk)
- Bo loc: Has PDF, Year: 2020-2026, Field: Computer Science
- Ngay search: 2026-06-02
- So ket qua: 16 papers
---

### String B (Diem dot bien & so sanh)
**Query nguyen van:**
LLM automated unit test mutation score Randoop comparison Java Python

- Database: CORE (core.ac.uk)
- Bo loc: Has PDF, Year: 2020-2026, Field: Computer Science
- Ngay search: 2026-06-02
- So ket qua: 6 papers
---

## ## Tong hop truoc dedup

| Database | String | Ket qua |
| :--- | :--- | :---: |
| CORE | String A | 16 |
| CORE | String B | 6 |
| **Tong truoc dedup** | | **2** |
| **Sau dedup** | | **19** |
| **So bi loai (trung lap)** | | **3** |

---

## ## Phan S - Cross-reference Search (Snowballing)
> Snowballing khong co query string - khong dien vao muc nay nhu cac String A/B/C.

**Phuong phap:** Backward snowballing - doc reference list cua cac paper da pass V2 screening
**Thuc hien:** Sau khi co 03_final_included.csv, doc reference list cua tung paper included -> neu thay paper moi co ve lien quan -> lookup tren CORE -> them vao 01_all_records.csv voi nguon la 'Snowballing'
**Cong cu:** CORE de lookup metadata tu DOI va check forward citations
**Ngay thuc hien:** 2026-06-04
**Paper included da scan:** 1 paper (tu du lieu goc cua ca nhan)
**Paper moi phat hien:** 0 paper (khong phat hien them paper moi qua snowballing do cac paper trong reference list da duoc bao gom trong cac String A-B)
---

## ## Ghi chu
- Thuc hien dedup bang: Excel
- Paper trung nhau nhieu nhat: Co 3 bai bi trung lap tu khoa giua chuoi String A va String B khi quet tren cung he thong CORE
- Trung lap he thong: Loai bo 3 loai bao trung lap giua cac string tim kiem cua ca nhan
- Snowballing: Khong phat hien them paper


