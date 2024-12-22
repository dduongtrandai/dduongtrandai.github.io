---
title: "Tìm kiếm tuyến tính"
---

**Tìm Kiếm Tuyến Tính (Linear Search): Cách Thức Hoạt Động, Đặc Điểm, và Ví Dụ**

Tìm kiếm tuyến tính (“Linear Search”) là một trong những thuật toán tìm kiếm cơ bản nhất trong lĩnh vực khoa học máy tính. Cách thức hoạt động rất đơn giản: duyệt qua từng phần tử trong danh sách một cách tần tự cho đến khi tìm thấy phần tử mong muốn hoặc duyệt hết danh sách.

---

### 1. Cách Thức Hoạt Động

Tìm kiếm tuyến tính được thực hiện bằng việc so sánh phần tử cần tìm (“key”) với từng phần tử trong danh sách, theo trình tự từ đầu đến cuối:

1. Bắt đầu từ phần tử đầu tiên trong danh sách.
2. So sánh phần tử hiện tại với key.
3. Nếu khớp, thuật toán kết thúc và trả về vị trí.
4. Nếu không khớp, chuyển đến phần tử tiếp theo.
5. Lặp lại bước 2 đến khi tìm thấy hoặc hết danh sách.
6. Nếu duyệt hết danh sách mà không tìm thấy, thuật toán trả về giá trị cho biết key không có trong danh sách.

---

### 2. Đặc Điểm Của Tìm Kiếm Tuyến Tính

#### **Ưu Điểm**

- Dễ hiểu, dễ triển khai.
- Hoạt động trên mọ̣i kiểu dữ liệu: danh sách có sắp xếp hay không.
- Phù hợp với danh sách nhỏ.

#### **Nhược Điểm**

- Thời gian thực thi chậm khi danh sách lớn (độ phức tạp O(n)).
- Không tối ưu cho tìm kiếm nhiều phần tử lặp lại.

---

### 3. Giải Thuật

Dưới đây là mã giải thuật tìm kiếm tuyến tính bằng Python:

```python
# Thuật toán Linear Search

def linear_search(arr, key):
    for i in range(len(arr)):
        if arr[i] == key:
            return i  # Trả về vị trí khi tìm thấy
    return -1  # Trả về -1 nếu không tìm thấy

# Ví dụ
array = [10, 20, 30, 40, 50]
key = 30

result = linear_search(array, key)

if result != -1:
    print(f"Phần tử {key} được tìm thấy tại vị trí {result}.")
else:
    print(f"Phần tử {key} không có trong danh sách.")
```

---

### 4. Ví Dụ Minh Họa

#### **Danh sách Dữ Liệu**: `[7, 14, 21, 28, 35]`

#### **Key Cần Tìm**: `28`

1. So sánh `7` với `28` (định rõ không khớp).
2. So sánh `14` với `28` (định rõ không khớp).
3. So sánh `21` với `28` (định rõ không khớp).
4. So sánh `28` với `28` (định rõ khôp).
5. Trả về vị trí `3`.

Kết quả: Phần tử `28` được tìm thấy tại vị trí `3` trong danh sách.

---

### 5. Khi Nào Sử Dụng Tìm Kiếm Tuyến Tính?

Tìm kiếm tuyến tính thường được sử dụng trong các trường hợp sau:

- Danh sách nhỏ hoặc không sắp xếp.
- Tìm kiếm nhanh chóng trong danh sách không có đòi hỏi tính tối ưu.
- Duyệt danh sách để tìm tất cả các phần tử thoả mãn một điều kiện (tìm nhiều phần tử).

---

### 6. Kết Luận

Tìm kiếm tuyến tính là một thuật toán quan trọng, dù đơn giản, nhưng vẫn là nền tảng cho nhiều thuật toán tìm kiếm phức tạp khác. Cách thức này hiệu quả với danh sách nhỏ hoặc không đòi hỏi tính tối ưu cao.
