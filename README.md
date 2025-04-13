# Dự án Dự đoán Giá nhà bằng Thuật toán K-Nearest Neighbors (KNN)

## Mục lục

- [Giới thiệu](#giới-thiệu)
- [Cài đặt](#cài-đặt)
- [Sử dụng](#sử-dụng)
- [Cấu trúc thư mục](#cấu-trúc-thư-mục)
- [Tác giả](#tác-giả)

## Giới thiệu

Dự án này sử dụng thuật toán K-Nearest Neighbors (KNN) để dự đoán giá nhà dựa trên dữ liệu về các đặc điểm của nhà ở California. Dữ liệu được lấy từ tệp `housing_ca.csv`, chứa các thông tin như số phòng, diện tích, vị trí và giá nhà. Mục tiêu của dự án là áp dụng thuật toán KNN để xây dựng mô hình dự đoán giá nhà chính xác.&#8203;:contentReference[oaicite:2]{index=2}

## Cài đặt

Để chạy dự án này, bạn cần cài đặt các thư viện sau:

- `numpy`: Thư viện hỗ trợ tính toán số học.&#8203;:contentReference[oaicite:3]{index=3}
- `pandas`: Thư viện xử lý và phân tích dữ liệu.&#8203;:contentReference[oaicite:4]{index=4}
- `matplotlib`: Thư viện vẽ đồ thị.&#8203;:contentReference[oaicite:5]{index=5}
- `scikit-learn`: Thư viện học máy, cung cấp các công cụ cho thuật toán KNN.&#8203;:contentReference[oaicite:6]{index=6}

Bạn có thể cài đặt các thư viện này bằng cách sử dụng pip:

```bash
pip install numpy pandas matplotlib scikit-learn

## Cấu trúc thư mục
KNN/
│
├── Du doan gia nha.ipynb       # Tệp notebook chính chứa mã nguồn và hướng dẫn.
├── cali_map.png               # Hình ảnh bản đồ California .
├── housing_ca.csv             # Dữ liệu về các đặc điểm và giá nhà ở California.
└── main.ipynb                 # Tệp notebook phụ trợ .

Dự án được thực hiện bởi CuongDAol
Bạn có thể liên hệ qua:Buipg0801@gmail.com
