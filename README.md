## HCMUS-AppliedMath-Project1
Color compression using K-means Clustering

## Đồ án 1 - Color Compression <a class="anchor" id="c2"></a>
### Nội dung đồ án <a class="anchor" id="c21"></a>
#### Giới thiệu
Một bức ảnh có thể lưu trữ dưới ma trận của các điểm ảnh. Có nhiều loại ảnh được sử dụng trong thực tế, ví dụ: ảnh xám, ảnh màu,...

Đối với ảnh xám, một điểm ảnh sẽ là được biểu diễn bằng giá trị không âm.

Ví dụ ta có thể dùng ma trận này:

```math
$$
\begin{bmatrix}
255 & 0 & 0  & 0  & 255 \\
255 & 0 & 255 & 0 & 255\\
255 & 0 & 255 & 0 & 255\\
255 & 0 & 255 & 0 & 255\\
255 & 0 & 0  & 0  & 255
\end{bmatrix}$$
$$
```
$$
có thể biểu diễn cho ảnh xám có nội dung như sau:
```
import matplotlib.pyplot as plt
plt.imshow(np.array([[255, 0, 0, 0, 255],
                     [255, 0, 255, 0, 255],
                     [255, 0, 255, 0, 255],
                     [255, 0, 255, 0, 255],
                     [255, 0, 0, 0, 255]]), cmap='gray', vmin=0, vmax=255);

```
<p align="center">
  <img src="https://github.com/KitoKotowa/HCMUS-AppliedMath-Project1/assets/110214271/5ba8e22f-5296-41ae-b85b-2372a4327716" />
</p>

Ảnh màu được sử dụng phổ biến là ảnh RGB, trong đó, mỗi điểm ảnh sẽ lưu trữ 3 thông tin kênh màu (mỗi kênh màu 1 byte) là: R (red - đỏ), G (green - xanh lá), B (blue - xanh dương). Ta có thể sử dụng ma trận:
```
                    [[[255, 255, 255], [255, 0, 0], [255, 0, 0], [255, 0, 0], [255, 255, 255]],
                     [[255, 255, 255], [255, 0, 0], [255, 255, 255], [255, 0, 0], [255, 255, 255]],
                     [[255, 255, 255], [255, 0, 0], [255, 255, 255], [255, 0, 0], [255, 255, 255]],
                     [[255, 255, 255], [255, 0, 0], [255, 255, 255], [255, 0, 0], [255, 255, 255]],
                     [[255, 255, 255], [255, 0, 0], [255, 0, 0], [255, 0, 0], [255, 255, 255]]]
```
để biểu diễn cho ảnh màu có nội dung sau:
```
plt.imshow(np.array([[[255, 255, 255], [255, 0, 0], [255, 0, 0], [255, 0, 0], [255, 255, 255]],
                     [[255, 255, 255], [255, 0, 0], [255, 255, 255], [255, 0, 0], [255, 255, 255]],
                     [[255, 255, 255], [255, 0, 0], [255, 255, 255], [255, 0, 0], [255, 255, 255]],
                     [[255, 255, 255], [255, 0, 0], [255, 255, 255], [255, 0, 0], [255, 255, 255]],
                     [[255, 255, 255], [255, 0, 0], [255, 0, 0], [255, 0, 0], [255, 255, 255]]]));
```
<p align="center">
  <img src="https://github.com/KitoKotowa/HCMUS-AppliedMath-Project1/assets/110214271/d2716869-99af-441a-a016-55d037017300" />
</p>

Như vậy, số màu trong ảnh RGB có thể là $256^3 \approx 1.7 \times 10^7$. Với số lượng màu khá lớn, khi lưu trữ ảnh có thể sẽ tốn chi phí lưu trữ. Do đó bài toán đặt ra là giảm số lượng màu để biểu diễn ảnh sao cho nội dung ảnh được bảo toàn nhất có thể.

Cho ảnh như sau:

![img](https://i.ibb.co/PZgqGDh/project01-new.png)

Trong ví dụ trên, số lượng màu cho ảnh ban đầu là 81705 màu. Sau khi giảm số lượng màu xuống còn 7, ảnh không còn được chi tiết nhưng cơ bản vẫn bảo toàn nội dung của ảnh ban đầu.

Để thực hiện giảm số lượng màu, ta cần tìm ra các đại diện có thể thay thế cho một nhóm màu. Cụ thể trong trường hợp ảnh RGB, ta cần thực hiện gom nhóm các pixel $(\mathbb{R}^3)$ và chọn ra đại diện cho từng nhóm. Như vậy, bài toán trên trở thành gom nhóm các vec-tơ.
#### Yêu cầu
Trong đồ án này, bạn được yêu cầu cài đặt chương trình giảm số lượng màu cho ảnh sử dụng thuật toán [K-Means](https://en.wikipedia.org/wiki/K-means_clustering).

Các thư viện được phép sử dụng là: `NumPy` (tính toán ma trận), `PIL` (đọc, ghi ảnh), `matplotlib` (hiển thị ảnh).

