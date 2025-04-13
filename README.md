# Dự án K-means Clustering trên Dữ liệu CA Housing

## Mục lục

- [Giới thiệu](#giới-thiệu)
- [Cài đặt](#cài-đặt)
- [Cấu trúc thư mục](#cấu-trúc-thư-mục)
- [Phân tích dữ liệu](#phân-tích-dữ-liệu)
- [Kết quả phân cụm K-means](#kết-quả-phân-cụm-k-means)
- [Sử dụng](#sử-dụng)
-  [Tác giả](#tác-giả)
## Giới thiệu

Dự án này sử dụng thuật toán K-means để phân cụm dữ liệu CA Housing, bao gồm các đặc trưng như `longitude`, `latitude`, `housing_median_age`, `total_rooms`, `total_bedrooms`, `population`, `households`, `median_income`, `median_house_value`, và `ocean_proximity`. Mục tiêu của dự án là khám phá dữ liệu và rút ra thông tin hữu ích từ các cụm được phân tích, đồng thời xây dựng mô hình dự đoán giá nhà, thu nhập trung vị và tuổi trung vị của các ngôi nhà.

## Cài đặt

Để chạy dự án này, bạn cần cài đặt các thư viện sau:

- `pandas`: Thư viện xử lý dữ liệu.
- `numpy`: Thư viện tính toán khoa học.
- `matplotlib`: Thư viện vẽ đồ thị.
- `seaborn`: Thư viện vẽ đồ thị nâng cao.
- `scikit-learn`: Thư viện học máy, hỗ trợ thuật toán K-means.
## Phân tích dữ liệu
Các đặc trưng trong bộ dữ liệu:
longitude: Kinh độ của khu vực.

```
latitude: Vĩ độ của khu vực.

housing_median_age: Tuổi trung vị của các ngôi nhà trong một block.

total_rooms: Tổng số phòng trong một block.

total_bedrooms: Tổng số phòng ngủ trong một block.

population: Tổng dân số trong một block.

households: Số hộ gia đình trong một block.

median_income: Thu nhập trung vị của các hộ gia đình trong một block (đơn vị là 10 nghìn USD).

median_house_value: Giá nhà trung vị trong một block.

ocean_proximity: Khoảng cách tới biển (hạng mục).
```
Quan sát dữ liệu:
Dữ liệu đầy đủ: Hầu hết các cột dữ liệu đều có giá trị đầy đủ, trừ cột total_bedrooms có 207 giá trị bị khuyết. Bạn có thể điền giá trị bị thiếu này bằng cách sử dụng giá trị trung bình, trung vị hoặc dùng mô hình KNN để dự đoán giá trị thiếu.

Dữ liệu không có giá trị trùng lặp: Các giá trị trong dữ liệu không bị trùng lặp.

Mức độ phân phối dữ liệu: Một số cột như total_rooms, total_bedrooms, population, households có sự phân phối lệch phải, với nhiều giá trị tập trung ở phía thấp và ít giá trị ở phía cao.

Kết quả phân cụm K-means
Phương pháp Elbow
Dựa trên phương pháp Elbow, chúng ta xác định rằng số cụm tối ưu là 5 (K=5), vì sau đó độ thay đổi của WCSS (within-cluster sum of squares) không còn rõ ràng nữa.
```bash
from sklearn.cluster import KMeans
wcss_list=[]
# thu với k=1 đến 10
for i in range(1,11):
    kmeans = KMeans(n_clusters=i, init="k-means++", random_state=42)
    kmeans.fit(x_scaler)
    wcss_list.append(kmeans.inertia_)
plt.plot(range(1,11), wcss_list)
plt.title("The Elbow Method Graph")
plt.xlabel("Number of Clusters (k)")
plt.ylabel("WCSS")
plt.show()
```
```bash
# Trực quan hóa kết quả phân cụm
Sau khi phân cụm, chúng ta có thể trực quan hóa kết quả với các cụm được phân biệt bằng màu sắc khác nhau:
```bash
plt.figure(figsize=(12,8), dpi=80)
colors = sns.color_palette("husl", 5)
for i in range(5):
    plt.scatter(x[y_predict == i, 0], x[y_predict == i, 1], s=15, c=colors[i], label=f'Cluster {i+1}')
    
kmeans.cluster_centers_ = sc.inverse_transform(kmeans.cluster_centers_)
plt.scatter(kmeans.cluster_centers_[:,0], kmeans.cluster_centers_[:,1], s=100, c="yellow", label="Centroids")
plt.title("Clusters of House Pricing Data")
plt.xlabel("Median Income")
plt.ylabel("Population")
plt.legend()
plt.show()
```
Nhận xét về các cụm:
Cụm 1: Thu nhập thấp, mật độ dân số thấp.

Cụm 2: Thu nhập trung bình, mật độ dân số thấp.

Cụm 3: Thu nhập thấp và trung bình, mật độ dân số trung bình.

Cụm 4: Thu nhập thấp và trung bình, mật độ dân số cao.

Cụm 5: Thu nhập cao, mật độ dân số thấp.

# Trực quan hóa các cụm trên bản đồ:
Mỗi cụm được phân bố trên bản đồ với kích thước điểm dữ liệu đại diện cho số dân (population) và màu sắc thể hiện giá trị nhà (median_house_value).
```bash
df["cluster"] = y_predict + 1
tmp_df = df.sort_values(by="cluster")
plt.figure(figsize=(30,8), dpi=80)
california_img = plt.imread("cali_map.png")
colors = sns.color_palette("husl", 5)

for i in range(1, 6):
    plt.subplot(1, 5, i)
    sns.scatterplot(data=tmp_df[tmp_df["cluster"] == i], x='longitude', y='latitude', color=colors[i-1], s=10, linewidth=0)
    plt.title(f'Cluster {i}')
    plt.imshow(california_img, extent=[-126.25, -113.85, 32.25, 42.15], alpha=1)
```
Dữ liệu phân cụm giúp chúng ta nhận diện các khu vực có đặc điểm thu nhập và mật độ dân cư tương tự nhau, từ đó có thể đưa ra các chiến lược phù hợp trong nghiên cứu về giá nhà và phân tích thị trường.


Bạn có thể cài đặt các thư viện này bằng cách sử dụng pip:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn
K-means-Clustering-CA-Housing/
│
├── housing_ca.csv            # Dữ liệu về các đặc trưng và giá trị nhà ở California.
├── du doan gia nha.ipynb      # Mã nguồn Python thực hiện phân cụm và trực quan hóa.
├── README.md                  # Tệp này.
└──main.ipynb                  # mã phụ
```

### Các điểm nổi bật trong tệp README:

- Các đoạn mã được cải thiện, dễ đọc và có định dạng rõ ràng.
- Các bước thực hiện và kết quả phân tích đã được mô tả chi tiết.
- Phần **Kết quả phân cụm K-means** đã được trình bày chi tiết, bao gồm phương pháp Elbow, các kết quả phân cụm và trực quan hóa kết quả.
## Tác giả 
Dự án này được thực hiện bởi [CuongDAol](https://github.com/CuongDAol).

- **Email**: buipg0801@gmail.com
Cảm ơn bạn đã xem qua dự án này! Nếu bạn có bất kỳ câu hỏi nào hoặc muốn hợp tác, đừng ngần ngại liên hệ với tôi.
