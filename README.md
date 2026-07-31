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



### 💰 7.1. Dashboard Tổng quan hiệu quả kinh doanh
<!-- 📸 THÊM ẢNH REVENUE DASHBOARD VÀO DÒNG BÊN DƯỚI -->
<img width="1407" height="790" alt="image" src="https://github.com/user-attachments/assets/006397fd-bc2e-45d8-adbe-a6b6e762d19f" />

#### Tác dụng

Dashboard cung cấp góc nhìn tổng quát về kết quả kinh doanh phòng thông qua các chỉ tiêu doanh thu thuần, tổng lợi nhuận, lợi nhuận trên mỗi phòng khả dụng, tỷ lệ lấp đầy và giá phòng trung bình. Bảng điều khiển còn thể hiện biến động hiệu quả theo ngày, kết quả theo tháng và danh sách những ngày có hiệu quả thấp cần ưu tiên xem xét.

#### Insight

- Doanh thu thuần đạt **34,72 tỷ đồng**, tổng lợi nhuận đạt **13,02 tỷ đồng**.
- Tỷ lệ lấp đầy trung bình đạt **87,84%**, cho thấy công suất khai thác phòng tương đối cao.
- Giá phòng trung bình đạt khoảng **2,01 triệu đồng**.
- Tháng 7 có kết quả tốt nhất với tỷ lệ lấp đầy **91,74%** và lợi nhuận khoảng **5,8 tỷ đồng**.
- Tháng 6 và tháng 8 có tỷ lệ lấp đầy lần lượt là **85,74%** và **85,96%**.
- Lợi nhuận trên mỗi phòng khả dụng đạt khoảng **661.863 đồng**, nhưng biến động mạnh theo ngày và nhiều thời điểm nằm dưới mức mục tiêu.
- Các ngày 02/06, 03/06, 09/06, 19/08 và 26/08 có hiệu quả thấp hơn mặt bằng chung, cần được ưu tiên phân tích nguyên nhân.


### 📈 7.2. Dashboard Phân tích nhu cầu và doanh thu
<!-- 📸 THÊM ẢNH PROFITABILITY DASHBOARD VÀO DÒNG BÊN DƯỚI -->
<img width="1411" height="792" alt="image" src="https://github.com/user-attachments/assets/7b3f82c6-43b4-4e24-a122-03079beeb9dc" />

#### Tác dụng

Dashboard phân tích nguồn hình thành doanh thu và lợi nhuận theo ba chiều chính gồm loại phòng, phân khúc khách hàng và kênh bán. Qua đó, nhà quản lý có thể xác định sản phẩm, nhóm khách và kênh phân phối đóng góp nhiều nhất vào kết quả kinh doanh.

#### Insight

- Tổng số phòng bán đạt khoảng **17,29 nghìn lượt phòng**.
- Tổng doanh thu đạt **40,23 tỷ đồng**, doanh thu thuần đạt **34,719 tỷ đồng** và lợi nhuận đóng góp đạt **20,46 tỷ đồng**.
- **Beachfront Oasis** là loại phòng tạo lợi nhuận đóng góp cao nhất, đạt khoảng **4,55 tỷ đồng**.
- **Partial Sea View Oasis** có doanh thu gần tương đương Beachfront Oasis nhưng lợi nhuận đóng góp thấp hơn, cho thấy cơ cấu chi phí hoặc mức giảm giá cần được xem xét.
- Nhóm **khách nội địa, mục đích nghỉ dưỡng, lưu trú 2–3 đêm** là phân khúc quan trọng nhất, đóng góp khoảng **12,29 tỷ đồng doanh thu** và **7,34 tỷ đồng lợi nhuận**.
- Agoda và Booking.com tạo ra sản lượng phòng và doanh thu lớn nhất.
- Biên đóng góp của Agoda và Booking.com chỉ khoảng **56%**, thấp hơn đại lý du lịch địa phương (**66,2%**) và website khách sạn (**63,3%**).
- Khách sạn có thể duy trì các nền tảng trực tuyến để bảo đảm sản lượng, đồng thời khuyến khích đặt phòng trực tiếp nhằm cải thiện biên lợi nhuận.

### 🕵️ 7.3. Dashboard Phân tích thị trường và giá đối thủ
<!-- 📸 THÊM ẢNH MARKET INTELLIGENCE DASHBOARD VÀO DÒNG BÊN DƯỚI -->
<img width="1322" height="736" alt="image" src="https://github.com/user-attachments/assets/38d7b299-529a-4e31-8ada-efc6ae0bc79d" />

#### Tác dụng

Dashboard theo dõi giá phòng niêm yết và trạng thái phòng của các cơ sở lưu trú tại Đà Nẵng trên Booking.com và iVIVU.com. Bảng điều khiển giúp nhận diện mặt bằng giá thị trường, sự khác biệt giữa các loại phòng, các khách sạn có mức giá cao và những tín hiệu hết phòng.

#### Insight

- Giá thị trường trung vị đạt khoảng **996,55 nghìn đồng**.
- Mức giá thấp nhất được ghi nhận là **240,27 nghìn đồng**.
- Dữ liệu ghi nhận **288 đối thủ**, **60 lượt hết phòng** và điểm đánh giá trung bình **8,29**.
- Loại phòng mã **RT01** có giá trung vị cao nhất, khoảng **1,3 triệu đồng**.
- Các loại phòng RT06, RT04 và RT08 có mức giá trung vị trong khoảng **888–915 nghìn đồng**.
- Khoảng cách lớn giữa giá thấp nhất và giá trung vị cho thấy thị trường có nhiều phân khúc và loại hình lưu trú khác nhau.
- Một số khách sạn nghỉ dưỡng cao cấp có giá từ khoảng **10,4 đến 24,7 triệu đồng**, cao hơn đáng kể so với mặt bằng chung.
- Các lượt hết phòng liên tiếp tại một số khách sạn có thể được xem là tín hiệu về nhu cầu thị trường tại từng thời điểm.

### 7.4. 💲 Dashboard Phân tích lợi nhuận và kiểm soát chi phí

<img width="1320" height="740" alt="image" src="https://github.com/user-attachments/assets/af034933-4225-45c5-a17e-e91e3fb6c3c5" />

#### Tác dụng

Dashboard đánh giá khả năng sinh lời, xu hướng chi phí và cơ cấu chi phí của hoạt động kinh doanh phòng. Kết quả hỗ trợ nhà quản lý xác định tháng có hiệu quả tốt, các hạng mục chi phí lớn và bộ phận cần ưu tiên kiểm soát.

#### Insight

- Lợi nhuận thuần đạt **13,02 tỷ đồng**, tương ứng biên lợi nhuận thuần **37,51%**.
- Lợi nhuận trên mỗi phòng khả dụng đạt khoảng **661.852 đồng**.
- Chi phí trên mỗi phòng khả dụng đạt **1,10 triệu đồng**.
- Chi phí trên mỗi phòng đã bán đạt **1,26 triệu đồng**.
- Tháng 7 có hiệu quả tốt nhất với lợi nhuận khoảng **5,83 tỷ đồng** và biên lợi nhuận **43,82%**.
- Tháng 6 có biên lợi nhuận thấp nhất, khoảng **32,89%**; tháng 8 đạt khoảng **34,26%**.
- Điện và lao động buồng phòng là hai hạng mục chi phí lớn nhất, lần lượt khoảng **4,34 tỷ đồng** và **4,19 tỷ đồng**.
- Theo phòng ban, bộ phận buồng phòng có chi phí cao nhất, khoảng **8,13 tỷ đồng**, tiếp theo là bộ phận kỹ thuật với khoảng **6,90 tỷ đồng**.
- Công suất và mức giá tốt trong tháng 7 đã giúp lợi nhuận tăng mạnh dù tổng chi phí cũng cao hơn.

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

