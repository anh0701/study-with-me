---
layout: default
title: 7.5 ACID
parent: 07. Database
description: ""
---

<div class="my-right-toc" markdown="1">
1. TOC
{:toc}
</div>

# ACID

## Tính chất

## Những lỗi thường gặp khi dùng ACID

### Dirty Read

#### Bản chất

- Đọc dữ liệu chưa commit của transaction khác.

#### Ví dụ

- T1: update balance = 1000 → 0 (chưa commit)
- T2: đọc thấy = 0
- T1: rollback → thực tế vẫn là 1000

> T2 đã đọc “dữ liệu bẩn” (không tồn tại thật)

#### Nguyên nhân

- Isolation level thấp (READ UNCOMMITTED)
- Không có cơ chế lock/version kiểm soát đọc

#### Hệ quả

- Logic sai hoàn toàn
- Dẫn tới tính toán sai dây chuyền

#### Giải pháp

- Dùng `Read committed` trở lên, DB sẽ không cho đọc dữ liệu chưa commit

### Non-repeatable Read

#### Bản chất

- Cùng 1 query, đọc 2 lần trong cùng transaction ra kết quả khác nhau

#### Ví dụ

- T1: đọc balance = 1000
- T2: update → 2000 + commit
- T1: đọc lại → 2000

> Không repeat được kết quả ban đầu

#### Nguyên nhân

- Transaction khác update + commit giữa hai lần read
- Isolation level: READ COMMITTED

#### Hệ quả

- Logic phụ thuộc "giá trị ổn định" bị sai
- VD: kiểm tra điều kiện trước -> sau không còn đúng

#### Giải pháp

- `REPEATABLE READ`, DB giữ snapshot hoặc lock row

### Phantom Read

#### Bản chất

- Cùng 1 query nhưng số lượng record thay đổi

#### Ví dụ

- T1: SELECT * FROM users WHERE age > 20 trả về 10 rows
- T2: insert thêm 1 user age 25  và commit
- T1: query lại thấy 11 rows

> xuất hiện thêm rows

#### Nguyên nhân

- Transaction khác insert/delete
- Query theo range condition

#### Hệ quả

- Sai logic aggregate (count, sum)

```sh
// T1
total = SELECT SUM(...)  // = 10000

// T2 chen vào
INSERT + COMMIT  // tổng = 15000

// T1 tiếp tục (KHÔNG query lại)
if (total < 12000) {
    INSERT thêm
}

// T1 đang dùng giá trị cũ (10000)
// Nhưng thực tế DB là 15000 (sai điều kiện total < 12000)
// insert thêm sẽ thành 20000
```

- Sai validation (VD: check tồn tại trước khi insert)

```sql
-- T1
SELECT COUNT(*) FROM orders WHERE user_id = 1 AND status = 'PENDING';
-- kết quả = 0 → nghĩ là OK để tạo mới

-- T2 (chạy song song)
INSERT INTO orders(user_id, status) VALUES (1, 'PENDING');
COMMIT;

-- T1 tiếp tục -> Kết quả: có 2 PENDING orders
INSERT INTO orders(user_id, status) VALUES (1, 'PENDING');

```

- Pagination bug

```sql
-- T1
SELECT * FROM products LIMIT 10 OFFSET 0;

-- T2
INSERT thêm product mới lên đầu list

-- T1
SELECT * FROM products LIMIT 10 OFFSET 10;

-- bị trùng item, hoặc miss item, UI hiển thị sai, User thấy dữ liệu nhảy loạn
```

#### Giải pháp

- `SERIALIZABLE`
- Hoặc dùng range lock / MVCC advanced
