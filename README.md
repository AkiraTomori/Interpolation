# Đồ Án 1: Nội Suy và Hồi Quy Đa Thức

## Mô tả
Đồ án này thực hiện các phương pháp nội suy và hồi quy dữ liệu bao gồm:
- **Natural Cubic Spline** (Spline bậc ba tự nhiên)
- **Polynomial Regression** (Hồi quy đa thức)
- **Simple Moving Average** (Trung bình trượt đơn giản)

Dự án được áp dụng trên hai bài toán thực tế:
1. Phân tích nhiệt dung của dung dịch H₂SO₄ theo nồng độ
2. Phân tích xu hướng dữ liệu COVID-19 tại Việt Nam (2020-2022)

## Cấu trúc thư mục
```
.
├── 23127379.ipynb       # Notebook chính chứa code và kết quả
├── Test.py              # File test các thư viện cần thiết
├── data.csv             # Dữ liệu COVID-19
└── README.md            # File hướng dẫn này
```

## Yêu cầu hệ thống

### Thư viện cần thiết
- Python 3.x
- NumPy
- Pandas
- Matplotlib
- scikit-learn

### Cài đặt
```bash
pip install numpy pandas matplotlib scikit-learn
```

## Nội dung chi tiết

### 1. Natural Cubic Spline
Lớp `NaturalCubicSpline` thực hiện nội suy dữ liệu bằng phương pháp Spline bậc ba tự nhiên.

**Đặc điểm:**
- Tạo đường cong trơn qua tất cả các điểm dữ liệu
- Tính toán các hệ số a, b, c, d cho mỗi đoạn spline
- Đảm bảo tính liên tục của đạo hàm bậc 1 và bậc 2

**Phương thức chính:**
- `compute_coefficients()`: Tính toán các hệ số của spline
- `interpolate(x)`: Nội suy giá trị tại điểm x

### 2. Polynomial Regression
Lớp `PolynominalRegression` thực hiện hồi quy đa thức với bậc tùy chỉnh.

**Đặc điểm:**
- Chuẩn hóa dữ liệu theo phương pháp min-max
- Sử dụng phương pháp bình phương tối thiểu (least squares)
- Có thể điều chỉnh bậc đa thức để tránh overfitting

**Phương thức chính:**
- `min_max_normalize(X)`: Chuẩn hóa dữ liệu đầu vào
- `compute_coefficients()`: Tính toán hệ số hồi quy
- `predict(x)`: Dự đoán giá trị tại điểm x

### 3. Moving Average
Lớp `MovingAverage` thực hiện làm mượt dữ liệu bằng trung bình trượt đơn giản.

**Đặc điểm:**
- Sử dụng cửa sổ trượt với kích thước lẻ
- Tính trung bình của các điểm gần nhất
- Giúp loại bỏ nhiễu và làm mượt đường cong

**Phương thức chính:**
- `predict(x)`: Dự đoán giá trị tại điểm x
- `smooth(X_new)`: Làm mượt một danh sách các giá trị

## Bài toán ứng dụng

### Bài 1: Nhiệt dung của dung dịch H₂SO₄
**Mục tiêu:** Phân tích mối quan hệ giữa nồng độ axit sulfuric và nhiệt dung riêng.

**Dữ liệu:**
- 38 điểm đo từ 0.34% đến 100% nồng độ H₂SO₄
- Nhiệt dung riêng (Cp) tương ứng tính bằng kJ/kg·K

**Phương pháp:**
- Natural Cubic Spline cho nội suy chính xác
- Polynomial Regression (bậc 10) để so sánh

**Kết quả:**
- So sánh MAE và RMSE giữa hai phương pháp
- Biểu đồ trực quan hóa sự khác biệt

### Bài 2: Phân tích COVID-19 tại Việt Nam
**Mục tiêu:** Phân tích xu hướng số ca nhiễm COVID-19 từ 2020-2022.

**Dữ liệu:**
- Nguồn: Our World in Data
- Thời gian: 01/01/2020 - 02/01/2022
- Số ca nhiễm mới hàng ngày

**Phương pháp:**
- Natural Cubic Spline cho dữ liệu có ca nhiễm > 0
- Simple Moving Average (window_size=5) để so sánh
- Lấy mẫu mỗi 7 ngày để phân tích xu hướng tuần

**Kết quả:**
- Trực quan hóa xu hướng đại dịch
- So sánh hiệu suất giữa Spline và Moving Average
- Đánh giá MAE và RMSE

## Hướng dẫn sử dụng

### 1. Kiểm tra môi trường
```bash
python Test.py
```

### 2. Chạy notebook
Mở file `23127379.ipynb` trong Jupyter Notebook hoặc VS Code và chạy từng cell theo thứ tự.

### 3. Cấu trúc notebook
1. Import thư viện
2. Định nghĩa các lớp (NaturalCubicSpline, PolynominalRegression, MovingAverage)
3. Hàm vẽ biểu đồ
4. Bài 1: Nhiệt dung H₂SO₄
5. Bài 2: Phân tích COVID-19

## Đánh giá hiệu suất

Dự án sử dụng các metrics sau để đánh giá:
- **MAE (Mean Absolute Error):** Sai số tuyệt đối trung bình
- **RMSE (Root Mean Squared Error):** Căn bậc hai của sai số bình phương trung bình

## Kết luận

### Nhận xét về Spline bậc ba:
- ✅ Khớp chính xác với dữ liệu gốc
- ✅ Tạo đường cong trơn tru giữa các điểm
- ✅ Không bị overfitting như hồi quy đa thức bậc cao
- ✅ Phù hợp cho dữ liệu có biến động lớn

### So sánh với Polynomial Regression:
- Hồi quy đa thức có thể bị dao động mạnh ở biên
- Spline cho kết quả ổn định và đáng tin cậy hơn
- Spline phù hợp hơn cho dữ liệu không có dạng đa thức đơn giản

### So sánh với Moving Average:
- Moving Average làm mượt tốt nhưng không khớp chính xác
- Spline vừa mượt vừa khớp với dữ liệu
- Moving Average phù hợp cho dự báo xu hướng tổng quát

## Tác giả
**MSSV:** 23127379
**Sinh viên thực hiện:** Thái Minh Huy

## Tham khảo
- Our World in Data - COVID-19 Dataset
- Numerical Methods for Engineers
- scikit-learn Documentation

## License
Dự án này được tạo cho mục đích học tập tại Đại học Khoa học Tự nhiên TP.HCM (VNU-HCMUS).
