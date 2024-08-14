---
author: "duongtd"
date: 2024-08-11
title: Autoencoder vs Variational Autoencoder
tags: [
    "VAE"
]
categories: [
    "Học Sâu"
]
---
Autoencoder (AE) và Variational Autoencoder (VAE) là hai loại mô hình học sâu được sử dụng rộng rãi trong các nhiệm vụ như giảm chiều dữ liệu, phát hiện bất thường, và tạo sinh dữ liệu mới. Mặc dù cả hai đều được thiết kế để học một biểu diễn tiềm ẩn (latent representation) của dữ liệu đầu vào, nhưng chúng khác nhau ở một số điểm quan trọng.

### **1. Autoencoder (AE)**

- **Cấu trúc**:
  - AE bao gồm hai phần chính: **Encoder** và **Decoder**.
  - **Encoder**: Chuyển đổi dữ liệu đầu vào thành một biểu diễn tiềm ẩn (latent representation) trong không gian có chiều thấp hơn.
  - **Decoder**: Chuyển đổi biểu diễn tiềm ẩn trở lại thành dữ liệu đầu ra, nhằm tái tạo lại dữ liệu gốc.

- **Hàm mất mát**:
  - Hàm mất mát của AE là **Reconstruction Loss**, thường được tính là khoảng cách giữa dữ liệu gốc và dữ liệu tái tạo (ví dụ: MSE - Mean Squared Error).
  - Mục tiêu là giảm thiểu mất mát này để đảm bảo dữ liệu tái tạo \(x'\) gần giống nhất với dữ liệu ban đầu \(x\).

- **Biểu diễn tiềm ẩn**:
  - Biểu diễn tiềm ẩn của AE là một vector cụ thể, không có sự phân phối xác suất rõ ràng nào cho các biến tiềm ẩn.

- **Hạn chế**:
  - AE có thể gặp phải vấn đề overfitting nếu không có kỹ thuật regularization phù hợp, và không có cơ chế kiểm soát để các biểu diễn tiềm ẩn học được có cấu trúc.

### **2. Variational Autoencoder (VAE)**

- **Cấu trúc**:
  - Giống như AE, VAE cũng bao gồm **Encoder** và **Decoder**.
  - Tuy nhiên, VAE được thiết kế để không chỉ học một vector tiềm ẩn mà còn học một phân phối xác suất của các biến tiềm ẩn.

- **Hàm mất mát**:
  - Hàm mất mát của VAE bao gồm hai thành phần:
    1. **Reconstruction Loss**: Tương tự như AE, để đảm bảo rằng dữ liệu tái tạo gần giống với dữ liệu gốc.
    2. **KL-Divergence**: Đo lường sự khác biệt giữa phân phối hậu nghiệm \(q(z|x)\) (do encoder mô hình hóa) và phân phối tiên nghiệm \(p(z)\) (thường là Gaussian). Thành phần này khuyến khích phân phối hậu nghiệm gần giống với phân phối tiên nghiệm.
  
- **Biểu diễn tiềm ẩn**:
  - Biểu diễn tiềm ẩn trong VAE là một phân phối xác suất, không phải là một vector cụ thể. Encoder học các tham số (mean và variance) của phân phối này.
  - Trong quá trình sinh dữ liệu mới, một mẫu \(z\) được lấy từ phân phối này và được sử dụng bởi decoder để tạo ra dữ liệu mới.

- **Ưu điểm**:
  - VAE có khả năng sinh dữ liệu mới có ý nghĩa bằng cách lấy mẫu từ không gian tiềm ẩn.
  - VAE có thể kiểm soát và mô hình hóa các biến tiềm ẩn, giúp tránh overfitting và tăng khả năng tổng quát hóa.

### **Tóm tắt Sự Khác Biệt Chính**

- **AE** học một vector tiềm ẩn cụ thể, trong khi **VAE** học một phân phối xác suất của các biến tiềm ẩn.
- **Hàm mất mát** của AE chỉ bao gồm phần tái cấu trúc, trong khi VAE bao gồm cả phần tái cấu trúc và KL-Divergence để điều chỉnh phân phối tiềm ẩn.
- **VAE** có thể sinh dữ liệu mới từ không gian tiềm ẩn một cách có kiểm soát, trong khi AE không có khả năng này.

Những điểm khác biệt này làm cho VAE trở nên hữu ích trong các ứng dụng mà việc sinh dữ liệu mới hoặc hiểu rõ về cấu trúc tiềm ẩn là quan trọng, như trong các bài toán mô hình hóa phân phối dữ liệu hoặc trong các bài toán sinh dữ liệu giả lập.