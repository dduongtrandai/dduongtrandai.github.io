---
author: "duongtd"
date: 2024-07-26
title: Tự Tương Quan
tags: [
    ""
]
categories: [
    "Signal Processing"
]
---
**Autocorrelation** là một khái niệm trong thống kê và xử lý tín hiệu dùng để đo lường mức độ tương quan của một tín hiệu với chính nó tại các khoảng thời gian trễ khác nhau. Nói cách khác, autocorrelation xác định mức độ tương tự của tín hiệu tại một thời điểm so với các thời điểm trước đó.

### Công thức

Autocorrelation của một tín hiệu \( x(t) \) tại một khoảng thời gian trễ \( \tau \) được định nghĩa như sau:

\[ R(\tau) = \mathbb{E}[x(t) \cdot x(t + \tau)] \]

Trong đó:

- \( R(\tau) \) là hàm autocorrelation tại khoảng thời gian trễ \( \tau \).
- \( x(t) \) là tín hiệu tại thời điểm \( t \).
- \( x(t + \tau) \) là tín hiệu tại thời điểm \( t + \tau \).
- \( \mathbb{E} \) là ký hiệu của kỳ vọng toán học.

### Ứng dụng

1. **Phân tích tín hiệu**: Autocorrelation được sử dụng để phân tích các đặc tính của tín hiệu, như tìm ra chu kỳ lặp lại hoặc tần số của tín hiệu.
2. **Xử lý âm thanh**: Trong lĩnh vực âm thanh, autocorrelation có thể giúp xác định các đặc điểm của âm thanh, như tần số cơ bản của một giọng nói.
3. **Phân tích chuỗi thời gian**: Autocorrelation được sử dụng trong phân tích chuỗi thời gian để xác định mức độ liên quan giữa các giá trị trong chuỗi tại các thời điểm khác nhau.
4. **Lọc và phát hiện tín hiệu**: Autocorrelation cũng được sử dụng trong việc lọc tín hiệu và phát hiện các mẫu tín hiệu trong nhiều lĩnh vực khác nhau, bao gồm viễn thông và radar.

Autocorrelation là một công cụ quan trọng trong phân tích tín hiệu và thống kê, giúp hiểu rõ hơn về cấu trúc và đặc tính của dữ liệu.
