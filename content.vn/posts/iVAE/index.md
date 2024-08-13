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


