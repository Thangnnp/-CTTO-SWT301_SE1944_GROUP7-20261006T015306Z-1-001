# data/raw — Dataset gốc (KHÔNG chỉnh sửa)

> [RBL-4] Mô tả nguồn dataset gốc dùng cho thực nghiệm.

## Nguồn

- **Tên:** Defects4J v2.0.0
- **URL:** https://github.com/rjust/defects4j (tag `v2.0.0`)
- **License:** MIT License
- **Focal methods:** `data/raw/methods/methods.json` (30 method, tất cả `verified: true`)

## Phạm vi — 30 focal methods (bug ID thật đã approve)

| Project | Bug IDs |
|---------|---------|
| Lang (commons-lang) | 8, 10, 19, 22, 26, 30, 41, 42, 57, 60 |
| Math (commons-math) | 2, 9, 27, 53, 55, 59, 63, 70, 75, 79 |
| Chart (jfreechart) | 1, 10, 11, 15, 17, 19, 21, 22, 23, 24 |

## Cấu trúc `methods.json`

Mỗi entry: `id`, `class`, `method`, `source` (mã nguồn fixed thật của Defects4J), `verified`.

## Ghi chú verify

- Lang/Math: lấy source qua `git show <fixed-sha>:<path>` theo `commit-db`.
- Chart: SVN → verify bằng `git log -G` pickaxe trên `jfree/jfreechart` (+ `jcommon` cho Chart-11), đối chiếu `Chart/patches/<id>.src.patch`.
- Không method nào dựng lại từ trí nhớ (xem `notes.md` repo).
