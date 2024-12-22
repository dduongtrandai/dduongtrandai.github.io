---
weight: 1
bookCollapseSection: true
title: "Đồ thị"
---

**Tổng quan về Đồ Thị trong Cấu trúc Dữ liệu và Giải thuật**

Trong lĩnh vực Cấu trúc Dữ liệu và Giải thuật, đồ thị (“Graph”) là một trong những khái niệm cốt lõi, đóng vai trò quan trọng trong việc biểu diễn các mối quan hệ và tương tác trong các hệ thống phức tạp.

### 1. Định nghĩa Đồ Thị

Đồ thị là một cặp gồm hai tập hợp:

- **Tập đỉnh (Vertices)**: Đại diện cho các điểm (nodes) trong đồ thị.
- **Tập các cạnh (Edges)**: Biểu diễn các mối quan hệ hoặc kết nối giữa hai đỉnh.

Các cạnh có thể có hướng (directed graph) hoặc không có hướng (undirected graph).

### 2. Đặc điểm chính

- **Có định hướng hay không**: Đồ thị đơn (simple graph), đồ thị có hướng (directed graph).
- **Có trọng số hay không**: Trọng số (“weight”) biểu thị độ lớn mối quan hệ hoặc chi phí của cạnh.
- **Tính liên thông**: Đồ thị liên thông khi tất cả các đỉnh có thể kết nối với nhau qua các cạnh.

### 3. Các loại Đồ Thị thường gặp

1. **Đồ thị đơn (Simple Graph)**: Các cạnh không lắp lại, không tự kết nối.
2. **Đồ thị có hướng (Directed Graph)**: Các cạnh có hướng, thể hiện mối quan hệ đơn chiều.
3. **Đồ thị có trọng số (Weighted Graph)**: Cạnh được gán trọng số.
4. **Đồ thị lưỡng (Dense Graph)**: Số cạnh rất lớn so với số đỉnh.
5. **Đồ thị thưa (Sparse Graph)**: Số cạnh nhỏ so với số đỉnh.

### 4. Ứng dụng thực tiễn

- **Hệ thống mạng (Networks)**: Biểu diễn các mạng máy tính, các tuyến kết nối trong Internet.
- **Giao thông vận tải**: Đồ thị biểu diễn hệ thống giao thông, các tuyến đường và trạm dừng.
- **Khoa học dữ liệu**: Phân tích mạng xã hội, quan hệ giữa các đối tượng trong một hệ sinh thái.
- **AI và Machine Learning**: Dụng trong các bài toán như Recommendation System, PageRank.

### 5. Các giải thuật quan trọng

- **Tìm kiếm trong đồ thị**:
  - BFS (Breadth-First Search)
  - DFS (Depth-First Search)
- **Tính đường đi ngắn nhất**:
  - Dijkstra
  - Bellman-Ford
  - Floyd-Warshall
- **Tính cây khung tối thiểu**:
  - Kruskal
  - Prim

### Kết luận

Hiểu rõ đồ thị giúp chúng ta đề ra các giải pháp hiệu quả cho những vấn đề phức tạp trong khoa học, kỹ thuật và cuộc sống hàng ngày. Đóng vai trò như là nền tảng cho nhiều giải thuật quan trọng, đồ thị chính là một lĩnh vực đáng để khảo sâu trong Cấu trúc Dữ liệu và Giải thuật.
