# Gap Statement - Nguồn 3 (CORE)
**Thành viên thực hiện:** Lý Minh Khôi
**Dựa trên paper:** "An Empirical Study on Fine-Tuning Large Language Models for Automated Unit Test Generation" (Yuan et al., 2024)

## 1. Khoảng trống nghiên cứu (The Research Gap)
Mặc dù nghiên cứu của *Yuan et al. (2024)* đã chứng minh rằng GPT-4 có khả năng sinh unit test case tự động đạt độ bao phủ nhánh vượt trội (trên 80%) và có điểm đột biến khá tốt (khoảng 61.2%) đối với các hàm Java/Python. Tuy nhiên, nghiên cứu này vẫn tồn tại một số hạn chế lớn (Gap) sau:
- **Chưa đi sâu vào đối tượng kiểm thử cụ thể theo từng ngưỡng phức tạp nhỏ:** Nghiên cứu gốc đánh giá chung trên một tập dataset lớn (Defects4J) có độ phức tạp vòng cung (Cyclomatic Complexity - CC) trải dài quá rộng từ 5 đến 20, chưa bóc tách và so sánh chi tiết hiệu năng của mô hình trong phân khúc CC trung bình cụ thể từ 5 đến 15.
- **Thiếu bối cảnh so sánh với nhân lực thực tế tại chỗ (Human Baseline):** Nghiên cứu chủ yếu so sánh GPT-4 với các công cụ sinh test case tự động truyền thống như EvoSuite hay Randoop, chưa thực hiện đối chiếu thực nghiệm trực tiếp với test suite do các sinh viên chuyên ngành kỹ thuật phần mềm tự viết tay thủ công để đánh giá tính thực tế của việc thay thế sức người trong môi trường giáo dục/dự án nhỏ.

## 2. Giải pháp lấp đầy khoảng trống của nhóm SE1944 (How our lab fills the gap)
Bài Lab thực hành của nhóm SE1944 sẽ trực tiếp lấp đầy khoảng trống nghiên cứu trên bằng cách:
1. **Thu hẹp và tập trung phạm vi:** Tập trung kiểm thử thực nghiệm trên các hàm Java và Python được lọc kỹ với độ phức tạp vòng cung nằm chính xác trong khoảng từ 5 đến 15 nhằm xác định rõ ngưỡng suy giảm hiệu năng của GPT-4.
2. **Bổ sung Baseline so sánh thực tế:** Đưa tập dữ liệu test suite do chính sinh viên viết tay (Manual Student Tests) làm cấu trúc so sánh đối chứng trực tiếp bên cạnh công cụ tự động Randoop. 
3. **Kiểm định thống kê chặt chẽ:** Sử dụng kiểm định phi tham số Mann-Whitney U ($p < 0.05$) để khẳng định sự khác biệt về Branch Coverage ($\ge 80\%$) và Mutation Score ($\ge 60\%$) giữa GPT-4 và sinh viên viết tay có thực sự mang ý nghĩa thống kê hay không.