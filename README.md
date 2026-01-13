# Phân Tích và Dự Báo Lượng Mưa Tại Huế (Dữ liệu Lịch sử & Sự kiện 2025)

### 1. Thành viên nhóm 20

| Thành viên           | MSSV     |
| :-----------------   | :--------|
| Phạm Hương Trà       | 23120177 |
| Hàn Vũ Phương Uyên   | 23120106 |
| Trần Minh Trọng      | 23120100 |
| Bạch Trương Tấn Phát | 23120316 |

---

### 2. Overview

Dự án này tập trung vào việc thu thập, xử lý và phân tích dữ liệu thời tiết tại khu vực Huế, Việt Nam. Động lực chính của dự án xuất phát từ sự kiện mưa lũ lịch sử vào cuối tháng 10 và đầu tháng 11 năm 2025, gây thiệt hại nghiêm trọng.

Mục tiêu của dự án là tìm hiểu các quy luật khí tượng, các yếu tố tác động đến lượng mưa và xây dựng mô hình dự báo để hỗ trợ công tác cảnh báo sớm.

---

### 3. Tổng quan Dataset
Dữ liệu thời tiết lịch sử tại Huế, được thu thập từ **Meteostat API**. Các đặc trưng gồm:
- latitude, longitude: cặp (vĩ độ, kinh độ)
- datetime: thời điểm dữ liệu được ghi lại theo giờ trong ngày.
- temperature_2m (độ C): nhiệt độ không khí được đo ở độ cao 2m so với mặt đất, trung bình theo giờ trong ngày.
- dewpoint_2m (độ C): nhiệt độ điểm sương, nhiệt độ hơi nước cần lạnh đi để đạt 100% độ ẩm, từ đó bắt đầu ngưng tụ.
- relativehumidity_2m (%): độ ẩm tương đối (lương hơi nước trong không khí / lượng tối đa không khí ở nhiệt độ đó có thể giữ).
- precipitation (mm): lượng mưa.
- windspeed_10m (km/h): tốc độ gió ở độ cao 10m so với mặt đất.
- winddirection_10m (độ): hướng gió.
- pressure_msl (hPa): áp suất tại mực nước biển trung bình, là chuẩn để phân biệt áp cao/thấp.

- Quy ước mùa:
  - Mùa khô: Tháng 12-4.
  - Mùa mưa: Tháng 5-11.

---

### 4. Tổng quan dự án
#### 1. Data collection
Notebook: `01_data_collection.ipynb`
- Trình bày lý do chọn đề tài.
- Mô tả phương pháp thu thập dữ liệu.
- Phân tích các vấn đề trong quá trình thu thập:
  - Thiếu dữ liêu.
  - Nhiễu.
  - Không đồng nhất theo thời gian.
 
#### 2. Data preprocessing
Notebook: `02_data_preprocessing.ipynb`
- Làm sạch dữ liệu:
  - Xử lý missing values.
  - Chuẩn hóa định dạng thời gian.
- Tạo các đặc trưng mới:
  - Tháng.
  - Giờ.
  - Mùa (Mưa/Khô).
- Hoàn thiện dataset cho quá trình phân tích và mô hình hóa.

#### 3. Exploratory Data Analysis (EDA)
**Q1. Tác động của các yếu tố thời tiết đến lượng mưa**
Notebook: `03_Q1_data_analysis.ipynb`
- Phân tích mối quan hệ giữa:
  - Nhiệt độ.
  - Độ ẩm.
  - Áp suất.
  - Gió.
- Xác định:
  - Yếu tố ảnh hưởng mạnh đến mưa.
  - Các ngưỡng giá trị dễ dẫn đến mưa.
 
**Q2. Đặc điểm cường độ, thời gian và tần suất mưa**
Notebook: `03_Q2_data_analysis.ipynb`
- Phân tích:
  - Cường độ mưa.
  - Thời gian kéo dài của các trận mưa.
  - Tần suất xuất hiện.
- Phân biệt cường độ mưa (nhẹ/vừa/lớn).

**Q3. Quy luật mưa theo thời gian**
Notebook: `03_Q3_data_analysis.ipynb`
- Phân tích lượng mưa theo thời gian (tháng/giờ trong ngày).
- So sánh đặc trưng thời tiết giữa hai mùa.
- Rút ra quy luật mưa theo chu kỳ thời gian.

**Q4. Đặc điểm của các trận mưa lớn**
Notebook: `03_Q4_data_analysis.ipynb`
- So sánh các đặc trưng thời tiết trước-trong-sau khi mưa lớn.
- So sánh mưa lớn và mưa thường.
- Chỉ ra các yếu tố thay đổi rõ rệt nhất.
- Đánh giá khả năng mưa lớn từ dữ liệu.

#### 4. Modeling
Notebook: `04_modeling.ipynb`
- Tạo feature cho mô hình.
- Chia tập train/test.
- Huấn luyện mô hình dự đoán lượng mưa.
- Đánh giá hiệu năng mô hình.
- Liên hệ kết quả mô hình với insight từ EDA.

---

### 5. Cấu trúc dự án

```
  ├── data/ 
  |   ├── raw/
  |   |    └── weather_raw.csv # Dữ liệu thô
  |   └── processed/
  |   |    ├── weather_processed.csv # Dữ liệu đã qua xử lý
  |   |    ├── test_data.csv # Tập test
  |   |    └── train_data.csv # Tập train
  ├── 01_data_collection.ipynb # Quá trình thu thập dữ liệu
  ├── 02_data_preprocessing.ipynb # Qua trình tiền xử lý
  ├── 03_data_analysis/
  |   ├── 03_Q1_data_analysis.ipynb # Các yếu tố thời tiết (nhiệt độ, độ ẩm, gió, áp suất…) có tác động và mức độ tương quan như thế nào đến lượng mưa
  |   ├── 03_Q2_data_analysis.ipynb # Cường độ, thời gian kéo dài và tần suất của các trận mưa có đặc điểm gì?
  |   ├── 03_Q3_data_analysis.ipynb # Sự thay đổi của lượng mưa và các yếu tố thời tiết theo thời gian cho thấy quy luật nào về mưa ở Huế?
  |   └── 03_Q4_data_analysis.ipynb # Trong và trước các trận mưa lịch sử tháng 10–11/2025 vừa rồi ở Huế, những biến khí tượng nào thể hiện sự thay đổi rõ rệt nhất, có gì khác biệt so với các trận còn lại không?
  └── 04_modeling.ipynb # Xây dựng mô hình học máy (Machine Learning) để dự đoán khả năng mưa hoặc lượng mưa dựa trên các đặc trưng đã xử lý.
```

---

### 6. Yêu cầu hệ thống
Để chạy được các notebook, hệ thống cần có các thư viện Python sau:
```bash
pip install pandas numpy matplotlib seaborn plotly windrose scikit-learn
```

---

### 7. Kết luận của dự án1. Dữ liệu thời tiết có cấu trúc theo chu kỳ rõ ràng
- Lượng mưa không phân bố ngẫu nhiên, mà phụ thuộc mạnh vào:
  - Tháng trong năm.
  - Mùa.
  - Giờ trong ngày.
- Các pattern này xuất hiện nhất quán từ EDA đến Modeling.

2. Mưa không do một yếu tố đơn lẻ, mà là kết quả của tổ hợp điều kiện
- Không tồn tại một feature đơn lẻ đủ mạnh quyết định mưa.
- Mưa (đặc biệt là mưa lớn) xảy ra khi:
  - Độ ẩm cao.
  - Áp suất phù hợp với mùa.
  - Nhiệt độ và gió tạo điều kiện tối ưu.
- Các yếu tố này tác động đồng thời chứ không độc lập với nhau.

3. Áp suất là yếu tố "điều kiện", không phải yếu tố độc lập
- Áp suất có ý nghĩa khi đặt trong bối cảnh thời gian: Có giá trị phân biệt trong mùa khô nhưng mất ở mùa mưa.
- Một số tổ hợp tháng-áp suất không xuất hiện trong dữ liệu, phản ánh đúng quy luật khí hậu thực tế.

4. Mưa lớn có đặc trưng khi tượng riêng, khác mưa thông thường
- Mưa lớn thường xảy ra trong một số khung giờ nhất định, đi kèm sự thay đổi rõ rệt của nhiều yếu tố thời tiết.
- Mưa lớn không đơn giản là "mưa nhiều hơn", nó là một **trạng thái khác**.

5. Dữ liệu phản ánh đúng quy luật tự nhiên
- Những feature không bao giờ xuất hiện cùng nhau không phải là lỗi, mà là kiến thức khí hậu được mã hóa trong data.

6. EDA giúp giải thích và định hướng mô hình Machine Learning
- Các insight từ EDA giải thích vì sao mô hình split theo thời gian và vì sao một số feature ít được chọn.

### 8. Hướng nghiên cứu và mở rộng tiếp theo
- Bổ sung thêm dữ liệu các năm để tăng tính tổng quát.
- Mở rộng phạm vi tọa độ thu thập (latitude, longitude) để nghiên cứu sự khác biệt đến từ địa hình, khu vực.
