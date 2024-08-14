---
title: Phân Phối Biên/Kết Hợp/Điều Kiện
---
Để hiểu rõ hơn về các khái niệm **phân phối kết hợp (joint distribution)**, **phân phối điều kiện (conditional distribution)**, và **phân phối biên (marginal distribution)**, chúng ta sẽ đi qua từng khái niệm một cách chi tiết cùng với ví dụ minh họa.

### **1. Phân phối kết hợp (Joint Distribution)**

**Phân phối kết hợp** mô tả xác suất của hai hoặc nhiều biến xảy ra đồng thời. Nói cách khác, nó cho biết xác suất của một tập hợp các biến cùng xảy ra.

#### **Công thức**:
- Đối với hai biến ngẫu nhiên \(X\) và \(Y\), phân phối kết hợp được ký hiệu là \(P(X = x, Y = y)\), thể hiện xác suất mà \(X\) nhận giá trị \(x\) và \(Y\) nhận giá trị \(y\) cùng lúc.

#### **Ví dụ**:
- Giả sử bạn đang quan tâm đến xác suất của việc một sinh viên đạt điểm A trong môn Toán và môn Văn. 
  - Gọi \(X\) là điểm Toán và \(Y\) là điểm Văn.
  - Phân phối kết hợp sẽ cho bạn biết xác suất mà một sinh viên có điểm A trong cả hai môn Toán và Văn, ví dụ: \(P(X = A, Y = A)\).

### **2. Phân phối điều kiện (Conditional Distribution)**

**Phân phối điều kiện** mô tả xác suất của một biến xảy ra khi biết trước giá trị của biến khác. Nó cho phép chúng ta tính toán xác suất của một sự kiện dựa trên thông tin đã biết về một sự kiện khác.

#### **Công thức**:
- Phân phối điều kiện của \(Y\) khi biết \(X\) được ký hiệu là \(P(Y = y | X = x)\), thể hiện xác suất mà \(Y\) nhận giá trị \(y\) khi biết rằng \(X\) đã nhận giá trị \(x\).

#### **Ví dụ**:
- Tiếp tục với ví dụ trên, giả sử bạn đã biết rằng một sinh viên đạt điểm A trong môn Toán. Bây giờ, bạn muốn biết xác suất mà sinh viên đó cũng đạt điểm A trong môn Văn.
  - Điều này được thể hiện qua phân phối điều kiện: \(P(Y = A | X = A)\).

### **3. Phân phối biên (Marginal Distribution)**

**Phân phối biên** mô tả xác suất của một biến mà không cần xem xét đến các biến khác. Đây là phân phối của một biến khi chúng ta "gạt bỏ" hoặc "marginalize" các biến khác.

#### **Công thức**:
- Phân phối biên của \(X\) được ký hiệu là \(P(X = x)\), và được tính bằng cách tổng hợp (hoặc tích phân) các giá trị của phân phối kết hợp trên tất cả các giá trị có thể của biến khác, ví dụ \(Y\):
  \[
  P(X = x) = \sum_y P(X = x, Y = y)
  \]

#### **Ví dụ**:
- Nếu bạn chỉ quan tâm đến xác suất mà một sinh viên đạt điểm A trong môn Toán, không quan tâm đến môn Văn, thì phân phối biên sẽ cung cấp thông tin này.
  - Ví dụ, \(P(X = A)\) cho bạn biết xác suất mà một sinh viên đạt điểm A trong môn Toán, không cần xem xét điểm số của môn Văn.

### **Minh họa Bằng Bảng Dữ Liệu Giả Định**

Giả sử bạn có một bảng dữ liệu về điểm số của sinh viên trong hai môn Toán (X) và Văn (Y):

| Toán (X) | Văn (Y) | Số lượng sinh viên |
|----------|---------|-------------------|
| A        | A       | 10                |
| A        | B       | 20                |
| B        | A       | 15                |
| B        | B       | 5                 |

#### **Phân phối kết hợp**:
- \(P(X = A, Y = A)\) = Xác suất một sinh viên đạt điểm A cả trong môn Toán và Văn = \( \frac{10}{50} = 0.2\).

#### **Phân phối điều kiện**:
- \(P(Y = A | X = A)\) = Xác suất một sinh viên đạt điểm A trong môn Văn khi biết rằng sinh viên đó đạt điểm A trong môn Toán = \( \frac{10}{30} = 0.33\).

#### **Phân phối biên**:
- \(P(X = A)\) = Xác suất một sinh viên đạt điểm A trong môn Toán, không xét môn Văn = \( \frac{10 + 20}{50} = 0.6\).

### **Kết Luận**
Ba khái niệm **phân phối kết hợp, điều kiện, và biên** cung cấp các cách khác nhau để mô tả và tính toán xác suất của các biến ngẫu nhiên trong thống kê và học máy. Những khái niệm này là cơ sở cho nhiều thuật toán và phương pháp trong việc xử lý dữ liệu và học máy.