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

#### **Bước 3: Đạo hàm theo biến phụ trợ \( u \)**
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

