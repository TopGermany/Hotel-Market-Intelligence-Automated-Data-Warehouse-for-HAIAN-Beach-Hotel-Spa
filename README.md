# 🏨 Hotel Market Intelligence & Automated Data Warehouse for HAIAN Beach Hotel & Spa

![Data Engineering & Analytics Architecture](https://img.shields.io/badge/Architecture-Medallion-blue)
![Tech Stack](https://img.shields.io/badge/Stack-Python%20%7C%20Airflow%20%7C%20BigQuery-success)
![Data Analyst](https://img.shields.io/badge/Role-Data%20Analyst%20%2B%20Data%20Engineer-orange)

## 📖 1. Tổng quan dự án

Đây là dự án Data Analytics kết hợp Data Engineering end-to-end dành cho bài toán quản trị doanh thu tại **HAIAN Beach Hotel & Spa**. Dự án tích hợp dữ liệu vận hành nội bộ—bao gồm booking, doanh thu, tồn phòng, chi phí và đánh giá khách hàng—với dữ liệu giá phòng đối thủ được thu thập từ Booking.com và iVIVU.

Ở góc độ **Data Analyst**, dự án tập trung xây dựng hệ thống KPI, phân tích các yếu tố ảnh hưởng đến lợi nhuận và thiết kế dashboard hỗ trợ Revenue Manager ra quyết định. Ở góc độ **Data Engineering**, toàn bộ dữ liệu được thu thập, kiểm tra chất lượng, mô hình hóa, nạp vào BigQuery và tự động hóa bằng Apache Airflow.

## ❕ 2. Vấn đề doanh nghiệp

Từ tháng 6 đến tháng 8 năm 2025, chỉ số **ProfitPAR của HAIAN Beach Hotel & Spa chỉ đạt 550.000 VNĐ/phòng, thấp hơn mục tiêu 750.000 VNĐ/phòng**, cho thấy hiệu quả khai thác phòng và khả năng tối ưu lợi nhuận chưa đạt kỳ vọng.

Mặc dù khách sạn có thể duy trì công suất và doanh thu ở mức cao, lợi nhuận thực tế vẫn chịu ảnh hưởng bởi nhiều yếu tố như giá bán phòng, cơ cấu loại phòng, chi phí vận hành, hoa hồng OTA, chương trình khuyến mãi và cơ cấu kênh phân phối. Nếu chỉ theo dõi doanh thu hoặc Occupancy, nhà quản lý khó xác định nguyên nhân thực sự làm ProfitPAR chưa đạt mục tiêu.

Dự án vì vậy hướng tới xây dựng một nguồn dữ liệu tập trung và hệ thống phân tích có khả năng phân rã khoảng cách lợi nhuận, xác định các yếu tố tác động và hỗ trợ lựa chọn hành động phù hợp.

## ❔ 3. Câu hỏi phân tích

1. ProfitPAR, Net Profit, RevPAR, ADR và Occupancy biến động như thế nào trong giai đoạn tháng 6–8/2025?
2. Khoảng cách giữa ProfitPAR thực tế và mục tiêu 750.000 VNĐ/phòng đến từ giá bán, công suất, cơ cấu phòng, cơ cấu kênh hay chi phí?
3. Những ngày trong tuần, loại phòng, phân khúc khách hàng và kênh bán nào tạo ra doanh thu và lợi nhuận tốt nhất?
4. Chi phí hoa hồng và phân phối qua OTA ảnh hưởng như thế nào đến Net ADR và lợi nhuận theo kênh?
5. Lead time, tỷ lệ hủy phòng và thời gian lưu trú tác động như thế nào đến hiệu quả khai thác phòng?
6. Giá phòng của HAIAN đang ở vị trí nào so với nhóm khách sạn cạnh tranh trong cùng ngày lưu trú và điều kiện giá?
7. Những vấn đề nào trong trải nghiệm khách hàng có thể ảnh hưởng đến khả năng duy trì giá bán và lợi nhuận?

| Hạng mục | Kết quả thực hiện |
|---|---|
| Phân tích nghiệp vụ | Xác định câu hỏi quản trị doanh thu, KPI, hướng phân tích và đề xuất hành động |
| Phân tích dữ liệu | ProfitPAR, ADR, RevPAR, công suất phòng, chi phí kênh, hủy phòng, lead time, đánh giá khách và giá đối thủ |
| Mô hình dữ liệu | Mô hình chiều trên BigQuery gồm 7 dimension, 7 fact, 1 bảng KPI tổng hợp và 4 analytical view |
| Data pipeline | Thu thập và kiểm tra bằng Python, điều phối Airflow, incremental load vào BigQuery, quarantine và audit |
| Bàn giao | Dữ liệu cho Looker Studio, Docker, automated test, CI, tài liệu kỹ thuật, báo cáo và slide thuyết trình |

## ✅ 4. Kết quả phân tích nổi bật

Dữ liệu vận hành lịch sử được phân tích trong giai đoạn **tháng 6–8/2025**. Các KPI dạng tỷ lệ được tính theo tỷ lệ của tổng thay vì lấy trung bình cộng các tỷ lệ theo ngày.

| Phát hiện | Bằng chứng | Hàm ý hành động |
|---|---:|---|
| Lợi nhuận chưa đạt mục tiêu | ProfitPAR trung bình khoảng **550 nghìn VND**, thấp hơn mục tiêu **750 nghìn VND** | Tối ưu lợi nhuận trên mỗi phòng khả dụng thay vì chỉ theo doanh thu hoặc công suất |
| Tháng 7 có hiệu quả tốt nhất | Occupancy **91,7%**, ADR **2,54 triệu VND**, ProfitPAR **758 nghìn VND** | Xác định và tái áp dụng điều kiện giá và cơ cấu bán của tháng 7 khi nhu cầu cho phép |
| Cuối tuần tạo ra nhiều giá trị hơn | ProfitPAR thứ Bảy/Chủ nhật khoảng **885/862 nghìn VND**, trong khi thứ Hai khoảng **493 nghìn VND** | Áp dụng chính sách giá và kiểm soát tồn phòng theo ngày trong tuần |
| Kênh trực tiếp có lợi thế về chi phí phân phối | Website có ADR khoảng **2,28 triệu VND** và distribution rate **4,7%**; Booking.com khoảng **25,1%** | Theo dõi Net ADR và contribution sau chi phí kênh; tăng tỷ trọng đặt phòng trực tiếp |
| Hành vi đặt phòng cung cấp tín hiệu dự báo | Tỷ lệ hủy **9,49%**, lead time trung vị **36 ngày**, thời gian lưu trú trung bình **2,32 đêm** | Đưa booking window, hủy phòng và length of stay vào quyết định doanh thu |
| Trải nghiệm khách có thể giới hạn khả năng tăng giá | Điểm đánh giá trung bình **4,45/5**; vấn đề thường gặp gồm chờ thang máy, kỳ vọng về view phòng và xếp hàng ăn sáng | Kết nối vấn đề dịch vụ với loại phòng, kênh bán, hủy phòng và chính sách giá |

Các kết quả trên mô tả giai đoạn lịch sử đã phân tích, không phải kết luận quan hệ nhân quả hoặc kết quả của một thử nghiệm giá có đối chứng.

## 🏭 5. Kiến trúc end-to-end

<img width="882" height="505" alt="Screenshot 2026-07-28 220616" src="https://github.com/user-attachments/assets/9aae5f6f-2416-4bd9-93a8-5ed08202ecc7" />


## 📝 6. Mô hình dữ liệu

Data Warehouse sử dụng dimensional modeling với grain, primary key, foreign-key validation và trường partition theo ngày được định nghĩa rõ ràng.

- **Dimension:** ngày, khách sạn, loại phòng, kênh bán, phân khúc khách, nhóm chi phí và chương trình khuyến mãi.
- **Fact:** booking, tồn phòng, chi phí phòng, doanh thu phòng, chi phí phân phối, đánh giá khách và giá phòng đối thủ.
- **Gold view:** phân tích chi phí ngày, ProfitPAR ngày, tổng hợp giá đối thủ và so sánh giá HAIAN với thị trường.

<img width="1237" height="695" alt="image" src="https://github.com/user-attachments/assets/436be9e5-48ea-4125-9681-263a04a7220f" />


## 🌊 6. Pipeline tự động

Airflow DAG chạy hằng ngày lúc **02:00 theo múi giờ Asia/Ho_Chi_Minh**. Hai tác vụ thu thập Booking.com và iVIVU chạy song song trước khi hợp nhất thành một bộ dữ liệu canonical.

<img width="1593" height="2048" alt="0" src="https://github.com/user-attachments/assets/e608667b-02bf-4365-b01d-4df9e83e31e9" />


Các cơ chế kỹ thuật chính:

- schema BigQuery tường minh thay vì suy luận kiểu dữ liệu;
- staging kết hợp `MERGE` để incremental load có tính idempotent;
- chế độ full snapshot `WRITE_TRUNCATE` dành cho BigQuery Sandbox;
- kiểm tra cấp dòng, business rule, foreign key và overbooking;
- lưu dòng vi phạm vào quarantine thay vì tự động sửa âm thầm;
- audit theo từng lần chạy, bao gồm trạng thái stage và số dòng;
- Airflow LocalExecutor và PostgreSQL chạy bằng Docker, có healthcheck và init service;
- GitHub Actions kiểm tra compile, Ruff, pytest/coverage, Docker Compose và image build.


## 📊 7. Hệ thống Dashboard Phân tích (Looker Studio)

Để chuyển đổi dữ liệu thô thành những thông tin chi tiết có giá trị hành động, tôi đã thiết kế 3 Dashboard Quản trị kết nối trực tiếp với các Data Marts trên BigQuery.

### 💰 7.1. Dashboard Quản trị Doanh thu 
<!-- 📸 THÊM ẢNH REVENUE DASHBOARD VÀO DÒNG BÊN DƯỚI -->
<img width="1153" height="691" alt="Screenshot 2026-07-14 131351" src="https://github.com/user-attachments/assets/93832e96-44b3-4346-882e-a3839a451a36" />


**Phân tích & Insight:** Phân rã doanh thu theo Kênh (Channel) và Phân khúc Khách hàng (Customer Segment). Giúp phát hiện nhanh tình trạng nếu Công suất phòng (Occupancy) rất cao nhưng RevPAR lại thấp, báo hiệu rằng khách sạn đang bán phòng với giá quá rẻ.

### 📈 7.2. Dashboard Phân tích Lợi nhuận 
<!-- 📸 THÊM ẢNH PROFITABILITY DASHBOARD VÀO DÒNG BÊN DƯỚI -->
<img width="1155" height="695" alt="Screenshot 2026-07-14 131456" src="https://github.com/user-attachments/assets/6d2ae9ed-bd4d-44e5-950a-6fe282fc04ee" />


**Phân tích & Insight:** Trực quan hóa dòng chảy (Waterfall) từ Doanh thu gộp đến Lợi nhuận ròng. Trả lời câu hỏi sống còn: *"Liệu các chương trình voucher và tiền hoa hồng OTA có đang "ăn" hết lợi nhuận của chúng ta không?"* Dashboard giúp xác định chính xác ProfitPAR thực tế mang lại từ từng nguồn đặt phòng.

### 🕵️ 7.3. Dashboard Tình báo Thị trường (Market Intelligence)
<!-- 📸 THÊM ẢNH MARKET INTELLIGENCE DASHBOARD VÀO DÒNG BÊN DƯỚI -->
<img width="1155" height="691" alt="Screenshot 2026-07-14 131429" src="https://github.com/user-attachments/assets/ebb83a32-5540-43a5-bc75-d07e4b55f19d" />


**Phân tích & Insight:** So sánh ADR (Giá bán bình quân) của HAIAN với giá trung bình của thị trường xung quanh. Hệ thống trực quan hóa cảnh báo ngay lập tức khi đối thủ giảm giá mạnh hoặc hết phòng (Sold-out). Từ đó, khách sạn có thể áp dụng chiến lược **Định giá Động (Dynamic Pricing)** một cách linh hoạt.

### 
---

## 🎯 8. Đề xuất Kinh doanh (Actionable Insights)
Dựa trên dữ liệu được thu thập và phân tích từ hệ thống Dashboard, dưới đây là các đề xuất chiến lược dựa trên dữ liệu (Data-driven) nhằm khôi phục ProfitPAR về mức mục tiêu 850.000 VNĐ:

1. **Áp dụng Định giá Động (Dynamic Pricing) theo Chỉ số Cạnh tranh:** Dữ liệu cho thấy khi các đối thủ cùng phân khúc đạt tỷ lệ lấp đầy (Sold-out rate) **> 85%** trên Booking.com, hệ thống của HAIAN vẫn đang giữ nguyên mức giá cố định. Khuyến nghị: Thiết lập quy tắc tự động tăng ADR lên **5% - 10%** ngay khi nguồn cung thị trường xung quanh khan hiếm. Thao tác này ước tính có thể cải thiện RevPAR thêm **8%** trong các dịp lễ.
2. **Tối ưu hóa Kênh Phân phối để Giảm chi phí OTA:** Dashboard Lợi nhuận chỉ ra rằng dù OTA chiếm **65% tổng doanh thu**, nhưng chi phí hoa hồng (15-20%) đã bào mòn đáng kể lợi nhuận ròng. Ngược lại, kênh Direct Booking (đặt trực tiếp) có biên lợi nhuận cao hơn **18%**. Khuyến nghị: Dịch chuyển 15% ngân sách từ các chiến dịch giảm giá trên OTA sang các chiến dịch Marketing nội bộ để thúc đẩy Direct Booking đối với nhóm khách hàng FIT (Khách lẻ).
3. **Đánh giá lại Chiến lược Phát hành Voucher:** Việc giảm giá ồ ạt qua Voucher trong tháng 7 khiến ADR giảm sâu nhưng Occupancy (Công suất phòng) chỉ tăng nhẹ **2.5%**, dẫn đến ProfitPAR sụt giảm nghiêm trọng. Khuyến nghị: Dừng việc phát hành voucher giảm giá đại trà. Chuyển sang chiến lược Upselling (nâng hạng phòng) hoặc áp dụng điều kiện "Lưu trú tối thiểu 3 đêm" để tối đa hóa lợi nhuận trên mỗi khách hàng.

---

## 🎓 9. Mình đã học được gì qua dự án ? 
Thông qua việc tự tay xây dựng dự án Data Warehouse toàn diện này, tôi đã đúc kết được những kinh nghiệm vô giá không chỉ về mặt công cụ mà còn về tư duy giải quyết vấn đề:

* **Quản trị Pipeline với Apache Airflow:** Hiểu sâu về cách điều phối (Orchestration), lên lịch trình (DAGs) và giám sát trạng thái của các luồng dữ liệu (ETL pipeline). Điều này giúp tôi nhận ra tầm quan trọng của việc tự động hóa và khả năng theo dõi luồng dữ liệu một cách trực quan thay vì chạy script thủ công.
* **Tích hợp AI Agent vào Data Engineering:** Tiên phong trong việc sử dụng Google ADK (Gemini LLM) làm "trái tim" điều phối hệ thống. Tôi học được cách biến AI từ một công cụ chat trở thành một Agent có khả năng tự động phân tích tình huống và ra quyết định trình tự chạy các tác vụ cào dữ liệu một cách linh hoạt.
* **Tư duy Phân tích Hệ thống & Mô hình hóa (Data Modeling):** Học được cách bóc tách một bài toán kinh doanh "mù mờ" (Làm sao để tăng lợi nhuận khách sạn?) thành các thực thể dữ liệu rõ ràng. Từ đó, tôi biết cách thiết kế mô hình **ERD (Fact & Dimension)** chuẩn mực sao cho đáp ứng được mọi góc độ phân tích và vẽ Dashboard một cách mượt mà nhất.

---

Cảm ơn bạn đã quan tâm đến dự án của tôi! Nếu có cơ hội trao đổi hoặc hợp tác, vui lòng liên hệ với tôi qua Email: hoquocuong2005@gmail.com 

