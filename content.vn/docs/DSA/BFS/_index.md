---
title: "Tìm kiếm theo chiều rộng"
---

# BFS (Breadth-First Search): Tìm kiếm theo chiều rộng

## Giới thiệu

BFS (Breadth-First Search) là một trong những thuật toán tìm kiếm trên đồ thị cơ bản nhất, được sử dụng rộng rãi trong khoa học máy tính và AI. Thuật toán này dò tìm tất cả các đỉnh trong một đồ thị theo chiều rộng, bắt đầu từ một đỉnh nguồn ban đầu.

## Đặc điểm chính

1. **Loại đồ thị:** BFS hoạt động tốt trên cả đồ thị hướng và vô hướng.
2. **Dừ liệu chính:** BFS sử dụng hàng đợi (queue) để theo dõi các đỉnh cần dò tìm.
3. **Phạm vi:** Tìm được đường đi ngắn nhất (về số cạnh) trong đồ thị không có trọng số.
4. **Thời gian thực thi:** O(V + E), với V là số đỉnh và E là số cạnh.

## Nguyên tắc hoạt động

1. Bắt đầu từ đỉnh nguồn.
2. Thêm đỉnh đầu tiên vào hàng đợi.
3. Khi hàng đợi không rỗng:
   - Lấy một đỉnh ra khỏi hàng đợi.
   - Đánh dấu đã duyệt.
   - Thêm tất các đỉnh kết nối chưa duyệt vào hàng đợi.

## Giải thuật toán BFS pseudocode

```python
BFS(Graph, start):
    Tạo hàng đợi rỗng queue
    Tạo danh sách visited ban đầu rỗng

    Đẩy start vào queue
    Đánh dấu start là đã duyệt

    while queue không rỗng:
        current = queue.pop()
        Xử lý current

        for each neighbor của current trong Graph:
            if neighbor chưa được duyệt:
                Đẩy neighbor vào queue
                Đánh dấu neighbor là đã duyệt
```

## Ví dụ minh họạ

### Bài toán

Cho một đồ thị:

```
   A
  / \
 B   C
 |   |
 D   E
```

Bắt đầu từ đỉnh `A`, duyệt qua tất cả đỉnh trong đồ thị.

### Input

```text
Graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D'],
    'C': ['A', 'E'],
    'D': ['B'],
    'E': ['C']
}
start = 'A'
```

### Output mong muốn

```text
A -> B -> C -> D -> E
```

### Code C++

```cpp
#include <iostream>
#include <queue>
#include <unordered_map>
#include <vector>
#include <set>
using namespace std;

void BFS(unordered_map<char, vector<char>> &graph, char start) {
    queue<char> q;
    set<char> visited;

    q.push(start);
    visited.insert(start);

    while (!q.empty()) {
        char current = q.front();
        q.pop();
        cout << current << " -> ";

        for (char neighbor : graph[current]) {
            if (visited.find(neighbor) == visited.end()) {
                q.push(neighbor);
                visited.insert(neighbor);
            }
        }
    }
    cout << "End" << endl;
}

int main() {
    unordered_map<char, vector<char>> graph = {
        {'A', {'B', 'C'}},
        {'B', {'A', 'D'}},
        {'C', {'A', 'E'}},
        {'D', {'B'}},
        {'E', {'C'}}
    };

    char start = 'A';
    BFS(graph, start);
    return 0;
}
```

### Output thực tế

```text
A -> B -> C -> D -> E -> End
```

## Ứng dụng thực tế

1. **Xác định đường đi ngắn nhất**: Trong các đồ thị không trọng số như mạng giao thông.
2. **Duyệt web**: Tìm kiếm liên kết trong một cây web.
3. **AI trong game**: Tìm nơi di chuyển ngắn nhất cho nhân vật.

## Kết luận

BFS là một thuật toán đơn giản nhưng đầy sức mạnh, thích hợp cho nhiều bài toán trong khoa học máy tính.
