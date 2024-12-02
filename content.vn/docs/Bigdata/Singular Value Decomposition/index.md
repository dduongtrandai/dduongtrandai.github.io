---
title: "Singular Value Decomposition"
---
SVD (Singular Value Decomposition) là một thuật toán phân tích toán học quan trọng trong lĩnh vực đại số tuyến tính và phân tích dữ liệu. SVD thường được sử dụng để giảm chiều dữ liệu, khai thác các đặc trưng tiềm ẩn của ma trận, và là nền tảng của nhiều ứng dụng trong học máy, xử lý ảnh, và khai phá dữ liệu. Dưới đây là chi tiết về SVD và cách nó hoạt động:

### Khái niệm cơ bản của SVD

SVD là một cách phân tích ma trận thành ba thành phần khác nhau, tương tự như cách ta phân tích một số thành tích của các số khác. Cụ thể, với một ma trận \( A \) kích thước \( m \times n \), SVD phân tích nó thành ba ma trận:

\[
A = U \Sigma V^T
\]

Trong đó:

- **\( A \)**: Ma trận ban đầu kích thước \( m \times n \).
- **\( U \)**: Ma trận trực giao kích thước \( m \times m \). Các cột của \( U \) là các **vector riêng** của \( A A^T \).
- **\( \Sigma \)**: Ma trận đường chéo kích thước \( m \times n \), chứa các giá trị đặc trưng gọi là **singular values** (giá trị kỳ dị) của ma trận \( A \). Các giá trị này sắp xếp theo thứ tự giảm dần và là căn bậc hai của các giá trị riêng của ma trận \( A A^T \) hoặc \( A^T A \).
- **\( V^T \)**: Ma trận chuyển vị của \( V \), kích thước \( n \times n \). Ma trận \( V \) có các cột là các **vector riêng** của \( A^T A \).

### Ý nghĩa của SVD

- **Ma trận \( U \)**: Các vector cột của \( U \) tạo thành một cơ sở trực chuẩn trong không gian của các hàng của \( A \), được gọi là **cơ sở trái**.
- **Ma trận \( V \)**: Các vector cột của \( V \) tạo thành một cơ sở trực chuẩn trong không gian của các cột của \( A \), được gọi là **cơ sở phải**.
- **Ma trận \( \Sigma \)**: Ma trận đường chéo chứa các giá trị kỳ dị (\( \sigma_1, \sigma_2, \ldots, \sigma_r \)), là các giá trị không âm và sắp xếp theo thứ tự giảm dần. Các giá trị này thể hiện mức độ quan trọng của các thành phần chính của dữ liệu.

### Cách SVD hoạt động

1. **Tính giá trị kỳ dị**: Bước đầu tiên trong SVD là tính toán các giá trị kỳ dị của ma trận \( A \). Các giá trị kỳ dị này là căn bậc hai của các giá trị riêng của \( A^T A \).
2. **Tính vector riêng**:
   - Tính các vector riêng của ma trận \( A A^T \) để tạo thành ma trận \( U \).
   - Tính các vector riêng của ma trận \( A^T A \) để tạo thành ma trận \( V \).
3. **Xây dựng ma trận \( U, \Sigma, V^T \)**: Sử dụng các giá trị kỳ dị và vector riêng để xây dựng các ma trận \( U, \Sigma, V^T \).

### Ứng dụng của SVD

1. **Giảm chiều dữ liệu**: SVD được sử dụng trong các bài toán giảm chiều dữ liệu như PCA (Principal Component Analysis). Bằng cách chỉ giữ lại một vài giá trị kỳ dị lớn nhất, chúng ta có thể xấp xỉ ma trận ban đầu với một ma trận có xếp hạng thấp hơn, giúp giảm độ phức tạp và giảm nhiễu trong dữ liệu.
  
   Ví dụ: Nếu chỉ giữ lại \( k \) giá trị kỳ dị lớn nhất trong \( \Sigma \), ta có thể xây dựng một ma trận \( A_k \) xấp xỉ với \( A \), giúp giảm chiều dữ liệu xuống \( k \) thành phần quan trọng nhất.

2. **Hệ gợi ý**: SVD là thuật toán cốt lõi trong các hệ gợi ý, đặc biệt là gợi ý dạng cộng tác (collaborative filtering). Bằng cách áp dụng SVD lên ma trận tương tác (ví dụ: ma trận người dùng - sản phẩm), ta có thể tìm ra các đặc trưng tiềm ẩn của người dùng và sản phẩm, từ đó dự đoán các tương tác tiềm năng.

3. **Phát hiện đặc trưng**: SVD có thể giúp phát hiện các đặc trưng tiềm ẩn của dữ liệu. Trong xử lý ảnh, SVD có thể được sử dụng để phân tích các hình ảnh và trích xuất các đặc trưng cơ bản của chúng.

4. **Giải bài toán hệ tuyến tính và ma trận**: SVD cũng được sử dụng để giải các hệ phương trình tuyến tính, đặc biệt là khi ma trận không phải là ma trận vuông hoặc ma trận có điều kiện kém.

### Ví dụ về giảm chiều dữ liệu với SVD

Giả sử bạn có một ma trận dữ liệu \( A \) là một ma trận \( 4 \times 5 \):

\[
A = \begin{bmatrix}
1 & 0 & 0 & 0 & 2 \\
0 & 3 & 0 & 0 & 0 \\
0 & 0 & 0 & 0 & 0 \\
0 & 0 & 0 & 4 & 0
\end{bmatrix}
\]

SVD sẽ phân tích ma trận \( A \) thành:

\[
A = U \Sigma V^T
\]

Nếu ta chỉ giữ lại các giá trị kỳ dị lớn nhất, giả sử là \( \sigma_1, \sigma_2 \), thì ta có thể xấp xỉ ma trận \( A \) với ma trận xếp hạng thấp hơn, giúp giảm lượng dữ liệu cần lưu trữ mà vẫn giữ được hầu hết thông tin của ma trận ban đầu.

### Tổng kết

- **SVD** là một công cụ phân tích mạnh mẽ, cho phép phân tích dữ liệu thành các thành phần chính và tìm ra các đặc trưng tiềm ẩn.
- SVD được sử dụng rộng rãi trong **giảm chiều dữ liệu**, **hệ gợi ý**, và **phát hiện đặc trưng**.
- Ý tưởng cơ bản của SVD là phân tích ma trận thành ba ma trận \( U, \Sigma, V^T \), trong đó ma trận \( \Sigma \) chứa các giá trị kỳ dị thể hiện mức độ quan trọng của các thành phần của dữ liệu.

Việc hiểu rõ SVD và cách hoạt động của nó sẽ giúp bạn áp dụng thuật toán này trong nhiều bài toán phân tích dữ liệu, từ khai phá đặc trưng, giảm nhiễu, đến xây dựng các mô hình dự đoán mạnh mẽ.