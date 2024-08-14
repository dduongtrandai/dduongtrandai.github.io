---
author: "duongtd"
date: 2024-07-26
title: Stationary vs Non-stationary
tags: [
    ""
]
categories: [
    "Xử Lý Tín Hiệu"
]
---

Trong xử lý tín hiệu, khái niệm **stationary (ổn định)** và **non-stationary (không ổn định)** được sử dụng để mô tả tính chất của tín hiệu theo thời gian.

## Tín hiệu ổn định (Stationary Signal)
Tín hiệu được gọi là ổn định khi các đặc tính thống kê của nó không thay đổi theo thời gian. Các đặc tính thống kê bao gồm trung bình, phương sai và các hàm tương quan. Có hai loại ổn định:

1. **Ổn định yếu (Weak Stationarity hoặc Wide-Sense Stationarity)**: Tín hiệu có trung bình và phương sai không đổi theo thời gian và hàm tương quan chỉ phụ thuộc vào khoảng thời gian giữa hai thời điểm, không phụ thuộc vào chính thời điểm đó.
   
2. **Ổn định mạnh (Strong Stationarity hoặc Strict-Sense Stationarity)**: Mọi phân bố xác suất của tín hiệu đều không thay đổi theo thời gian.

## Tín hiệu không ổn định (Non-Stationary Signal)
Tín hiệu được gọi là không ổn định khi các đặc tính thống kê của nó thay đổi theo thời gian. Điều này có nghĩa là trung bình, phương sai, hoặc các hàm tương quan của tín hiệu thay đổi theo thời gian. Tín hiệu không ổn định thường xuất hiện trong các hệ thống mà đặc tính của chúng thay đổi theo thời gian, ví dụ như tín hiệu âm thanh, tín hiệu y tế (nhịp tim, sóng não), và nhiều loại dữ liệu thực tế khác.

## Ứng dụng và Xử lý
1. **Xử lý tín hiệu ổn định**: Các phương pháp như Fourier Transform (FT) và Fast Fourier Transform (FFT) thường được áp dụng vì chúng giả định tín hiệu là ổn định.
   
2. **Xử lý tín hiệu không ổn định**: Các phương pháp phân tích thời gian-tần số như Short-Time Fourier Transform (STFT), Wavelet Transform, và Empirical Mode Decomposition (EMD) thường được sử dụng để phân tích và xử lý tín hiệu không ổn định.

Hiểu rõ sự khác biệt giữa tín hiệu ổn định và không ổn định là rất quan trọng trong việc lựa chọn phương pháp xử lý tín hiệu phù hợp nhằm đạt được kết quả chính xác và hiệu quả.