---
title: "Tìm kiếm theo chiều sâu"
---

# DFS (Depth-First Search) trong Cấu Trúc Dữ Liệu và Giải Thuật

DFS (Depth-First Search) là một trong những thuật toán duyệt (traverse) trong các cấu trúc dữ liệu đồ thị (graph). Thuật toán này bắt đầu từ một đỉnh điểm, duyệt theo chiều sâu trên một nhánh trước khi quay lại các nhánh khác.

DFS thường được sử dụng trong các bài toán:

1. Kiểm tra tính liên thông của đồ thị.
2. Tìm đường đi trong ma trận hoặc đồ thị.
3. Xác định các thanh phần liên thông trong đồ thị.
4. Giải quyết bài toán định lộ (backtracking).

## Nguyên lý hoạt động

DFS sử dụng một trong hai cách triển khai:

- **Đẫy đệ quy (Recursion):** Sử dụng stack của hàm gọi.
- **Stack thủ công:** Triển khai bằng cách tự quản lý stack.

Thuật toán hoạt động như sau:

1. Bắt đầu từ đỉnh ban đầu.
2. Đánh dấu đỉnh này đã được thăm.
3. Thăm tất cả các đỉnh kết nối chưa được thăm theo chiều sâu.
4. Quay lại các đỉnh khác khi không thể thăm sâu hơn.

## Mã Giải Thích

Dưới đây là mã C++ triển khai DFS bằng đệ quy:

```cpp
#include <iostream>
#include <vector>
using namespace std;

void DFS(int u, vector<vector<int>>& adj, vector<bool>& visited) {
    cout << u << " "; // In đỉnh vừa thăm
    visited[u] = true;

    for (int v : adj[u]) {
        if (!visited[v]) {
            DFS(v, adj, visited);
        }
    }
}

int main() {
    int n = 6; // Số đỉnh
    vector<vector<int>> adj(n);

    // Thêm các cạnh vào danh sách kết nối
    adj[0] = {1, 2};
    adj[1] = {0, 3, 4};
    adj[2] = {0};
    adj[3] = {1, 5};
    adj[4] = {1};
    adj[5] = {3};

    vector<bool> visited(n, false);

    cout << "DFS traversal: ";
    DFS(0, adj, visited); // Duyệt từ đỉnh 0

    return 0;
}
```

### Kết Quả

Nếu bạn chạy đoạn mã trên, đầu ra sẽ là:

```
DFS traversal: 0 1 3 5 4 2
```

### Giải Thích

1. Bắt đầu từ đỉnh `0`.
2. Duyệt theo chiều sâu: đi từ `0 -> 1 -> 3 -> 5`.
3. Quay lại và thăm đỉnh `4`, sau đó là `2`.

## Ưu Điểm và Nhược Điểm

### Ưu Điểm

1. **Dễ triển khai:** DFS có thể được triển khai dễ dàng bằng đệ quy hoặc stack.
2. **Tính tiết kiệm:** DFS sử dụng bộ nhớ ít hơn BFS trong đồ thị lớn nếu đường đi ngắn.

### Nhược Điểm

1. **Dễ rơi vào vòng lặp:** Nếu không có các biện pháp đánh dấu, DFS có thể duyệt lại các đỉnh đã thăm.
2. **Khó điều chỉnh:** DFS không thích hợp tìm đường ngắn nhất trong đồ thị có trọng số.

## Kết Luận

DFS là một thuật toán mạnh mẽ, hữu ích trong nhiều bài toán đòi hỏi duyệt sâu vào từng ngóc ngách của đồ thị. Tuy nhiên, nó cần được sử dụng thận trọng trong các bài toán lớn hoặc đồ thị có vòng để tránh vòng lặp vô tận.
