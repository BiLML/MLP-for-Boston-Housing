# PR4 - Dự đoán Giá nhà Boston (Boston Housing Price Prediction)

## Tổng quan Dự án
Dự án này là Bài thực hành (Lab 4) nhằm giải quyết bài toán Hồi quy (Regression) dự đoán giá trị trung bình của những ngôi nhà ở Boston (biến `MEDV`). 
Dự án tập trung vào việc áp dụng các kỹ thuật Khoa học dữ liệu từ Tiền xử lý (EDA, Xử lý Outliers bằng Biến đổi Logarit, Chuẩn hóa Z-Score), cho đến việc xây dựng và so sánh hiệu suất giữa mô hình **Học Sâu (Deep Learning - Mạng MLP Pytorch)** với các mô hình **Học Máy Cổ điển (Linear Regression, Decision Tree, Random Forest)**.

## Cấu trúc Thư mục

```text
PR4/
├── README.md                       # Tài liệu giới thiệu dự án (File bạn đang đọc)
├── data/                           # Dữ liệu dự án
│   ├── features/                   # Lưu trữ ma trận features (Train/Val/Test đã chuẩn hóa)
│   ├── processed/                  # Dữ liệu sạch sau khi tiền xử lý và xử lý nhiễu
│   └── raw/                        # Dữ liệu thô ban đầu (Boston-house-price-data.csv)
├── docs/                           # Thư mục chứa tài liệu tham khảo và kiến thức
│   ├── flowcharts/                 # Các sơ đồ Pipeline và Workflow (Mermaid diagrams)
│   └── lab4_explanation.md         # Tài liệu phân tích chuyên sâu về quy trình và biểu đồ
├── models/                         # Nơi lưu trữ trọng số mô hình tốt nhất (.pth, .pkl)
├── runs/                           # Nơi lưu trữ đồ thị huấn luyện TensorBoard (Sẽ sinh ra khi chạy mã)
└── src/                            # Thư mục mã nguồn chính
    └── lab4.ipynb                  # Tệp Jupyter Notebook chứa toàn bộ pipeline thực hành
```

## Yêu cầu Hệ thống
Dự án yêu cầu Python 3.8+ và các thư viện cốt lõi sau:
- `pandas` & `numpy` (Tính toán và xử lý dữ liệu)
- `matplotlib` & `seaborn` (Trực quan hóa biểu đồ)
- `scikit-learn` (Tiền xử lý và Xây dựng mô hình ML truyền thống)
- `torch` & `torchvision` (Xây dựng mạng Nơ-ron Deep Learning)
- `tensorboard` (Theo dõi Loss Real-time)

## Hướng dẫn Khởi chạy
1. Mở Terminal tại thư mục gốc của dự án (`PR4`).
2. (Tùy chọn) Khởi tạo và kích hoạt môi trường ảo:
   ```bash
   python -m venv .venv
   .venv\Scripts\activate
   ```
3. Cài đặt các thư viện cần thiết bằng lệnh:
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn torch torchvision tensorboard notebook
   ```
4. Khởi chạy giao diện Jupyter Notebook:
   ```bash
   jupyter notebook
   ```
5. Điều hướng tới `src/lab4.ipynb` trên trình duyệt và chọn `Run All` để thực thi toàn bộ luồng công việc từ trên xuống dưới.
6. Để xem biểu đồ huấn luyện Real-time, mở một Terminal khác và gõ:
   ```bash
   tensorboard --logdir src/runs
   ```

## Tài liệu Phân tích Chuyên sâu
Để hiểu rõ cặn kẽ ý nghĩa của từng biểu đồ, lý do chọn phương pháp xử lý ngoại lai (Log Transform), cũng như tại sao thiết kế MLP với cấu trúc 13->64->32->1, vui lòng tham khảo tài liệu phân tích chi tiết tại: [lab4_explanation.md](lab4_explanation.md).
