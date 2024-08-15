---
title: Họ Phân Phối Mũ
---

# Họ Phân Phối Mũ (Exponential Family)

Họ phân phối mũ là một lớp rộng của các phân phối xác suất có cấu trúc toán học cụ thể, cho phép chúng ta mô hình hóa nhiều dạng dữ liệu khác nhau một cách tổng quát. Một phân phối thuộc họ phân phối mũ có thể được viết dưới dạng:

\[
p(x|\theta) = h(x) \exp\left(\eta(\theta)^\top T(x) - A(\theta)\right)
\]

Trong đó:

- **\( x \)**: Biến ngẫu nhiên.
- **\( \theta \)**: Bộ tham số của phân phối.
- **\( h(x) \)**: Thước đo cơ sở (base measure), có thể là một hàm phụ thuộc vào \( x \).
- **\( \eta(\theta) \)**: Tham số tự nhiên (natural parameter) của phân phối, là một hàm của \( \theta \).
- **\( T(x) \)**: Thống kê đủ (sufficient statistic), là một hàm của \( x \).
- **\( A(\theta) \)**: Hàm log-normalizer hoặc hằng số chuẩn hóa, đảm bảo rằng phân phối xác suất tích phân trên không gian \( x \) là 1.

## Cấu trúc của Phân phối mũ

- **Thước đo cơ sở \( h(x) \)**: Đây là một hàm của \( x \) không phụ thuộc vào \( \theta \).
- **Tham số tự nhiên \( \eta(\theta) \)**: Thông thường, đây là một hàm tuyến tính của các tham số mô hình \( \theta \).
- **Thống kê đủ \( T(x) \)**: Đây là một hàm của dữ liệu và thường là các đặc trưng quan trọng của dữ liệu mà chúng ta muốn mô hình hóa.
- **Hàm log-normalizer \( A(\theta) \)**: Hàm này đảm bảo rằng \( p(x|\theta) \) là một phân phối xác suất hợp lệ, tức là tích phân của nó trên toàn bộ không gian là 1.

## Ví dụ về Các Phân phối Thuộc Họ Phân Phối Mũ

1. **Phân phối Bernoulli**

Phân phối Bernoulli mô hình hóa một biến nhị phân có giá trị 0 hoặc 1:

\[
p(x|\theta) = \theta^x (1 - \theta)^{1-x}
\]

Trong dạng phân phối mũ:

- \( h(x) = 1 \)
- \( \eta(\theta) = \log\left(\frac{\theta}{1 - \theta}\right) \)
- \( T(x) = x \)
- \( A(\theta) = \log(1 + \exp(\eta(\theta))) \)

2. **Phân phối Gaussian (1 chiều)**

Phân phối Gaussian với trung bình \( \mu \) và phương sai \( \sigma^2 \):

\[
p(x|\mu, \sigma^2) = \frac{1}{\sqrt{2\pi \sigma^2}} \exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right)
\]

Trong dạng phân phối mũ:

- \( h(x) = \frac{1}{\sqrt{2\pi}} \)
- \( \eta(\mu, \sigma^2) = \left(\frac{\mu}{\sigma^2}, -\frac{1}{2\sigma^2}\right) \)
- \( T(x) = (x, x^2) \)
- \( A(\theta) = \frac{\mu^2}{2\sigma^2} + \log(\sigma) \)

3. **Phân phối Poisson**

Phân phối Poisson với tham số \( \lambda \) mô hình hóa số lần xảy ra sự kiện trong một khoảng thời gian cố định:

\[
p(x|\lambda) = \frac{\lambda^x \exp(-\lambda)}{x!}
\]

Trong dạng phân phối mũ:

- \( h(x) = \frac{1}{x!} \)
- \( \eta(\lambda) = \log(\lambda) \)
- \( T(x) = x \)
- \( A(\lambda) = \lambda \)

### Tính chất quan trọng của họ phân phối mũ

- **Tính dễ dàng trong việc tính toán**: Họ phân phối mũ cho phép tính toán các xác suất, kỳ vọng và các đặc trưng khác một cách dễ dàng.
- **Khả năng mô hình hóa đa dạng**: Họ phân phối mũ bao gồm nhiều phân phối phổ biến như Gaussian, Bernoulli, Poisson, và nhiều phân phối khác, làm cho nó rất linh hoạt trong việc mô hình hóa các loại dữ liệu khác nhau.
- **Thống kê đủ**: Họ phân phối mũ có một tính chất quan trọng là thống kê đủ, nghĩa là toàn bộ thông tin về \( \theta \) trong dữ liệu được nắm bắt hoàn toàn bởi \( T(x) \).

### Kết luận

Họ phân phối mũ là một công cụ mạnh mẽ trong thống kê và học máy, cho phép mô hình hóa một cách tổng quát và linh hoạt nhiều loại phân phối xác suất khác nhau. Các phân phối trong họ này thường được sử dụng trong các mô hình xác suất, như VAE, để nắm bắt các đặc trưng quan trọng của dữ liệu trong một dạng tổng quát và dễ xử lý.
