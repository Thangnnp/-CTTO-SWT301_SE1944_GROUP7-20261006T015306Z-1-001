# PRISMA Flow – LLM for Automated Acceptance Test Case & Unit Test Case Generation
**Thành viên:** Phùng Thanh Nhân
```
[Records từ database searching (N = 35)]
← String A (Topic 1) – arXiv = 9, Google Scholar = 8
← String B (Topic 2) – arXiv = 10, Google Scholar = 8
↓

[Sau khi xóa duplicate (N = 30)]
← Số bị loại (trùng lặp) = 5
↓

┌─────────────────────────────────────────┐
│ Screened title + abstract (N = 30)     │
│ └── Excluded (N = 10):                 │
│     EC-O = 7 (không đúng topic)        │
│     EC-N = 2 (không có thực nghiệm)   │
│     EC-S = 1 (dưới 4 trang)           │
└─────────────────────────────────────────┘
↓ 20 papers pass V1 (INCLUDE + Unsure)

┌─────────────────────────────────────────┐
│ Snowballing                            │
│ Scan 20 paper included                 │
│ Paper mới phát hiện: 0                 │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│ Full-text V2 screening (N = 20)        │
│ └── Excluded (N = 0)                   │
└─────────────────────────────────────────┘

↓ 20 papers INCLUDE final

[03_final_included.csv – N = 20]
├── Topic 1 (BDD/Gherkin): 7 papers
└── Topic 2 (Unit Test): 13 papers
```
