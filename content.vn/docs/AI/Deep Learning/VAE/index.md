---
title: "Variational Autoencoder (VAE)"
---

# **Variational Autoencoder (VAE)**
Variational Autoencoder (VAE) là một mô hình học sâu sử dụng phương pháp suy luận biến thể để học các biểu diễn tiềm ẩn của dữ liệu một cách có cấu trúc. VAE là một trong những phương pháp phổ biến nhất để xây dựng các mô hình sinh, tức là các mô hình có thể sinh ra dữ liệu mới giống với dữ liệu đã học. Dưới đây là mô tả chi tiết về VAE.

## **1. Cơ Sở Lý Thuyết**
VAE thuộc loại mô hình **Bayesian Inference** kết hợp với **Autoencoder**. Thay vì học một hàm ánh xạ trực tiếp từ không gian dữ liệu đầu vào sang không gian tiềm ẩn và ngược lại như Autoencoder truyền thống, VAE học một phân phối xác suất có điều kiện giữa các không gian này.

### **Biến tiềm ẩn và dữ liệu quan sát**
- **Biến tiềm ẩn** \( z \): Là những biến ẩn chưa biết mà chúng ta muốn học. VAE giả định rằng dữ liệu quan sát \( x \) được sinh ra từ những biến ẩn này.
- **Dữ liệu quan sát** \( x \): Là những dữ liệu mà chúng ta có sẵn và muốn mô hình hóa.

### **Mục tiêu của VAE**:
VAE cố gắng tìm phân phối \( p(z|x) \) để từ đó suy ra dữ liệu \( x \) bằng cách tìm một hàm ánh xạ từ không gian tiềm ẩn \( z \) sang không gian dữ liệu \( x \). Điều này đạt được thông qua việc tối đa hóa một hàm hợp lý biến thể được gọi là **Evidence Lower Bound (ELBO)**.

## **2. Cấu Trúc Mô Hình**
VAE bao gồm hai thành phần chính: **Encoder** và **Decoder**.

### **Encoder (Bộ mã hóa)**
- **Vai trò**: Biến đổi dữ liệu quan sát \( x \) thành một phân phối xác suất của biến tiềm ẩn \( z \).
- **Công thức**: 
  \[
  q_{\phi}(z|x) = \mathcal{N}(z; \mu(x), \Sigma(x))
  \]
  - \( \mu(x) \): Trung bình của phân phối Gaussian, là một hàm của \( x \) và được học qua một mạng nơron.
  - \( \Sigma(x) \): Phương sai của phân phối Gaussian, cũng là một hàm của \( x \) và được học.

### **Decoder (Bộ giải mã)**
- **Vai trò**: Biến đổi một mẫu từ phân phối tiềm ẩn \( z \) trở lại không gian dữ liệu \( x \).
- **Công thức**:
  \[
  p_{\theta}(x|z) = \mathcal{N}(x; \mu'(z), \Sigma'(z))
  \]
  - \( \mu'(z) \): Trung bình của phân phối Gaussian, là một hàm của \( z \) và được học qua một mạng nơron.
  - \( \Sigma'(z) \): Phương sai của phân phối Gaussian.

## **3. Hàm Mất Mát trong VAE**
VAE sử dụng một hàm mất mát tổng hợp để tối ưu hóa mô hình, bao gồm hai phần chính:

### **1. Mất mát tái tạo (Reconstruction Loss)**:
- **Mục tiêu**: Đo lường độ khác biệt giữa dữ liệu gốc \( x \) và dữ liệu tái tạo \( x' \) từ mẫu \( z \).
- **Công thức**:
  \[
  \text{Reconstruction Loss} = -\mathbb{E}_{q_{\phi}(z|x)}[\log p_{\theta}(x|z)]
  \]
- **Ý nghĩa**: Phần này khuyến khích mô hình tái tạo lại dữ liệu đầu vào sao cho dữ liệu sinh ra từ \( z \) là gần giống nhất với dữ liệu gốc.

### **2. Mất mát Kullback-Leibler Divergence (KL Loss)**:
- **Mục tiêu**: Đo lường độ khác biệt giữa phân phối \( q_{\phi}(z|x) \) mà Encoder học được và phân phối tiên nghiệm \( p(z) \) thường được giả định là \( \mathcal{N}(0, I) \).
- **Công thức**:
  \[
  \text{KL Loss} = D_{KL}(q_{\phi}(z|x) || p(z))
  \]
- **Ý nghĩa**: Phần này khuyến khích phân phối \( q_{\phi}(z|x) \) mà mô hình học được gần với phân phối chuẩn \( \mathcal{N}(0, I) \), giúp mô hình có tính tổng quát và dễ dàng lấy mẫu từ không gian tiềm ẩn.

## **4. Tối Ưu Hóa**
Tổng hàm mất mát của VAE là sự kết hợp của hai thành phần trên:
\[
\mathcal{L}(\theta, \phi; x) = -\mathbb{E}_{q_{\phi}(z|x)}[\log p_{\theta}(x|z)] + D_{KL}(q_{\phi}(z|x) || p(z))
\]
Mục tiêu của quá trình huấn luyện là tối thiểu hóa hàm mất mát này.

## **5.  Ví Dụ Cụ Thể**
Giả sử ta muốn xây dựng một VAE để học biểu diễn tiềm ẩn của một bộ dữ liệu hình ảnh đơn giản, như bộ dữ liệu MNIST.

- **Dữ liệu đầu vào**: Hình ảnh số viết tay 28x28 pixel từ bộ dữ liệu MNIST.
- **Encoder**:
  - Dữ liệu được flatten thành vector 784 chiều.
  - Qua một mạng nơron có hai lớp ẩn với hàm kích hoạt ReLU, sau đó là hai lớp đầu ra cho \( \mu \) và \( \log(\sigma^2) \).
- **Reparameterization Trick**:
  - Lấy mẫu từ phân phối tiềm ẩn bằng cách sử dụng \( z = \mu(x) + \sigma(x) \cdot \epsilon \) với \( \epsilon \sim \mathcal{N}(0, I) \).
- **Decoder**:
  - Mẫu \( z \) được đưa qua một mạng nơron khác để tái tạo lại hình ảnh.
  - Đầu ra của Decoder là một phân phối xác suất Gaussian cho mỗi pixel của ảnh tái tạo.
- **Tối ưu hóa**:
  - Huấn luyện mô hình bằng cách tối thiểu hóa tổng hàm mất mát, tức là tối đa hóa ELBO.

## **6. Ứng Dụng của VAE**
- **Sinh dữ liệu mới**: Sau khi huấn luyện, ta có thể lấy mẫu từ không gian tiềm ẩn để sinh ra dữ liệu mới mà mô hình chưa từng thấy.
- **Giảm kích thước**: Sử dụng VAE để giảm kích thước dữ liệu (dimensionality reduction) bằng cách chuyển dữ liệu sang không gian tiềm ẩn.
- **Phân loại**: Sử dụng biểu diễn tiềm ẩn \( z \) làm đặc trưng đầu vào cho các mô hình phân loại khác.

## **7. Ưu điểm và Hạn chế của VAE**
- **Ưu điểm**:
  - Có khả năng học biểu diễn tiềm ẩn hữu ích cho nhiều ứng dụng khác nhau.
  - Tích hợp tốt các yếu tố không chắc chắn và đảm bảo tính khả thi của việc sinh dữ liệu mới.
- **Hạn chế**:
  - Khả năng sinh dữ liệu có thể không sắc nét hoặc chi tiết bằng các mô hình khác như GAN (Generative Adversarial Networks).
  - Việc tối ưu hóa KL-divergence có thể dẫn đến một số vấn đề về học tập, như hiện tượng "posterior collapse", nơi mà mô hình không tận dụng hết không gian tiềm ẩn.

## **Kết Luận**

Variational Autoencoder (VAE) là một mô hình mạnh mẽ và linh hoạt, đặc biệt trong việc học các biểu diễn tiềm ẩn và sinh dữ liệu mới. Mặc dù có một số hạn chế, nhưng VAE vẫn là một công cụ quan trọng trong kho vũ khí của các nhà nghiên cứu học sâu, với nhiều ứng dụng tiềm năng trong phân tích dữ liệu và học biểu diễn.
