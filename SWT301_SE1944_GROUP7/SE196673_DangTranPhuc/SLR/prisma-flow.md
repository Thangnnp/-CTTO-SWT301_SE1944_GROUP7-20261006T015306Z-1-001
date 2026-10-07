# PRISMA Flow – LLM for Unit Test Case Generation
**Thành viên:** Đặng Trần Phúc
**MSSV:** SE196673

---

[Records từ database searching (N = 82)] ← Tổng từ search-log.md
↓
[Sau khi bổ sung Snowballing (N = 82)] ← Không có paper mới từ snowballing
↓
[Screened title + abstract (N = 82)]
└── Excluded (N = 60): EC-D=12 (trùng Bảo Ngọc hoặc trùng string khác), EC-O=38 (không phải unit test gen), EC-N=10 (không có thực nghiệm)
↓
[Full-text assessed (N = 22)]
└── Excluded (N = 0): Tất cả 22 paper pass V2 sau khi đọc full-text
↓
[Final included (N = 22)] ← Bằng Include trong 03_final_included.csv

---

Kiểm tra nhất quán (tự check trước khi nộp):
- Rows trong 01 CSV = 82 sau dedup ✓
- Count(v1_decision = EXCLUDE) trong 02 = 60 = Excluded vòng 1 ✓
- Count(v1 = INCLUDE + Unsure) = 22 = Full-text assessed ✓
- Count(v2_decision = Include) trong 03 = 22 = Final included ✓
