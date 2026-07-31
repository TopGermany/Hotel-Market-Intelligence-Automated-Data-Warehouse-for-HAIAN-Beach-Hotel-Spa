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
Các chiến lược dưới đây được đề xuất dựa trên insight từ bốn dashboard. Do dữ liệu nội bộ HAIAN là dữ liệu mô phỏng, các đề xuất được xem là định hướng thử nghiệm và cần được kiểm chứng bằng dữ liệu vận hành thực tế trước khi áp dụng.

---

### 8.1. Điều chỉnh giá theo mức cầu

Kết quả phân tích cho thấy tháng 7 có tỷ lệ lấp đầy, giá phòng trung bình và biên lợi nhuận cao nhất. Trong những giai đoạn có mức cầu tương tự, HAIAN nên:

- Hạn chế giảm giá đại trà.
- Ưu tiên bán phòng theo giá tiêu chuẩn hoặc cung cấp gói giá trị gia tăng.
- Áp dụng điều kiện lưu trú tối thiểu trong những ngày có nhu cầu cao.
- Theo dõi đồng thời tỷ lệ lấp đầy, ADR và ProfitPAR trước khi điều chỉnh giá.

Đối với các ngày có hiệu quả thấp như 02/06, 03/06, 09/06, 19/08 và 26/08, khách sạn có thể triển khai ưu đãi có mục tiêu như đặt sớm, lưu trú nhiều đêm hoặc gói phòng kèm ăn sáng. Không nên giảm giá cho toàn bộ giai đoạn vì có thể làm giảm lợi nhuận ở những ngày đã có nhu cầu tốt.

---

### 8.2. Tập trung vào loại phòng có đóng góp cao

Beachfront Oasis là loại phòng tạo ra lợi nhuận đóng góp cao nhất. Vì vậy, HAIAN nên:

- Duy trì định vị cao cấp cho loại phòng này.
- Xây dựng các gói phòng hướng biển kết hợp với spa, ăn sáng hoặc đưa đón.
- Ưu tiên giới thiệu Beachfront Oasis trong hoạt động truyền thông.
- Triển khai chương trình bán nâng hạng từ các loại phòng thấp hơn.
- Hạn chế áp dụng giảm giá sâu trong những ngày có nhu cầu cao.

Partial Sea View Oasis có doanh thu gần tương đương Beachfront Oasis nhưng lợi nhuận đóng góp thấp hơn. Khách sạn cần kiểm tra mức giảm giá, chi phí phục vụ và tỷ lệ hoa hồng của loại phòng này trước khi tiếp tục mở rộng doanh số.

---

### 8.3. Phát triển phân khúc khách hàng chủ lực

Nhóm khách nội địa đi nghỉ dưỡng và lưu trú từ 2–3 đêm là phân khúc đóng góp lớn nhất vào doanh thu và lợi nhuận. HAIAN có thể:

- Xây dựng gói nghỉ dưỡng cuối tuần 2 đêm hoặc 3 ngày 2 đêm.
- Kết hợp phòng với ăn sáng, spa hoặc dịch vụ đưa đón.
- Áp dụng chương trình ưu đãi cho khách quay lại.
- Cá nhân hóa nội dung truyền thông cho cặp đôi, gia đình và nhóm bạn.
- Khuyến khích khách kéo dài thời gian lưu trú bằng ưu đãi theo số đêm.

Đối với khách quốc tế, khách sạn có thể phát triển các gói lưu trú dài ngày, dịch vụ đưa đón và thông tin du lịch địa phương. Phân khúc khách đoàn và MICE có thể được khai thác vào những ngày công suất thấp nhằm bổ sung nhu cầu.

---

### 8.4. Tối ưu cơ cấu kênh bán

Agoda và Booking.com tạo ra sản lượng và doanh thu lớn nhưng có biên đóng góp thấp hơn website khách sạn và đại lý du lịch địa phương. HAIAN không nên loại bỏ các nền tảng OTA mà cần xác định vai trò phù hợp của từng kênh:

- Sử dụng OTA để tiếp cận khách hàng mới và duy trì sản lượng.
- Khuyến khích khách quay lại đặt phòng qua website hoặc kênh trực tiếp.
- Cung cấp quyền lợi riêng cho kênh trực tiếp như nhận phòng sớm, trả phòng muộn hoặc nâng hạng tùy tình trạng.
- Đánh giá kênh bán dựa trên lợi nhuận sau hoa hồng, không chỉ dựa trên doanh thu.
- Kiểm soát mức giảm giá, hoa hồng và chi phí khuyến mãi trên từng nền tảng.
- Theo dõi tỷ lệ chuyển đổi từ khách OTA thành khách hàng trực tiếp.

Cách tiếp cận này phù hợp với nguyên tắc quản trị doanh thu theo kênh, trong đó hiệu quả phân phối cần được đánh giá dựa trên phần đóng góp sau chi phí thay vì chỉ nhìn vào doanh thu phòng.

---

### 8.5. Kiểm soát các nhóm chi phí lớn

Kết quả dashboard cho thấy điện, lao động buồng phòng và chi phí kỹ thuật là những khoản chi lớn nhất. HAIAN nên:

- Theo dõi điện năng theo phòng khả dụng và phòng đã bán.
- Điều chỉnh lịch làm việc của bộ phận buồng phòng theo công suất dự kiến.
- Xây dựng định mức vật tư vệ sinh, đồ dùng phòng và giặt là.
- Lập kế hoạch bảo trì phòng ngừa để hạn chế sửa chữa đột xuất.
- Theo dõi chi phí bữa sáng trên mỗi khách lưu trú.
- So sánh chi phí thực tế với ngân sách theo tháng.
- Thiết lập cảnh báo khi chi phí vượt ngưỡng kiểm soát.

Tháng 7 có tổng chi phí cao nhưng biên lợi nhuận vẫn tốt nhất. Điều này cho thấy mục tiêu không phải cắt giảm toàn bộ chi phí mà là kiểm soát chi phí trong mối quan hệ với doanh thu, công suất và chất lượng dịch vụ.

---

### 8.6. Sử dụng giá đối thủ như tín hiệu thị trường

Dữ liệu đối thủ có thể hỗ trợ nhận diện mặt bằng giá và tín hiệu hết phòng. Tuy nhiên, dữ liệu HAIAN năm 2025 và dữ liệu đối thủ năm 2026 không cùng thời kỳ nên không được so sánh trực tiếp theo ngày.

Để sử dụng dữ liệu đối thủ hiệu quả hơn, HAIAN nên:

- Xây dựng tập đối thủ tương đồng về hạng sao, vị trí và loại hình lưu trú.
- Chỉ so sánh những loại phòng có đặc điểm tương đương.
- Thu thập dữ liệu HAIAN và đối thủ trong cùng thời kỳ.
- Theo dõi giá trung vị thay vì chỉ sử dụng giá trung bình.
- Phân biệt trạng thái hết phòng với trường hợp không thu thập được dữ liệu.
- Kết hợp giá đối thủ với công suất nội bộ, tốc độ đặt phòng và chi phí.
- Theo dõi biến động giá theo ngày nhận phòng và thời điểm thu thập.

Trong phạm vi hiện tại, dashboard đối thủ chỉ cung cấp **tín hiệu tham khảo về thị trường**, chưa thể xác định mức giá tối ưu cho HAIAN.

---

### 8.7. Chuyển từ quản lý doanh thu sang quản lý lợi nhuận

Các quyết định kinh doanh không nên chỉ dựa trên doanh thu hoặc tỷ lệ lấp đầy. HAIAN cần theo dõi đồng thời:

- Giá phòng trung bình.
- Tỷ lệ lấp đầy.
- Doanh thu trên mỗi phòng khả dụng.
- Lợi nhuận trên mỗi phòng khả dụng.
- Biên lợi nhuận đóng góp.
- Chi phí phân phối theo kênh.
- Chi phí trên mỗi phòng đã bán.
- Giá trị đóng góp của từng loại phòng và phân khúc khách hàng.

Cách tiếp cận này giúp hạn chế trường hợp doanh thu tăng nhưng lợi nhuận giảm do hoa hồng, khuyến mãi hoặc chi phí vận hành tăng. Mục tiêu cuối cùng là tối ưu lợi nhuận và giá trị khách hàng thay vì chỉ tối đa hóa số lượng phòng bán.

---

## 🎓 9. Mình đã học được gì qua dự án ? 
Thông qua việc tự tay xây dựng dự án Data Warehouse toàn diện này, tôi đã đúc kết được những kinh nghiệm vô giá không chỉ về mặt công cụ mà còn về tư duy giải quyết vấn đề:

* **Quản trị Pipeline với Apache Airflow:** Hiểu sâu về cách điều phối (Orchestration), lên lịch trình (DAGs) và giám sát trạng thái của các luồng dữ liệu (ETL pipeline). Điều này giúp tôi nhận ra tầm quan trọng của việc tự động hóa và khả năng theo dõi luồng dữ liệu một cách trực quan thay vì chạy script thủ công.
* **Tích hợp AI Agent vào Data Engineering:** Tiên phong trong việc sử dụng Google ADK (Gemini LLM) làm "trái tim" điều phối hệ thống. Tôi học được cách biến AI từ một công cụ chat trở thành một Agent có khả năng tự động phân tích tình huống và ra quyết định trình tự chạy các tác vụ cào dữ liệu một cách linh hoạt.
* **Tư duy Phân tích Hệ thống & Mô hình hóa (Data Modeling):** Học được cách bóc tách một bài toán kinh doanh "mù mờ" (Làm sao để tăng lợi nhuận khách sạn?) thành các thực thể dữ liệu rõ ràng. Từ đó, tôi biết cách thiết kế mô hình **ERD (Fact & Dimension)** chuẩn mực sao cho đáp ứng được mọi góc độ phân tích và vẽ Dashboard một cách mượt mà nhất.

---

Cảm ơn bạn đã quan tâm đến dự án của tôi! Nếu có cơ hội trao đổi hoặc hợp tác, vui lòng liên hệ với tôi qua Email: hoquocuong2005@gmail.com 

