# Phân Tích Khoảng Trống Nghiên Cứu (GAP Analysis) & Kiểm Tra Phản Chứng
**Thành viên:** Phùng Thanh Nhân
**Đề tài:** LLM for Automated Acceptance Test Case & Unit Test Case Generation

## 1. Bảng Kiểm Tra Phản Chứng Kiểm Định GAP (Evidence Counter-Check)

| Mã GAP | Tuyên bố Khoảng trống ban đầu | Trạng thái | Bằng chứng phản chứng từ Y văn (20 Paper) |
|:---|:---|:---:|:---|
| **GAP-T** | Thiếu so sánh trực tiếp GPT-4o vs expert viết Acceptance Test Case tay trên user stories Connextra | **Được xác nhận (VALID)** | • Các nghiên cứu trước đây so sánh với người dùng thực tế tại công ty/issue thực tế, không có nhóm kiểm soát bởi expert.<br>• Các bài toán khác có chuyên gia nhưng thuộc domain pháp lý hoặc quy định đặc thù.<br>• Không có paper nào dùng user stories chuẩn cấu trúc Connextra đối chiếu trực tiếp với kịch bản văn bản tự nhiên của expert. |
| **GAP-M** | Thiếu đo semantic similarity định lượng trên văn bản test case từ user stories Connextra | **Được xác nhận (VALID)** | • Các nghiên cứu đo tính rõ ràng, đầy đủ hoặc cú pháp mã nguồn.<br>• Một số nghiên cứu đo semantic similarity nhưng dùng mô tả yêu cầu chung chung, không dùng Connextra format.<br>• Chưa có nghiên cứu nào đo Cosine Similarity/BLEU trên tập test case văn bản tự nhiên sinh từ Connextra. |
| **GAP-T2** | Thiếu so sánh GPT-4 với sinh viên viết unit test thủ công ở quy mô đủ lớn | **Được xác nhận (VALID)** | • Có nghiên cứu so sánh LLM vs human viết tay nhưng cỡ mẫu rất nhỏ và chưa đo mutation score.<br>• Các nghiên cứu lớn khác đều chỉ so sánh với các công cụ sinh mã tự động (EvoSuite, Randoop). |
| **GAP-D** | Thiếu dataset tích hợp cả Acceptance Test Case generation và Unit Test generation trên cùng một codebase | **Được xác nhận (VALID)** | • Toàn bộ 20 paper đều tách rời hai bài toán này. Nhóm kịch bản kiểm thử dùng tập user stories riêng; nhóm Unit Test dùng các benchmark code cô lập. Không có pipeline tích hợp đồng thời cả hai tầng trên cùng một hệ thống. |

## 2. Đánh Giá Tính Khả Thi Thực Nghiệm (Feasibility & Risk Assessment)

### 2.1. Dataset
* **Rủi ro:** Cần thu thập cấu trúc user stories Connextra đi kèm codebase Java/Python tương ứng để chạy đồng thời cả 2 tầng kiểm thử.
* **Xử lý:** Sử dụng các dự án mã nguồn mở trên GitHub có tài liệu yêu cầu rõ ràng hoặc chuyển đổi hệ thống yêu cầu hiện có sang định dạng Connextra chuẩn (`As a... I want... So that...`).

### 2.2. Tool / API
* **Rủi ro:** Chi phí gọi API của GPT-4o và GPT-4; rủi ro nghẽn mạng hoặc thay đổi phiên bản mô hình.
* **Xử lý:** Cố định phiên bản API cụ thể (ví dụ: `gpt-4o-2024-05-13` và `gpt-4-turbo`), lưu cache cục bộ (local caching) cho toàn bộ phản hồi để tránh gọi trùng lặp.

### 2.3. Compute (Tài nguyên tính toán)
* **Rủi ro:** Chạy Mutation Testing tốn rất nhiều thời gian và CPU do thực thi test suite liên tục với hàng ngàn mutants.
* **Xử lý:** Sử dụng các framework tối ưu như PITest (Java) hoặc MutMut (Python), giới hạn phạm vi mutants trên các hàm có độ phức tạp vòng trung bình.

### 2.4. Ground Truth (Nhóm Đối Chứng)
* **Rủi ro:** Cần kịch bản test case do Expert viết tay và Unit Test do Sinh viên viết tay làm dữ liệu đối chứng.
* **Xử lý:** Lấy dữ liệu từ bài tập lớn/đồ án của sinh viên công nghệ phần mềm đã qua kiểm duyệt (đối với Unit Test) và nhờ 2-3 kỹ sư phần mềm có trên 3 năm kinh nghiệm viết/kiểm định kịch bản Acceptance Test Case.

### 2.5. Skills (Kỹ năng)
* **Xử lý:** Đã cấu hình thành thạo pipeline, thư viện NLP (`sentence-transformers`) và công cụ đo test coverage. Thành thạo phân tích thống kê trên Python (`scipy.stats`).

### 2.6. Thời gian (Time Constraints)
* **Xử lý:** Xây dựng pipeline tự động hóa hoàn toàn từ prompt đến tính toán các chỉ số metric. Quá trình thu thập ground truth từ sinh viên/expert được thực hiện song song trong các tuần đầu.

## 3. Kết Luận Chốt Khoảng Trống (Final GAP Selection)
Nghiên cứu này chính thức lựa chọn giải quyết cả **4 khoảng trống (GAP-T, GAP-M, GAP-T2, GAP-D)** thông qua thiết kế thực nghiệm đồng thời (Co-evaluation Pipeline): Đánh giá mô hình ngôn ngữ lớn trên cùng một hệ thống thực tế từ khâu đặc tả yêu cầu dạng Connextra (Acceptance Test Cases) cho đến khâu cài đặt hàm chi tiết (Unit Test), sử dụng cả hệ thống đo lường ngữ nghĩa định lượng và kiểm định độ đột biến (mutation testing) so với các nhóm đối chứng con người.