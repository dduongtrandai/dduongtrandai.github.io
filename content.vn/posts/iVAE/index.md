---
author: "duongtd"
date: 2024-08-12
title: Identifiable VAE
tags: [
    "Nonlinear ICA", "VAE"
]
categories: [
    "Học Sâu"
]
---

**Identifiable VAE (iVAE)** [[1]](#ref1) là một biến thể của mô hình Variational Autoencoder (VAE) với mục tiêu chính là làm cho mô hình này trở nên "có thể nhận dạng được" (identifiable). Điều này có nghĩa là iVAE có khả năng đảm bảo rằng các biến tiềm ẩn \(z\) mà nó học được là duy nhất (up to permutation), không bị ảnh hưởng bởi các biến đổi không mong muốn như sự hoán vị (permutation) hoặc biến đổi phi tuyến (nonlinear transformation). Dưới đây là chi tiết về cấu trúc và cách hoạt động của iVAE.

## **1. Cơ Bản về Identifiability trong Học Máy**

- **Identifiability** trong học máy đề cập đến khả năng xác định duy nhất các biến tiềm ẩn \(z\) từ dữ liệu quan sát \(x\). 
- Trong mô hình VAE truyền thống, không gian tiềm ẩn thường không có tính chất nhận dạng mạnh, nghĩa là cùng một dữ liệu có thể dẫn đến nhiều biểu diễn tiềm ẩn khác nhau, gây khó khăn cho việc giải thích và áp dụng trong thực tế.
- iVAE được thiết kế để khắc phục vấn đề này bằng cách đảm bảo rằng các biến tiềm ẩn học được từ mô hình là duy nhất, phù hợp với các nguồn gốc tiềm ẩn trong dữ liệu.

## **2. Cấu Trúc của Identifiable VAE (iVAE)**

iVAE được xây dựng dựa trên cấu trúc của VAE truyền thống, nhưng có những cải tiến và điều kiện bổ sung để đảm bảo tính nhận dạng.

### **Encoder và Decoder**

- **Encoder**: 
  - Ánh xạ dữ liệu đầu vào \(x\) sang không gian tiềm ẩn \(z\), tương tự như VAE truyền thống. 
  - Tuy nhiên, trong iVAE, encoder được thiết kế để nhận thêm thông tin điều kiện \(u\), có thể là các biến ngoài hoặc các đặc trưng khác của dữ liệu mà giúp phân biệt giữa các nguồn tiềm ẩn khác nhau.
  - Công thức: \( q_{\phi}(z|x, u) \), trong đó \(u\) là biến điều kiện.

- **Decoder**: 
  - Nhận biến tiềm ẩn \(z\) từ encoder và tái tạo lại dữ liệu \(x'\).
  - Giống như VAE, decoder trong iVAE cũng được tối ưu hóa để tái tạo dữ liệu đầu vào từ không gian tiềm ẩn, nhưng bây giờ có thêm yếu tố điều kiện.
  - Công thức: \( p_{\theta}(x|z, u) \).

### **Điều Kiện Hóa Latent Space**

- **Latent Space**:
  - Để đảm bảo tính nhận dạng, iVAE điều kiện hóa không gian tiềm ẩn \(z\) trên các biến điều kiện \(u\).
  - Việc điều kiện hóa này đảm bảo rằng cùng một nguồn tiềm ẩn trong các tập dữ liệu khác nhau có thể được xác định một cách duy nhất, tức là tránh được các sự hoán vị không mong muốn giữa các biến tiềm ẩn.

### **Phân Phối Tiên Nghiệm Có Điều Kiện (Conditional Prior Distribution)**

Trong mô hình iVAE (Identifiable Variational Autoencoder), phân phối tiên nghiệm \( p(z|u) \) được mô hình hóa dựa trên họ phân phối mũ (exponential family). Công thức chi tiết để tính \( p(z|u) \) được trình bày như sau:

\[
p(z|u) = \prod_{i=1}^{n} \frac{Q_i(z_i)}{Z_i(u)} \exp\left( \sum_{j=1}^{k} T_{i,j}(z_i) \lambda_{i,j}(u) \right)
\]

**Trong đó:**

1. **\( Q_i(z_i) \)**: 
   - Đây là hàm cơ sở (base measure) của thành phần \( z_i \) trong biến tiềm ẩn \( z \). 
   - Hàm này có thể là hằng số hoặc có thể phụ thuộc vào \( z_i \), tùy thuộc vào cách mô hình hóa.

2. **\( Z_i(u) \)**:
   - Đây là hằng số chuẩn hóa (normalizing constant) cho thành phần \( z_i \), đảm bảo rằng tổng xác suất trên tất cả các giá trị của \( z_i \) bằng 1. 
   - \( Z_i(u) \) phụ thuộc vào biến phụ trợ \( u \), và nó được tính bằng cách tích phân hoặc tổng trên không gian của \( z_i \).

3. **\( T_{i,j}(z_i) \)**:
   - Đây là hàm thống kê đủ (sufficient statistic) cho \( z_i \). 
   - Các hàm này mô tả các đặc trưng của \( z_i \) mà phân phối phụ thuộc vào.

4. **\( \lambda_{i,j}(u) \)**:
   - Đây là tham số tự nhiên (natural parameter) của phân phối, và nó phụ thuộc vào biến phụ trợ \( u \). 
   - Tham số \( \lambda_{i,j}(u) \) xác định cách mà \( u \) điều kiện hóa phân phối của \( z_i \).

**Ý nghĩa của công thức:**

- **Điều kiện hóa theo \( u \)**: Phân phối \( p(z|u) \) cho phép mô hình iVAE điều kiện hóa các biến tiềm ẩn \( z \) theo biến phụ trợ \( u \), giúp phá vỡ tính đối xứng và đảm bảo rằng các biến tiềm ẩn \( z \) có thể nhận dạng được một cách duy nhất từ dữ liệu quan sát.

- **Mô hình hóa phân phối \( p(z|u) \)**: Phân phối này là sự kết hợp của các thành phần \( Q_i(z_i) \), các hàm thống kê đủ \( T_{i,j}(z_i) \), và các tham số \( \lambda_{i,j}(u) \), từ đó mô tả cách mà các biến tiềm ẩn được sinh ra dựa trên thông tin từ \( u \).

### **Phân Phối Hậu Nghiệm Có Điều Kiện (Conditional Posterior Distribution)**

- iVAE mở rộng phân phối hậu nghiệm bằng cách điều kiện hóa trên \(u\), thay vì chỉ đơn thuần là phân phối \(q(z|x)\) như trong VAE truyền thống.
- Điều này có nghĩa là khi học các biến tiềm ẩn, iVAE sử dụng thêm thông tin \(u\) để tách biệt các nguồn tiềm ẩn khác nhau, giúp chúng trở nên có thể nhận dạng được.

## **3. Hàm Mục Tiêu (Objective Function)**

- Hàm mục tiêu của iVAE cũng tương tự như VAE, nhưng với một số điều khoản bổ sung để đảm bảo tính nhận dạng:
  \[
  \mathcal{L}(\theta, \phi; x, u) = \mathbb{E}_{q_{\phi}(z|x,u)}[\log p_{\theta}(x|z,u)] - D_{\text{KL}}(q_{\phi}(z|x,u) \| p(z|u))
  \]
  - **Term 1**: Tái tạo dữ liệu \(x\) từ \(z\) và \(u\), giống như trong VAE truyền thống.
  - **Term 2**: KL-divergence giữa phân phối hậu nghiệm có điều kiện và phân phối tiên nghiệm có điều kiện \(p(z|u)\), giúp điều kiện hóa và duy trì tính nhận dạng của không gian tiềm ẩn.

## **4. Ứng Dụng Thực Tế**

iVAE có thể được áp dụng trong nhiều lĩnh vực nơi mà việc nhận dạng các nguồn tiềm ẩn là quan trọng:

- **Tách nguồn (source separation)**: Trong các ứng dụng như tách nguồn âm thanh hoặc tách tín hiệu não, iVAE giúp đảm bảo rằng các nguồn tiềm ẩn học được từ tín hiệu hỗn hợp là duy nhất và có thể nhận dạng.
- **Phân tích nhân tố tiềm ẩn (latent factor analysis)**: iVAE hữu ích trong việc phân tích các nhân tố tiềm ẩn trong dữ liệu phức tạp như dữ liệu y tế hoặc tài chính, nơi mà việc nhận dạng chính xác các nhân tố này là rất quan trọng.
- **Học biểu diễn có thể giải thích được (interpretable representation learning)**: iVAE giúp học các biểu diễn tiềm ẩn mà có thể giải thích được, giúp ích cho việc ra quyết định và phân tích dữ liệu.

## **Kết Luận**

**Identifiable VAE (iVAE)** là một biến thể mạnh mẽ của VAE, giúp khắc phục vấn đề nhận dạng trong không gian tiềm ẩn bằng cách điều kiện hóa trên các biến điều kiện. Điều này làm cho iVAE trở thành một công cụ hữu ích trong các ứng dụng cần sự nhận dạng chính xác các nguồn tiềm ẩn hoặc nhân tố tiềm ẩn trong dữ liệu, và giúp tăng cường tính giải thích và độ tin cậy của các mô hình học máy.

**Identifiable VAE (iVAE)** [1](#ref1) là một biến thể mạnh mẽ của VAE, giúp khắc phục vấn đề nhận dạng trong không gian tiềm ẩn bằng cách điều kiện hóa trên các biến điều kiện.

## **Tài Liệu Tham Khảo**

<a id="ref1"></a>[1] I. Khemakhem, D. P. Kingma, R. P. Monti, and A. Hyvärinen, [“Variational Autoencoders and Nonlinear ICA: A Unifying Framework,”](https://arxiv.org/abs/1907.04809) Dec. 21, 2020, arXiv: arXiv:1907.04809. doi: 10.48550/arXiv.1907.04809.

## **Phụ Lục**
Trong bài báo "Variational Autoencoders and Nonlinear ICA: A Unifying Framework", các tác giả đã chứng minh rằng mô hình iVAE có thể nhận dạng được (identifiable) khi có thêm biến phụ trợ \( u \). Dưới đây là chi tiết về chứng minh này:

### 1. **Giả định ban đầu**:
   - Ta có một mô hình biến ẩn sâu (deep latent-variable model) với biến quan sát \( x \), biến tiềm ẩn \( z \), và một biến phụ trợ \( u \).
   - Mô hình có dạng: \( p_{\theta}(x, z | u) = p_f(x | z) p_{T, \lambda}(z | u) \)
     - \( p_f(x | z) \) là phân phối điều kiện của \( x \) dựa trên \( z \).
     - \( p_{T, \lambda}(z | u) \) là phân phối tiên nghiệm của \( z \) dựa trên biến phụ trợ \( u \), được giả định là một phân phối thuộc họ hàm mũ có điều kiện.

### 2. **Bước đầu tiên** - Biến đổi phân phối dữ liệu quan sát thành phân phối không nhiễu:
   - Từ giả thiết \( p_{\theta}(x, z | u) = p_{\theta'}(x, z | u) \) với mọi \( x \) và \( u \), các tác giả sử dụng phép biến đổi Fourier để loại bỏ ảnh hưởng của nhiễu \( \epsilon \), từ đó chuyển bài toán về trường hợp không có nhiễu:
     \[
     \log p_{T, \lambda}(f^{-1}(x) | u) = \log p_{T', \lambda'}(f'^{-1}(x) | u) + \text{c}
     \]
   - Điều này giúp rút gọn bài toán về việc so sánh trực tiếp các thành phần không nhiễu.

### 3. **Bước thứ hai** - Loại bỏ các biến phụ trợ:
   - Sau khi có được phương trình trên, họ tiếp tục loại bỏ biến phụ trợ \( u \) bằng cách sử dụng một số điểm \( u_0, u_1, \dots, u_{nk} \) sao cho ma trận \( L \) liên quan đến các tham số \( \lambda(u) \) là khả nghịch. Điều này dẫn đến:
     \[
     T(f^{-1}(x)) = A T'(f'^{-1}(x)) + c
     \]
   - Tại đây, \( A \) là một ma trận khả nghịch và \( c \) là một vector, điều này cho thấy sự phụ thuộc tuyến tính giữa các thành phần của mô hình.

### 4. **Bước thứ ba** - Chứng minh tính khả nghịch của ma trận \( A \):
   - Trong trường hợp \( k = 1 \), ma trận \( A \) khả nghịch do \( A \) là một ma trận vuông.
   - Khi \( k > 1 \), bằng việc sử dụng các ma trận Jacobian và giả thiết rằng các thống kê đủ \( T_i(z) \) tuyến tính độc lập trên các tập hợp \( X \) có độ đo dương, các tác giả chứng minh được rằng ma trận \( A \) là khả nghịch.

### 5. **Kết luận**:
   - Cuối cùng, các tác giả chứng minh rằng với các giả thiết đã nêu, mô hình iVAE là nhận dạng được. Điều này có nghĩa là với một mô hình iVAE, nếu các tham số mô hình được học từ dữ liệu, các tham số đó sẽ tương ứng duy nhất với các biến tiềm ẩn \( z \), giúp đảm bảo rằng quá trình học không rơi vào tình trạng không xác định.

Chứng minh này là một trong những kết quả quan trọng trong bài báo, cho thấy rằng việc thêm biến phụ trợ \( u \) vào mô hình có thể giải quyết được vấn đề không nhận dạng được trong các mô hình biến ẩn sâu như VAE truyền thống.

Dưới đây là quá trình chứng minh chi tiết tính nhận dạng của mô hình iVAE dựa trên biến phụ trợ \( u \), được trình bày trong phần B.2.2 của bài báo:

### **B.2.2 Chứng minh tính nhận dạng của iVAE**

#### **Bước 1: Giới thiệu khái niệm về thể tích của ma trận**
- Tác giả sử dụng khái niệm thể tích ma trận, ký hiệu là vol A, là tích của các giá trị riêng (singular values) của ma trận A.
- Khi ma trận A có hạng đầy đủ, vol A bằng căn bậc hai của định thức \( \text{det}(A^T A) \).
- Khi ma trận A là ma trận vuông và khả nghịch, vol A bằng giá trị tuyệt đối của định thức \( | \text{det}(A) | \).
- Thể tích ma trận này được sử dụng trong công thức biến đổi (change of variable formula), đặc biệt hữu ích khi Jacobian là một ma trận hình chữ nhật (tức là số hàng ít hơn số cột, \( n < d \)).

#### **Bước 2: Thiết lập phương trình cho hai bộ tham số**
- Giả sử có hai bộ tham số \( (f, T, \lambda) \) và \( (\tilde{f}, \tilde{T}, \tilde{\lambda}) \) sao cho \( p_{f,T,\lambda}(x|u) = p_{\tilde{f}, \tilde{T}, \tilde{\lambda}}(x|u) \) với mọi cặp \( (x, u) \). Điều này có nghĩa là phân phối xác suất điều kiện cho cả hai bộ tham số là tương đương.
- Từ đó, ta có phương trình sau đây:

\[
\log \text{vol} J_{f^{-1}}(x) + \sum_{i=1}^{n} \left( \log Q_i(f^{-1}_i(x)) - \log Z_i(u) + \sum_{j=1}^{k} T_{i,j}(f^{-1}_i(x)) \lambda_{i,j}(u) \right) 
\]

bằng với:

\[
\log \text{vol} J_{\tilde{f}^{-1}}(x) + \sum_{i=1}^{n} \left( \log \tilde{Q}_i(\tilde{f}^{-1}_i(x)) - \log \tilde{Z}_i(u) + \sum_{j=1}^{k} \tilde{T}_{i,j}(\tilde{f}^{-1}_i(x)) \tilde{\lambda}_{i,j}(u) \right)
\]

#### **Bước 3: Đạo hàm theo biến phụ trợ u**
- Lấy đạo hàm của cả hai vế phương trình theo \( u \) để loại bỏ các thành phần chỉ phụ thuộc vào \( x \), giả sử \( \tilde{\lambda} \) cũng khả vi. Khi đó, ta được phương trình:

\[
J_\lambda(u)T T(f^{-1}(x)) - \sum_{i} \nabla \log Z_i(u) = J_{\tilde{\lambda}}(u)T \tilde{T}(\tilde{f}^{-1}(x)) - \sum_{i} \nabla \log \tilde{Z}_i(u)
\]

- Sau đó, phương trình này được đánh giá tại một điểm cụ thể \( u_0 \) (được giả định trong điều kiện iv) và nhân với ma trận \( J_\lambda(u_0)^{-T} \) (khả nghịch do giả thiết).

#### **Bước 4: Kết luận từ phương trình**
- Sau khi thực hiện các phép toán trên, ta có được phương trình dạng:

\[
T(f^{-1}(x)) = A \tilde{T}(\tilde{f}^{-1}(x)) + c
\]

trong đó \( A \) là một ma trận và \( c \) là một hằng số liên quan đến \( Z_i(u_0) \) và \( \tilde{Z}_i(u_0) \).

- Phần còn lại của chứng minh tiếp tục từ điểm này, sử dụng các lập luận để chỉ ra rằng \( J_{\tilde{\lambda}}(u_0) \) là khả nghịch, từ đó đảm bảo rằng các tham số \( (f, T, \lambda) \) và \( (\tilde{f}, \tilde{T}, \tilde{\lambda}) \) phải tương đương, tức là mô hình có khả năng nhận dạng.

### **Kết luận**
Phương pháp đạo hàm theo \( u \) trong phần B.2.2 của bài báo đóng vai trò then chốt trong chứng minh tính nhận dạng của iVAE. Biến phụ trợ \( u \) được sử dụng để loại bỏ các thành phần không liên quan, từ đó tập trung vào những phần quan trọng giúp đảm bảo rằng các tham số của mô hình có thể được xác định duy nhất.

### Định lý 1 trong bài báo đề xuất mô hình iVAE

#### **Nội dung Định lý 1:**

Giả sử rằng dữ liệu quan sát được lấy mẫu từ một mô hình sinh theo các tham số \( (f, T, \lambda) \) như được định nghĩa trong các công thức (5)-(7) của bài báo. Định lý 1 thiết lập các điều kiện dưới đó các tham số \( (f, T, \lambda) \) có thể nhận dạng được từ dữ liệu quan sát, cụ thể như sau:

**Giả định:**
1. **Giả định (i):** Tập hợp các điểm \( \{x \in X | \varphi_\epsilon(x) = 0\} \) có độ đo bằng 0, trong đó \( \varphi_\epsilon \) là hàm đặc trưng của mật độ xác suất \( p_\epsilon \) được định nghĩa trong công thức (6).
   - Ý nghĩa: Điều này đảm bảo rằng hàm mật độ xác suất không bị mất mát thông tin tại bất kỳ điểm nào trên không gian quan sát.

2. **Giả định (ii):** Hàm trộn \( f \) trong công thức (6) là một ánh xạ injective, nghĩa là mỗi điểm trong không gian tiềm ẩn \( z \) sẽ ánh xạ tới một điểm duy nhất trong không gian quan sát \( x \).
   - Ý nghĩa: Đây là điều kiện quan trọng để đảm bảo rằng không có hai giá trị \( z \) khác nhau nào cho cùng một giá trị \( x \), tức là có thể đảo ngược từ \( x \) về \( z \).

3. **Giả định (iii):** Các hàm thống kê đủ \( T_{i,j} \) trong công thức (7) là khả vi gần như ở mọi nơi và các \( T_{i,j} \) là độc lập tuyến tính trên bất kỳ tập con nào của \( X \) có độ đo lớn hơn 0.
   - Ý nghĩa: Điều kiện này đảm bảo rằng các hàm thống kê \( T_{i,j} \) là đủ linh hoạt để mô tả các đặc trưng của dữ liệu mà không bị phụ thuộc vào nhau.

4. **Giả định (iv):** Tồn tại \( nk + 1 \) điểm phân biệt \( u_0, \dots, u_{nk} \) sao cho ma trận 
   \[
   L = (\lambda(u_1) - \lambda(u_0), \dots, \lambda(u_{nk}) - \lambda(u_0))
   \]
   có kích thước \( nk \times nk \) là khả nghịch.
   - Ý nghĩa: Điều này đảm bảo rằng các giá trị của tham số \( \lambda \) khác biệt nhau đủ để xác định được các tham số trong mô hình.

**Kết luận:**
- Dưới các giả định trên, các tham số \( (f, T, \lambda) \) là \( \sim_A \)-nhận dạng được, tức là chúng có thể được xác định một cách duy nhất từ dữ liệu quan sát \( x \) thông qua biến phụ trợ \( u \).

### **Định lý 1:**

1. **Injectivity (tính injective) của \( f \):**
   - Đây là điều kiện cần thiết để đảm bảo rằng không có sự mơ hồ khi ánh xạ từ không gian tiềm ẩn \( z \) sang không gian quan sát \( x \). Nếu \( f \) không phải là một hàm injective, thì có thể tồn tại nhiều giá trị \( z \) tương ứng với cùng một giá trị \( x \), dẫn đến việc không thể nhận dạng chính xác các tham số của mô hình.

2. **Độc lập tuyến tính của các hàm thống kê đủ \( T_{i,j} \):**
   - Điều kiện này giúp đảm bảo rằng các hàm thống kê \( T_{i,j} \) có thể mô tả đầy đủ các đặc trưng của dữ liệu quan sát mà không bị phụ thuộc lẫn nhau. Điều này là quan trọng để giữ cho các tham số \( T \) có thể nhận dạng được.

3. **Khả nghịch của ma trận \( L \):**
   - Ma trận \( L \) chứa sự khác biệt giữa các tham số \( \lambda \) tại các điểm khác nhau của biến phụ trợ \( u \). Khả nghịch của ma trận này đảm bảo rằng các tham số \( \lambda \) có đủ độ phân biệt để xác định các giá trị khác nhau của \( u \), từ đó đảm bảo rằng các tham số của mô hình có thể nhận dạng được.

4. **Ý nghĩa của tính \( \sim_A \)-nhận dạng được:**
   - \( \sim_A \) là một quan hệ tương đương mà trong đó các bộ tham số \( (f, T, \lambda) \) và \( (\tilde{f}, \tilde{T}, \tilde{\lambda}) \) được coi là tương đương nếu chúng liên quan đến nhau qua một biến đổi tuyến tính \( A \) và một số phi tuyến. Định lý 1 đảm bảo rằng nếu dữ liệu được tạo ra bởi một bộ tham số nhất định, thì bộ tham số đó có thể nhận dạng được từ dữ liệu, và nếu có một bộ tham số khác dẫn đến cùng một phân phối quan sát, thì hai bộ tham số này phải tương đương nhau theo nghĩa của quan hệ \( \sim_A \).

### **Kết luận:**
Định lý 1 thiết lập các điều kiện cụ thể dưới đó mô hình iVAE có thể nhận dạng được các tham số tiềm ẩn từ dữ liệu quan sát. Điều này là cơ sở lý thuyết quan trọng để đảm bảo rằng mô hình iVAE có thể học được các đặc trưng tiềm ẩn từ dữ liệu một cách chính xác và duy nhất.
