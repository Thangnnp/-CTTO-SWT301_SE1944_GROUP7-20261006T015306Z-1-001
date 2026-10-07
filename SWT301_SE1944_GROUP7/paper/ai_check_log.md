# AI Check Log

Công cụ dùng: **SciSpace** (typeset.io/ai-detector) + **ZeroGPT** (zerogpt.com)

Quy tắc:
- Copy từng section riêng lẻ, không paste cả paper cùng lúc.
- Chạy qua cả 2 công cụ. Nếu cả 2 đều báo AI cho cùng 1 đoạn → đoạn đó cần viết lại (paraphrase/thêm góc nhìn cá nhân).
- Ghi kết quả % AI mỗi công cụ + ngày check vào bảng dưới.

## Kết quả

| Section | SciSpace (%AI) | ZeroGPT (%AI) | Ngày check | Trạng thái | Ghi chú |
|---|---|---|---|---|---|
| Abstract | 0% | 0% | 2026-07-24 | OK | Cả 2 công cụ đều 0% — không cần viết lại |
| Introduction | 0% | 1.5% | 2026-07-24 | OK | ZeroGPT flag nhẹ (1.5%, nhãn "chatGPT") — dưới ngưỡng cảnh báo, không cần viết lại |
| Related Work | 0% | 0% | 2026-07-24 | OK | Cả 2 công cụ đều 0% — không cần viết lại |
| Methodology | 0% | 7.1% | 2026-07-24 | OK | ZeroGPT flag nhẹ (7.1%, nhãn "chatGPT") — dưới ngưỡng cảnh báo, không cần viết lại |
| Results | 0% | 15.4% | 2026-07-24 | OK | ZeroGPT flag (15.4%) — vẫn dưới ngưỡng cảnh báo 20%, nhưng cao nhất từ đầu tới giờ, để ý nếu Discussion/Threats cũng cao |
| Discussion | 0% | 0% | 2026-07-24 | OK | Cả 2 công cụ đều 0% — không cần viết lại |
| Threats to Validity | 0% | 0% | 2026-07-24 | OK | Cả 2 công cụ đều 0% — không cần viết lại |
| Conclusion | 0% | 0% | 2026-07-24 | OK | Cả 2 công cụ đều 0% — không cần viết lại |

## Đọc kết quả %AI

- **0–20%**: OK, giữ nguyên.
- **20–50%**: Cảnh báo — nên paraphrase các câu bị flag, thêm số liệu/nhận xét cá nhân.
- **>50%**: Phải viết lại — đặc biệt nếu cả 2 công cụ đều flag cùng đoạn.
