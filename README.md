# Dự án K-means Clustering trên Dữ liệu CA Housing

## Mục lục

- [Giới thiệu](#giới-thiệu)
- [Cài đặt](#cài-đặt)
- [Sử dụng](#sử-dụng)
- [Cấu trúc thư mục](#cấu-trúc-thư-mục)
- [Tác giả](#tác-giả)

## Giới thiệu

Dự án này sử dụng thuật toán K-means để phân cụm dữ liệu CA Housing, bao gồm các đặc trưng như `longitude`, `latitude` và `housing_median_age`. Mục tiêu của dự án là khám phá dữ liệu và rút ra thông tin hữu ích từ các cụm được phân tích. Dữ liệu được sử dụng trong dự án là tệp `housing_ca.csv`, chứa các thông tin về các khu vực tại California, bao gồm tọa độ và thông tin về giá nhà và độ tuổi trung bình của nhà ở.

## Cài đặt

Để chạy dự án này, bạn cần cài đặt các thư viện sau:

- `pandas`: Thư viện xử lý dữ liệu.
- `numpy`: Thư viện tính toán khoa học.
- `matplotlib`: Thư viện vẽ đồ thị.
- `scikit-learn`: Thư viện học máy, hỗ trợ thuật toán K-means.

Bạn có thể cài đặt các thư viện này bằng cách sử dụng pip:

```bash
pip install pandas numpy matplotlib scikit-learn

K-means-Clustering-CA-Housing/
│
├── housing_ca.csv            # Dữ liệu về các đặc trưng và giá trị nhà ở California.
├── dư doan gia nha.ipynb      # Mã nguồn Python thực hiện phân cụm và trực quan hóa.
├── README.md                  # Tệp này.
└──main.ipynb                  #

