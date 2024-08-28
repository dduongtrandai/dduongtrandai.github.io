---
title: "Log-likelihood"
---

**Log-likelihood** là một khái niệm cơ bản trong thống kê và học máy, được sử dụng để đo lường mức độ khớp của một mô hình xác suất với dữ liệu quan sát. Nó là logarit của **likelihood**, một giá trị biểu diễn xác suất rằng dữ liệu quan sát được sinh ra từ mô hình với các tham số đã cho.

## 1. **Likelihood là gì?**
   - **Likelihood** của một tập dữ liệu \( \mathbf{X} = \{x_1, x_2, \ldots, x_n\} \) dưới một mô hình với tham số \( \theta \) là xác suất của dữ liệu đó khi biết các tham số:
     \[
     L(\theta|\mathbf{X}) = p(\mathbf{X}|\theta) = \prod_{i=1}^{n} p(x_i|\theta)
     \]
   - Trong đó, \( p(x_i|\theta) \) là xác suất của mẫu dữ liệu \( x_i \) dưới mô hình với tham số \( \theta \).

## 2. **Log-Likelihood:**
   - **Log-likelihood** là logarit tự nhiên của likelihood. Log-likelihood thường được sử dụng thay vì likelihood trực tiếp bởi vì:
     - Logarit chuyển phép nhân thành phép cộng, điều này đơn giản hóa các tính toán, đặc biệt là khi làm việc với các sản phẩm của xác suất.
     - Log-likelihood có thể được tối đa hóa dễ dàng hơn trong các bài toán tối ưu.
   - Công thức log-likelihood là:
     \[
     \ell(\theta|\mathbf{X}) = \log L(\theta|\mathbf{X}) = \log \left( \prod_{i=1}^{n} p(x_i|\theta) \right) = \sum_{i=1}^{n} \log p(x_i|\theta)
     \]
   - Ở đây, \( \ell(\theta|\mathbf{X}) \) là log-likelihood của tham số \( \theta \) cho tập dữ liệu \( \mathbf{X} \).

## 3. **Sử dụng log-likelihood trong học máy:**
   - **Tối đa hóa log-likelihood**: Trong nhiều bài toán học máy, ta thường tìm các tham số \( \theta \) của mô hình sao cho log-likelihood đạt giá trị lớn nhất. Quá trình này gọi là **Maximum Likelihood Estimation (MLE)**.
     - Ví dụ: Trong hồi quy logistic, ta tối đa hóa log-likelihood để tìm các trọng số của mô hình.
   - **Thích hợp với các mô hình xác suất**: Log-likelihood cho phép ta định lượng mức độ khớp của một mô hình với dữ liệu thực tế, từ đó điều chỉnh các tham số của mô hình cho phù hợp hơn.

## 4. **Ví dụ cụ thể:**

   - **Hồi quy logistic**:
     - Với hồi quy logistic, \( p(x|\theta) \) là xác suất dự đoán đầu ra đúng khi biết đầu vào và các tham số \( \theta \) của mô hình.
     - Log-likelihood sẽ được tối đa hóa để tìm các tham số \( \theta \) sao cho mô hình dự đoán chính xác nhất có thể.

   - **Gaussian Distribution**:
     - Nếu \( x_i \) được giả định tuân theo phân phối Gaussian với trung bình \( \mu \) và phương sai \( \sigma^2 \), log-likelihood sẽ có dạng:
       \[
       \ell(\mu, \sigma^2 | \mathbf{X}) = -\frac{n}{2} \log(2\pi\sigma^2) - \frac{1}{2\sigma^2} \sum_{i=1}^{n} (x_i - \mu)^2
       \]
     - Ở đây, \( \theta = (\mu, \sigma^2) \) và ta có thể tối đa hóa log-likelihood để tìm các giá trị \( \mu \) và \( \sigma^2 \) tốt nhất.

## Kết luận:

Log-likelihood là một công cụ mạnh mẽ trong thống kê và học máy, cho phép định lượng mức độ khớp của mô hình với dữ liệu và tối ưu hóa các tham số của mô hình một cách hiệu quả. Nó là nền tảng của nhiều phương pháp và thuật toán trong học máy, từ hồi quy đến các mô hình xác suất phức tạp như VAE.