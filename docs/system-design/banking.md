---
layout: default
title: 24.3 Hệ thống banking
parent: 24. System Design
description: ""
permalink: /banking/
---

<div class="my-right-toc" markdown="1">
1. TOC
{:toc}
</div>

# Hệ thống banking

## 1. Các bài toán

### Bài toán 1. Bấm “chuyển khoản” nhiều lần khi mạng lỗi nhưng không bị trừ tiền nhiều lần

- Thường là nhờ cơ chế kỹ thuật quan trọng: transaction, Idempotency, core banking, cơ chế hàng đợi (queue)

1. Transaction (ACID)

- Các hệ thống ngân hàng luôn xử lý chuyển tiền như một transaction trong database
- Transaction tuân theo nguyên tắc ACID:

> **Atomicity** - hoặc thực hiện toàn bộ, hoặc không làm gì cả  
> **Consistency** - dữ liệu luôn hợp lệ  
> **Isolation** - transaction không ảnh hưởng nhau  
> **Durability** - khi commit thì dữ liệu không mất

- Ví dụ:

```sh
BEGIN TRANSACTION
  Trừ tiền tài khoản A
  Cộng tiền tài khoản B
COMMIT
```

- Nếu mạng lỗi trước khi commit, transaction bị rollback, nên tiền không bị trừ.

2. Idempotency (chống xử lý trùng)

- Ý tưởng: Cùng một request gửi nhiều lần -> hệ thống chỉ xử lý 1 lần duy nhất.
- Cách làm phổ biến: Client gửi kèm một transaction id / request id. Server kiểm tra id trùng thì không xử lý. Vì vậy bấm nhiều lần cũng không tạo transaction mới.

3. Core Banking kiểm tra trùng giao dịch

- Ngoài API layer, hệ thống core banking còn kiểm tra: transaction_id, timestamp, from_account, amount. Nếu phát hiện duplicate transaction -> reject.

4. Cơ chế hàng đợi (queue)

- Apache Kafka hoặc RabbitMQ đảm bảo: request được xử lý đúng 1 lần, tránh duplicate processing

5. Đôi khi vẫn xảy ra double charge, duplicate transaction, nhưng hệ thống sẽ có reconciliation job phát hiện và hoàn tiền.
