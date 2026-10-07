# Evidence Table – LLM for Automated Acceptance Test Case & Unit Test Case Generation
**Thành viên:** Phùng Thanh Nhân
**Evidence table: N = 20 papers**

## Topic 1 – Acceptance Test Case Generation (7 papers)

| Paper (Tên + Năm + Venue) | Tool/LLM | Dataset | Metric | Kết quả | Hạn chế tự nêu |
|---------------------------|----------|---------|--------|---------|----------------|
| Ferreira et al., 2025, IEEE/ACM AST | GPT-4 Turbo (AutoUAT+TestFlow) | User stories từ web app công ty đối tác | Tỷ lệ hữu ích, executable rate | 95% hữu ích; 92% dùng được; 60% dùng ngay | Chỉ 1 công ty, chưa generalize |
| Fonseca et al., 2025, IEEE/ACM ASE | LLM chuyên dụng (AToMIC) | MyBMW Flutter – 13 issues, 170+ màn hình | Executable syntax rate, pass rate | 93.3% test đúng cú pháp; 100% UI tests OK | Chỉ Flutter |
| Hassani et al., 2025, IST | Claude, Llama | 60 kịch bản từ quy định an toàn thực phẩm | Semantic similarity, rõ ràng, đầy đủ | Rõ ràng 100%; phù hợp 95%; đầy đủ 94.2% | Domain pháp lý, hallucination nhỏ |
| Jagielski et al., 2025, cs.SE | Private GPT | Acceptance criteria từ epics/stories | Khả năng đọc hiểu, số dòng code | 2 bước story→Test Case→test tốt hơn | Chỉ 2 kịch bản đơn giản |
| Rathnayake et al., 2026, arXiv | GPT-4, Claude 3, Gemini | 500 user stories từ 4 phần mềm thực tế | Semantic similarity, text similarity, human assessment | GPT-4 cao nhất text/semantic; Claude 3 cao nhất human eval | Input quality ảnh hưởng lớn |
| Fernandes et al., 2025, SBES | 7 LLMs: GPT-3.5/4/4o, LLaMA, Phi-3, Gemini, DeepSeek | 1,286 test descriptions thực tế | METEOR score, variability, ANOVA | Zero-shot hiệu quả tương đương few-shot; Gemini tốt nhất | Chỉ 10 samples |
| Paduraru et al., 2025, ICAART | Llama3.1 8B fine-tuned + NLP + Agentic AI | 13 GitHub projects + 2 game projects | Step matching accuracy, user iterations | 1,484/1,983 tests matched; 4.7 iter/step | Fine-tuned model nhỏ, lỗi đổi đơn vị |

## Topic 2 – Unit Test Case Generation (13 papers)

| Paper (Tên + Năm + Venue) | Tool/LLM | Dataset | Metric | Kết quả | Hạn chế tự nêu |
|---------------------------|----------|---------|--------|---------|----------------|
| Wang et al., 2025, IEEE TSE | ChatTester (GPT-4) | 300 Java projects từ GitHub | Branch coverage, mutation score | Branch coverage tăng 23% vs EvoSuite; Mutation 78% | Chi phí token cao |
| Khelladi et al., 2025, ACM TOSEM | DeepSeek-Coder, StarCoder | HumanEval-X, Defects4J | Pass@k, compilability | Compilability đạt 89%; sửa lỗi hồi quy tốt | Khó với hàm thừa kế |
| Huang et al., 2025, IEEE/ACM ICSE | PyTestGen (GPT-4o) | 150 Python open-source repos | Statement coverage, flaky rate | Coverage đạt 84.5%; tỷ lệ flaky test < 3% | Chạy chậm |
| Xie et al., 2025, IEEE/ACM ICSE | InternLM-Math + Agent | 85 mã nguồn thuật toán | Logic correctness, edge cases | Khắc phục 92% lỗi chia cho 0 và tràn số | Chỉ kiểm thử đơn vị toán học |
| Mastropaolo et al., 2025, ESE | GitHub Copilot (Codex) | 1,000 phương thức Java | Trùng lặp với developer test | 64% test sinh ra giống hệt test viết tay | Thiếu đa dạng kịch bản |
| Zhang et al., 2026, cs.SE | LLaMA-3-70B fine-tuned | Tập dữ liệu đóng của doanh nghiệp | Line coverage, execution time | Đạt 81.2% line coverage trong 4.2 giây/hàm | Đóng gói môi trường phức tạp |
| Toisi et al., 2025, SBES | GPT-4o, DeepSeek V3 | Dự án Java | Mutation score | GPT-4o kết quả tương đương DeepSeek V3 | Chỉ so sánh hai mô hình lớn |
| Díaz-Arrieta et al., 2024, SSRN | LLM (ChatGPT) | Các dự án quy hoạch động | Pass rate, đối chiếu thủ công | So sánh trực tiếp LLM vs người viết thủ công | Tập dữ liệu nhỏ |
| Ouédraogo et al., 2024, arXiv | Nhiều LLM khác nhau | 690 lớp Java | Khả năng biên dịch, độ phủ | Nghiên cứu quy mô lớn đầu tiên về tính biên dịch | Chưa đo mutation score |
| Ouédraogo et al., 2026, ESE Springer | LLMs + prompt engineering | Dự án Java (JUnit) | Branch coverage, line coverage | Thực nghiệm diện rộng với 5 chiến lược prompt | Chỉ giới hạn ở ngôn ngữ Java |
| Godage et al., 2025, IEEE | ChatGPT, Claude, LLaMA, Command | Nhiều dự án Java | Chỉ số hiệu quả kiểm thử | Khảo sát tính đa dạng của 4 cấu hình mô hình | Quy mô mẫu nhỏ |
| Shang et al., 2025, FSE/ACM | Mô hình LLM tinh chỉnh | Đa dự án | Sinh kiểm thử và sinh xác định | Nghiên cứu tinh chỉnh quy mô lớn hiệu quả | Đòi hỏi tài nguyên huấn luyện |
| Yang et al., 2025, ASE Springer | Mô hình tiến hóa kết hợp LLM | Các ngôn ngữ phi định kiểu (Python) | Độ phủ đo tại mức Python bytecode | Tối ưu hóa độ phủ nhánh sâu tại tầng mã máy | Độ phức tạp thuật toán cao |
