---
layout: default
title: 24.1 Chuỗi Markov
parent: 24. AI
description: ""
permalink: /markov-chain/
---

## Khái niệm

- Xác suất trạng thái tiếp theo chỉ phụ thuộc vào trạng thái hiện tại, không phụ thuộc vào quá khứ trước đó.

## Ý tưởng

- Giả sử hệ thống thời tiết với 3 trạng thái: Sunny, Cloudy, Rainy  

Ví dụ:

| Hôm nay | Ngày mai   |
| ------- | ---------- |
| Sunny   | 70% Sunny  |
| Sunny   | 20% Cloudy |
| Sunny   | 10% Rainy  |

- Nếu hôm nay là Sunny, xác suất ngày mai chỉ phụ thuộc Sunny, không cần biết hôm kia là gì.
- Từ đó ta có ma trận chuyển trạng thái như sau:

$$
P = \begin{bmatrix}
0.7 & 0.2 & 0.1 \\
0.3 & 0.4 & 0.3 \\
0.2 & 0.5 & 0.3
\end{bmatrix}
$$

- Mỗi hàng = xác suất chuyển từ trạng thái hiện tại sang trạng thái khác

## Mô hình toán học

- chuỗi Markov là một dãy biến ngẫu nhiên: 

$$ X_0, X_1, X_2, ...$$

thỏa mãn:

$$P(X_{n+1} = x \mid X_n, X_{n-1}, \dots, X_0) = P(X_{n+1} = x \mid X_n)$$

Nghĩa là: Quá khứ không quan trọng - chỉ trạng thái hiện tại quyết định tương lai

## Ví dụ

- Người dùng website có trạng thái truy cập: Home, Product, Checkout, Exit

| From    | To       | Probability |
| ------- | -------- | ----------- |
| Home    | Product  | 0.6         |
| Home    | Exit     | 0.4         |
| Product | Checkout | 0.3         |
| Product | Home     | 0.5         |
| Product | Exit     | 0.2         |

- Mô hình này sẽ giúp dự đoán: người dùng có mua hàng không, họ sẽ rời website khi nào

## Ứng dụng

- Search Engine (Page Rank)
    - Ý tưởng: mỗi trang web là một trạng thái, link là xác suất chuyển
    - Trang nào có nhiều link từ trang quan trọng -> rank cao

- NLP (Xử lý ngôn ngữ tự nhiên):
    - text prediction
    - language modeling
    - autocomplete
- Speech Recognition (Nhận dạng giọng nói dùng mô hình Hidden Markov Model): Siri, Google Speech, Alexa
- Finace: dùng để mô hình biến động giá cổ phiếu, thị trường bull/bear
- Robotics & AI: 
    - Robot dùng Markov để định vị (localization), lập kế hoạch đường đi
    - Ví dụ: robot vacuum xác suất chuyển sang ô khác
- Biology: ứng dụng trong phân tích DNA, gene prediction 
- Gợi ý gõ từ của bàn phím

