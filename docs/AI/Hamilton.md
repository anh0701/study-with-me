---
layout: default
title: 23.2 Thuật toán đồ thị Hamilton
parent: 23. AI
description: ""
permalink: /hamilton/
has_toc: side_bar 
---

# Thuật toán đồ thị Hamilton

## 1. Xuất phát bài toán

- Bài toán xuất phát từ nhà toán học, ông tạo ra một trò chơi toán học tên là `Icosian Game`. Nhiệm vụ: *đi qua tất cả các đỉnh chỉ một lần* rồi quay về điểm xuất phát.
- Trò chơi này được mô hình hóa bằng đồ thị.

## 2. Định nghĩa bài toán Hamilton

- Trong đồ thị G = (V, E)
- Một **Hamilton Path** là: đường đi qua *tất cả các đỉnh đúng 1 lần*. Ví dụ: `A - B - C - D - E` đi qua mọi đỉnh đúng một lần.
- Nếu đường đi đó *quay lại điểm đầu* thì gọi là **Hamilton Cycle**:

```sh
A — B — C — D — E
|               |
+---------------+
```

- Tổng kết:

| Loại           | Ý nghĩa                          |
| -------------- | -------------------------------- |
| Hamilton Path  | đi qua mọi đỉnh 1 lần            |
| Hamilton Cycle | đi qua mọi đỉnh 1 lần và quay về |

## 3. Cách giải (thuật toán)

- Các cách giải phổ biến:

1. Backtracking

- Ý tưởng: thử mọi đường đi có thể, nếu đi hết đỉnh thì thành công, không thì quay lui

```sh
hamilton(v):
    if visited all vertices:
        return true

    for each neighbor u of v:
        if u chưa visited:
            mark u
            if hamilton(u) return true
            unmark u

    return false
# Độ phức tạp: O(N!), rất lớn
```

2. Dynamic Programming (Held-Karp)

- Dùng bitmask. Độ phức tạp: O(n^2 + 2^n), nhanh hơn brute force

3. Heuristic / Approximation

- Dùng khi đồ thị lớn: greedy, genetic algorithm, simulated annealing.

## 4. Khác gì với các bài toán đồ thị nổi tiếng khác

- So sánh Hamilton với Euler.

|                   | Hamilton            | Euler              |
| ----------------- | ------------------- | ------------------ |
| Đi qua            | **đỉnh**            | **cạnh**           |
| Lặp lại           | không được lặp đỉnh | có thể lặp đỉnh    |
| Điều kiện tồn tại | khó kiểm tra        | có định lý rõ ràng |
| Độ khó            | NP-complete         | dễ hơn             |

- Ví dụ dễ hiểu: Giả sử có 5 thành phố
    - Hamilton: `A - B - C - D - E`
    - Euler: đi qua **mọi con đường** đúng 1 lần

## 5. Ứng dụng thực tế hiện nay

- Logistics: tối ưu giao hàng, xe tải, shipper
- Thiết kế mạch điện: trong VLSI Design, tối ưu đường đi của dây dẫn
- Robot/Drone: Robot phải đi qua tất cả vị trí kiểm tra, tối ưu đường
- Sinh học: Trong Bioinformatics, dùng trong genome assembly, DNA sequencing
- Game AI: NPC phải đi qua toàn bộ map, không lặp vị trí

## 6. Bài toán mã đi tuần

- Là một trường hợp đặc biệt của Hamilton Path
- Bài toán xuất phát từ quân mã trong cờ cua, quy tắc quân mã là đi hình chữ L
- Bài toán trên bàn cơ 8x8: hãy di chuyển quân mã sao cho đi qua tất cả 64 ô đúng 1 lần.
- Ta biến bàn cờ thành đồ thị. Mỗi ô = 1 đỉnh, nước đi của mã = cạnh, nếu mã đi được từ A -> B. Sau đó bài toán trở thành: Tìm đường đi qua tất cả các đỉnh đúng 1 lần. Đây chính là **Hamilton Path**. Nếu yêu cầu quay lại ô xuất phát thì nó trở thành **Hamilton Cycle**

- Cách giải phổ biến:

> **Backtracking**: thử từng bước, nếu mắc kẹt thì quay lui. Đây chính là DFS + backtracking  
> **Warnsdorff's Rule**: ý tưởng là luôn đi tới ô có ít lựa chọn theo nhất, tức là chọn ô có degree nhỏ nhất. Ví dụ từ một vị trí hiện tại, 8 nước đi có thể, chọn ô có ít đường đi tiếp nhất. Lúc này các góc bàn cờ hoặc các cạnh bàn cờ (phần khó nhất) được giải quyết trước, phần còn lại đi rất nhanh.
