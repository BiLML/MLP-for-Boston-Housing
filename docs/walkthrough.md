# Walkthrough: Restructure lab4.ipynb

## Tóm tắt
Đã restructure [lab4.ipynb](file:///d:/Machine%20Learning/m%C3%A1y%20h%E1%BB%8Dc/PR4/src/lab4.ipynb) để tuân thủ pipeline chống Data Leakage: **EDA tổng quan → Split → EDA chuyên sâu trên Train → Tiền xử lý cả 3 tập → Feature Scaling → Model**.

Backup gốc lưu tại [lab4_backup.ipynb](file:///d:/Machine%20Learning/m%C3%A1y%20h%E1%BB%8Dc/PR4/src/lab4_backup.ipynb).

## Pipeline mới (39 cells, tăng 2 so với 37 gốc)

| Cell | Section | Thay đổi |
|------|---------|----------|
| 0-1 | 1. Import | Giữ nguyên |
| 2-3 | 2. Load data + EDA tổng quan | Thêm `describe()` |
| 4-5 | 3. Define vars + **Split (70/15/15)** | **MỚI** — di chuyển split lên đây |
| 6-7 | 4. Missing/Duplicates — CHỈ TRAIN | Sửa `df` → `df_train` |
| 8-9 | 5. Outlier Analysis — CHỈ TRAIN | Sửa `df_clean` → `df_train` |
| 10-11 | 6. Tiền xử lý: Drop NA & Duplicates | **MỚI** — apply cả 3 tập |
| 12-13 | 6.1. Log Transform | **VIẾT LẠI** — auto-detect skewness từ Train |
| 14-15 | 7. Distributions — CHỈ TRAIN | Sửa `df_clean` → `df_train` |
| 16-17 | 8. Correlation & VIF — CHỈ TRAIN | Sửa `df_clean` → `df_train` |
| 18-19 | 9. Target Analysis — CHỈ TRAIN | Sửa `df_clean` → `df_train` |
| 20-21 | 10. Feature Scaling | Sửa: bỏ split, chỉ giữ scaling |
| 22-23 | 10.1. Before/after viz | Giữ nguyên logic |
| 24-38 | 11-18. Model → Train → Eval → Kết luận | Giữ nguyên logic, chỉ renumber |

## Thay đổi quan trọng

### 1. Log Transform viết lại hoàn toàn
- **Trước:** Hardcode 4 cột `['CRIM', 'ZN', 'B', 'LSTAT']`, transform trên toàn bộ dataset
- **Sau:** Tự động detect cột có `|skewness| > 1.0` từ **tập Train**, rồi apply cho cả 3 tập
- `max_val` cho reflect_log lấy từ **tập Train** (không rò rỉ từ val/test)

### 2. Split di chuyển lên bước 3
- **Trước:** Split ở bước 9 (sau toàn bộ EDA + preprocessing)
- **Sau:** Split ở bước 3 (ngay sau EDA tổng quan)

### 3. Variables downstream không đổi
Các biến `X_train`, `X_val`, `X_test`, `X_train_scaled`, `X_val_scaled`, `X_test_scaled`, `y_train`, `y_val`, `y_test`, `feature_cols`, `input_dim` vẫn được tạo ra đúng tên → phần model/training/eval **không cần sửa**.

## Rủi ro / Lưu ý
- **Kết quả số sẽ thay đổi** so với bản gốc vì split xảy ra trước khi dropNA, dẫn đến phân bổ mẫu khác.
- **Cần chạy lại toàn bộ notebook** từ đầu để đảm bảo không lỗi runtime.
- Nếu muốn rollback: copy `lab4_backup.ipynb` → `lab4.ipynb`.
