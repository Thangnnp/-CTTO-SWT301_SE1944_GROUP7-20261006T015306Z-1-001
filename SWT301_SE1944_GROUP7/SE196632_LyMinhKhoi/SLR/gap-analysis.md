# GAP Analysis – Personal Research Area
Evidence table: N = 5 paper | Ngày: 2026-06-08

## ## Bảng GAP

| Cột | Phát hiện | Loại GAP | Phản chứng |
| :--- | :--- | :--- | :--- |
| Tool/LLM | Phần lớn các nghiên cứu hiện tại (như P1, P5) chỉ tập trung vào các dòng mô hình thương mại đóng của OpenAI (ChatGPT/GPT-4). Chưa có nghiên cứu nào đánh giá sâu năng lực của mô hình mã nguồn mở thế hệ mới tối ưu chi phí là DeepSeek-V3 trong Software Testing. | GAP-T | [x] Quét qua P1, P2, P3, P4, P5 |
| Metric | Các framework hiện tại (như P2, P3) chủ yếu chạy đua tối ưu độ phủ mã nguồn (Coverage-Guided). Rất ít bài phân tích sâu về chất lượng kiểm thử ở mức độ logic hoặc các lỗi khẳng định trùng lặp (Redundant Assertions) sinh ra từ LLM. | GAP-M | [x] Quét qua P1, P2, P3, P4, P5 |

**Ưu tiên khi nhiều GAP xung đột:** GAP-T > GAP-M

## ## GAP Chính: [GAP-T]
Đánh giá và tối ưu hóa năng lực sinh mã kiểm thử tự động (Unit Test Generation) của mô hình mã nguồn mở thế hệ mới DeepSeek-V3 so với mô hình đóng thương mại (ChatGPT) trên khía cạnh kiểm thử đột biến (Mutation Testing).

## ## GAP Secondary: [GAP-M]
Đo lường chi tiết tỷ lệ khẳng định trùng lặp (Redundant Assertions) nhằm đánh giá chất lượng logic và độ tinh gọn của mã kiểm thử sinh bởi LLM khi cố gắng tối ưu độ phủ.

## ## Chi tiết kiểm tra phản chứng
* **GAP tuyên bố:** Chưa có nghiên cứu nào trong 5 paper được chọn đánh giá khả năng tối ưu hóa cấu trúc Assertion và độ bền vững mã nguồn của DeepSeek-V3 trong kiểm thử Java.
* **Chi tiết rà soát từng paper trong Evidence Table cá nhân:**
  * **P1 (Frank Tip et al., 2025):** Thực nghiệm diện rộng trên các LLM phổ thông của OpenAI nhưng hoàn toàn KHÔNG có cấu hình mô hình DeepSeek-V3 -> **Bác bỏ phản chứng.**
  * **P2 (CoverUp, 2025):** Tập trung vào thuật toán lặp để đẩy tối đa độ phủ dòng lệnh (Coverage-Guided), KHÔNG đo lường cấu trúc Assertions hay Mutation Score -> **Bác bỏ phản chứng.**
  * **P3 (AGONETEST, 2025):** Đánh giá Unit Test tự động cho Java nhưng sử dụng các mô hình nền tảng và metric độ phủ truyền thống, KHÔNG phân tích cấu trúc rác câu lệnh assert -> **Bác bỏ phản chứng.**
  * **P4 (Guancheng Wang, 2025):** Có hướng tiếp cận dùng kỹ thuật Mutation-Guided để hướng dẫn sinh test nhưng áp dụng trên các LLM đời cũ, CHƯA khai thác năng lực của DeepSeek-V3 -> **Bác bỏ phản chứng.**
  * **P5 (Yutian Tang, 2023):** So sánh ChatGPT với kỹ thuật SBST truyền thống, sử dụng tập dữ liệu cũ từ năm 2023 nên chưa cập nhật mô hình mới -> **Bác bỏ phản chứng.**

$->$ **Kết luận:** XÁC NHẬN GAP HỢP LỆ (Không có paper nào giải quyết trùng lặp với thiết kế thực nghiệm này).

## ## Feasibility Check – GAP Chính
| Tiêu chí | Mức | Ghi chú |
| :--- | :--- | :--- |
| Dataset | [x] An toàn | Sử dụng bộ dữ liệu Java benchmark có sẵn từ các paper gốc (như Defects4J hoặc tương đương). |
| Tool/API | [x] An toàn | Chi phí gọi API DeepSeek-V3 cực kỳ rẻ, nằm trong khả năng chi trả cá nhân. |
| Compute | [x] An toàn | Chỉ gọi API và chạy thực thi kiểm thử cục bộ trên máy cá nhân, không cần hạ tầng GPU. |
| Skills | [x] An toàn | Bản thân em đã làm chủ kỹ thuật sinh test bằng prompt và kết nối API từ RBL-1. |
| Thời gian | [x] An toàn | Phạm vi thực nghiệm cô đọng trên 5 nguồn bài rõ ràng nên kiểm soát thời gian rất tốt. |

**Kết quả:** [x] An toàn -> Tiếp tục triển khai GAP này.