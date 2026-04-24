---
layout: default
title: 23.4 Backtracking
parent: 23. AI
description: ""
permalink: /backtracking/
has_toc: true
---

# Backtracking

## Bài toán N-Queens

- Cho bàn cờ NxN, đặt N quân hậu (queen) sao cho không có 2 quân hậu nào ăn nhau. Trong cờ vua, quân hậu có thể đi (ngang, dọc, chéo). Vì vậy ta phải đảm bảo: không cùng hàng, không cùng cột, không cùng đường chéo.

## Các cách giải quyết bài toán

1. Brute force: đặt ngẫu nhiên trên bàn cờ, nên số case: 2^(N^2) -> cực lớn.
2. Backtracking: đặt quân hậu từng hàng, nếu sai thì quay lại thử vị trí khác. Độ phức tạp: O(N!)

## Ý tưởng thuật toán

```sh
solve(row):

    if row == N
        print solution
        return

    for col = 0 -> N-1

        if valid(row, col)

            place queen

            solve(row + 1)

            remove queen   // backtrack
```

## Ứng dụng

| Bài toán       | Ý nghĩa                   |
| -------------- | ------------------------- |
| Sudoku solver  | giải sudoku               |
| Graph coloring | tô màu đồ thị             |
| Hamilton path  | tìm đường đi qua mọi đỉnh |
| Maze solving   | tìm đường trong mê cung   |
| N-Queens       | tối ưu ràng buộc          |
