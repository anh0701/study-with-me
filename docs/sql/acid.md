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

### Atomicity (Tính nguyên tử) – "Tất cả hoặc không có gì"

- Trong hóa học, một nguyên tử là đơn vị nhỏ nhất không thể chia tách. Trong database, một Transaction cũng vậy.
- VD: bạn chuyển 1 triệu cho bạn thân, có 2 bước: (1) trừ 1 triệu ở tài khoản bạn, (2) cộng 1 triệu vào tài khoản của bạn thân
- Nếu tính Atomicity được đảm bảo: hoặc là cả hai bước đều thành công, hoặc là không có bước nào xảy ra cả. Không bao giờ có chuyện tiền đã trừ ở máy bạn mà bên kia chưa nhận được. Nếu bước (2) lỗi, hệ thống sẽ Rollback lại trạng thái ban đầu

### Consistency (Tính nhất quán) – "Đúng quy tắc"

- Dữ liệu trước và sau khi giao dịch phải luôn tuân thủ các quy tắc (constraints) đã đặt ra
- VD: Ngân hàng có quy tắc "Số dư tài khoản không được âm"
- Nếu Consistency được đảm bảo: nếu bạn chỉ còn 500k mà cố chuyển 1 triệu, hệ thống sẽ báo lỗi và ngăn giao dịch đó lại để bảo vệ quy tắc "không âm". Sau khi giao dịch (dù thành hay bại), tổng số tiền trong hệ thống phải logic và chính xác

### Isolation (Tính cô lập) – "Việc ai nấy làm"

- Tại một thời điểm, có hàng triệu người cùng giao dịch. Tính cô lập đảm bảo các giao dịch này không "giẫm chân" lên nhau.
- VD: Bạn và vợ/chồng cùng dùng chung một tài khoản có 2 triệu để mua sắm online cùng một lúc
- Nếu Isolation được đảm bảo: Database sẽ xử lý tuần tự hoặc có cơ chế khóa (locking) sao cho giao dịch A không nhìn thấy trạng thái "dang dở" của giao dịch B. Kết quả cuối cùng phải giống như thể hai người thực hiện cách nhau một khoảng thời gian, tránh việc cả hai cùng mua món đồ 2 triêụ mà tài khoản vẫn chỉ trừ 2 triệu

### Durability (Tính bền vững) – "Lưu là lưu luôn"

- Một khi hệ thống đã báo "Giao dịch thành công", thì dữ liệu đó phải được ghi xuống ổ cứng vĩnh viễn
- VD: Ngay giây phút màn hình hiện "Bạn đã chuyển tiền thành công", bỗng nhiên trạm điện nổ, server sập nguồn tối thui
- Nếu tính Durability được đảm bảo: Khi server khởi động lại, giao dịch của bạn vẫn phải nằm đó, không được phép "bay màu" hay mất dấu vết

### Bảng tổng hợp

| Chữ cái | Tính chất | Ý nghĩa ngắn gọn |
| --- | --- | --- |
| A | Atomicity | Thành công cả cụm hoặc thất bại cả cụm. |
| C | Consistency | Không vi phạm quy tắc dữ liệu. |
| I | Isolation | Giao dịch này không làm phiền giao dịch kia. |
| D | Durability | Hệ thống sập thì dữ liệu đã xong vẫn còn đó. |

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
