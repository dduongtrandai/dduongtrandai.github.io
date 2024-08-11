---
author: "duongtd"
date: 2024-08-11
title: Phân phối Tiên Nghiệm và Hậu Nghiệm
tags: [
    ""
]
categories: [
    ""
]
---
### **Phân phối Tiên Nghiệm và Hậu Nghiệm**

Trong bối cảnh thống kê Bayes và các mô hình học sâu như Variational Autoencoder (VAE) hoặc iVAE, hai khái niệm **phân phối tiên nghiệm (prior distribution)** và **phân phối hậu nghiệm (posterior distribution)** thường được sử dụng để mô tả sự không chắc chắn và cách thông tin mới được tích hợp vào mô hình. Dưới đây là giải thích chi tiết về hai khái niệm này:

### **1. Phân phối Tiên Nghiệm (Prior Distribution)**

- **Định nghĩa**: Phân phối tiên nghiệm, ký hiệu là \( p(z) \), là phân phối xác suất mô tả sự hiểu biết ban đầu hoặc giả định về các biến số trước khi quan sát bất kỳ dữ liệu nào. Trong một mô hình, nó thể hiện những gì ta tin tưởng về các biến tiềm ẩn \( z \) trước khi dữ liệu quan sát \( x \) được tính đến.
  
- **Ví dụ**: Giả sử ta có một mô hình mà \( z \) đại diện cho nhiệt độ trung bình hàng ngày. Trước khi thu thập dữ liệu, ta có thể giả định rằng nhiệt độ trung bình hàng ngày thường tuân theo phân phối Gaussian với trung bình là 20°C và độ lệch chuẩn là 5°C. Phân phối này là phân phối tiên nghiệm.

- **Vai trò trong Mô hình**: Phân phối tiên nghiệm giúp mô hình có một giả định ban đầu về các biến tiềm ẩn và có thể ảnh hưởng đến cách mô hình diễn giải dữ liệu mới.

### **2. Phân phối Hậu Nghiệm (Posterior Distribution)**

- **Định nghĩa**: Phân phối hậu nghiệm, ký hiệu là \( p(z|x) \), là phân phối xác suất của các biến tiềm ẩn \( z \) sau khi đã quan sát dữ liệu \( x \). Nó kết hợp thông tin từ dữ liệu quan sát với thông tin tiên nghiệm để cung cấp một cái nhìn cập nhật về các biến tiềm ẩn.

- **Ví dụ**: Sau khi thu thập dữ liệu thực tế về nhiệt độ trong nhiều ngày, ta nhận thấy rằng nhiệt độ trung bình thực tế có thể khác với giả định ban đầu. Phân phối hậu nghiệm sẽ điều chỉnh sự hiểu biết của ta về nhiệt độ dựa trên cả phân phối tiên nghiệm và dữ liệu mới thu thập này.

- **Vai trò trong Mô hình**: Phân phối hậu nghiệm là thông tin cuối cùng mà mô hình học được về các biến tiềm ẩn, kết hợp cả kiến thức tiên nghiệm và dữ liệu quan sát. Nó cung cấp thông tin chính xác hơn về các biến tiềm ẩn dựa trên dữ liệu thực tế.

### **Mối Quan Hệ giữa Phân phối Tiên Nghiệm và Hậu Nghiệm**

Trong Bayes' theorem, phân phối hậu nghiệm được tính toán dựa trên phân phối tiên nghiệm và hàm khả năng (likelihood) của dữ liệu quan sát:

\[
p(z|x) = \frac{p(x|z) \cdot p(z)}{p(x)}
\]

- **Hàm khả năng (Likelihood)** \( p(x|z) \): Xác suất của dữ liệu quan sát \( x \) với một giá trị cụ thể của \( z \).

- **Phân phối hậu nghiệm** \( p(z|x) \): Kết hợp giữa thông tin ban đầu từ phân phối tiên nghiệm và thông tin mới từ dữ liệu quan sát.

### **Kết Luận**

- **Phân phối tiên nghiệm** là giả định ban đầu về các biến tiềm ẩn trước khi có dữ liệu, trong khi **phân phối hậu nghiệm** là sự hiểu biết cập nhật về các biến tiềm ẩn sau khi đã quan sát dữ liệu. Sự kết hợp giữa hai phân phối này thông qua Bayes' theorem giúp mô hình học tập và cải thiện độ chính xác dựa trên dữ liệu thực tế.
