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

**Identifiable VAE (iVAE)** là một biến thể của mô hình Variational Autoencoder (VAE) với mục tiêu chính là làm cho mô hình này trở nên "có thể nhận dạng được" (identifiable). Điều này có nghĩa là iVAE có khả năng đảm bảo rằng các biến tiềm ẩn \(z\) mà nó học được là duy nhất (up to permutation), không bị ảnh hưởng bởi các biến đổi không mong muốn như sự hoán vị (permutation) hoặc biến đổi phi tuyến (nonlinear transformation). Dưới đây là chi tiết về cấu trúc và cách hoạt động của iVAE.

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