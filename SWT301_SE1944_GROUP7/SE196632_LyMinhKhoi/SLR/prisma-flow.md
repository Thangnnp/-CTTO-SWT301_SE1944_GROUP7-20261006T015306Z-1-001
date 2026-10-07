# PRISMA Flow Diagram - Quy trình sàng lọc tài liệu cá nhân (CORE)

```text
[Records từ database searching (Tổng kết quả cá nhân trên CORE) | N = 22]
       │
       ├─► [Số bị loại do trùng lặp giữa String A & B / Duplicate (N = 3)]
       │
       ▼
[Số lượng bản ghi sau khi lọc trùng / Sau dedup (N = 19)]
       │
       ├─► [Sàng lọc Vòng 1 (Title & Abstract Screening) | Loại bỏ N = 14]
       │   ├── Lý do EC-O (Không đo lường branch coverage/mutation score): Loại 6
       │   ├── Lý do EC-P (Không thuộc phạm vi ngôn ngữ Java/Python): Loại 5
       │   └── Lý do EC-N (Thiếu dữ liệu thực nghiệm thực tế): Loại 3
       │
       ▼
[Số lượng bản ghi đưa vào đọc Full-text / Vòng 2 (N = 5)]
       │
       ├─► [Sàng lọc Vòng 2 (Full-text Review) | Loại bỏ N = 0]
       │
       ▼
[Số lượng bài báo chốt đưa vào trích xuất dữ liệu (N = 5)]
       └── Đạt chuẩn 100% tiêu chí, đưa vào Evidence Table (5 papers)