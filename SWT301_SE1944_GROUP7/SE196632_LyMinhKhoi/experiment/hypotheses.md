# Hypotheses - TOPIC 2: Unit Test Case Generation																									
																									
## ## RQ1: Đánh giá năng lực tối ưu độ bao phủ mã nguồn (Branch Coverage) của GPT-4 so với Baseline truyền thống																									
- **H0:** Việc áp dụng mô hình can thiệp GPT-4 (Fixturize) **KHÔNG** giúp đạt mức tăng trưởng độ bao phủ nhánh trung bình (Branch coverage) ≥ 24.08% trên tập dữ liệu hỗn hợp Python và Java so với các giải pháp kiểm thử truyền thống.																									
- **H1:** Việc áp dụng mô hình can thiệp GPT-4 (Fixturize) **ĐẠT** mức tăng trưởng độ bao phủ nhánh trung bình (Branch coverage) ≥ 24.08% trên tập dữ liệu hỗn hợp Python và Java so với các giải pháp kiểm thử truyền thống.																									
- **Statistical test dự kiến:** **Wilcoxon signed-rank test** (do chỉ số Branch Coverage là dữ liệu liên tục thu thập cặp trước/sau can thiệp trên cùng một phân hệ hàm kịch bản).																									
																									
## ## RQ2: Đánh giá sự cải thiện về tỷ lệ biên dịch và thực thi thành công (Suite Pass Rate) của mã kiểm thử sinh ra																									
- **H0:** Kỹ thuật sinh mã kiểm thử bằng GPT-4 **KHÔNG** làm tăng tỷ lệ kịch bản thực thi thành công (Suite Pass Rate) đạt ngưỡng tối thiểu ≥ 43% trên các hàm kiểm thử phức tạp.																									
- **H1:** Kỹ thuật sinh mã kiểm thử bằng GPT-4 **ĐẠT** tỷ lệ kịch bản thực thi thành công (Suite Pass Rate) đạt ngưỡng tối thiểu ≥ 43% trên các hàm kiểm thử phức tạp.																									
- **Statistical test dự kiến:** **Binomial exact test** (do output của từng ca kiểm thử cấu thành tỷ lệ Pass Rate mang tính chất nhị phân độc lập: Pass hoặc Fail).																									
																									
## ## RQ3: So sánh hiệu năng diệt đột biến mã nguồn (Mutation Score) giữa mô hình can thiệp GPT-4o và Llama3-70B																									
- **H0:** Năng lực diệt đột biến (Mutation score) của mã kiểm thử do GPT-4o sinh ra **KHÔNG** có sự khác biệt có ý nghĩa thống kê so với mã do mô hình mã nguồn mở Llama3-70B sinh ra trên hệ thống benchmark EvalPlus.																									
- **H1:** Năng lực diệt đột biến (Mutation score) của mã kiểm thử do GPT-4o sinh ra **ĐẠT** sự khác biệt vượt trội có ý nghĩa thống kê so với mã do mô hình mã nguồn mở Llama3-70B sinh ra trên hệ thống benchmark EvalPlus.																									
- **Statistical test dự kiến:** **Mann-Whitney U test** (do đây là phép thử so sánh giá trị phân phối của hai hệ thống mô hình độc lập thực thi trên các tập tác vụ kiểm thử không bắt cặp).																									