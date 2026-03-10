---
layout: default
title: 7.1 SQL basic
parent: 07. Database
description: ""
---

# Database

<!-- <details>
<summary>Expand contents</summary>
</details> -->

<details>
<summary><b>SQL là gì? kiến thức cơ bản.</b></summary>

**Mục đích:**
- **Tạo** cơ sở dữ liệu & bảng
- **Thêm / Sửa / Xóa / Tìm kiếm** dữ liệu
- **Phân tích & tổng hợp** dữ liệu

**Các lệnh cơ bản**

| Nhóm | Mục đích            | Ví dụ                                  |
| ---- | ------------------- | -------------------------------------- |
| DDL  | Định nghĩa cấu trúc | `CREATE`, `ALTER`, `DROP`              |
| DML  | Thao tác dữ liệu    | `SELECT`, `INSERT`, `UPDATE`, `DELETE` |
| DCL  | Quyền truy cập      | `GRANT`, `REVOKE`                      |
| TCL  | Transaction         | `COMMIT`, `ROLLBACK`                   |

> Thứ tự thực hiện trong câu lệnh SQL:
>
> **FROM** -> **ON** -> **JOIN** -> **WHERE** -> **GROUP BY** -> **HAVING** -> **SELECT** -> **DISTINCT** -> **ORDER BY** -> **LIMIT/OFFSET(TOP)**

1. SELECT – Truy vấn dữ liệu

```sql
SELECT name, age FROM users WHERE age > 20 ORDER BY age DESC;
```

2. Toán tử & điều kiện

    - So sánh: =, <>, >, <, >=, <=

    - Logic: AND, OR, NOT

    - Template: LIKE, IN, BETWEEN, IS NULL

3. JOIN – Kết nối bảng

    *Các loại join:*

    - INNER JOIN: chỉ lấy trùng

    - LEFT JOIN: lấy tất cả bên trái

    - RIGHT JOIN: lấy tất cả bên phải

    - FULL JOIN: lấy tất cả 2 bên

4. Subquery – Truy vấn lồng

```sql
SELECT name FROM users
WHERE id IN (SELECT user_id FROM orders WHERE amount > 1000);

```

5. View, Index, Function

6. Transaction – Đảm bảo tính toàn vẹn

7. CTE (WITH ... AS)

8. Window Functions (ROW_NUMBER, RANK, OVER(PARTITION BY ...))

9. Stored Procedure & Trigger

10. Optimization (EXPLAIN, Index tuning)

11. SQL vs NoSQL 

</details>

<details>
<summary>explain analyze mysql</summary>

</details>

<details>
<summary>hash table vs hash map</summary>

</details>

<details>
<summary>dùng hash map với trường hợp trường dữ liệu lớn (ví dụ url)</summary>

</details>

<details>
<summary>primary key và foreign key</summary>

</details>

<details>
<summary>Sự khác biệt giữa DELETE, TRUNCATE và DROP</summary>

</details>

<details>
<summary>Trigger là gì ?</summary>

</details>

<details>
<summary>Có những cách nào để tối ưu 1 câu SQL nếu tốc độ truy cập của nó chậm ?</summary>

</details>

<details>
<summary>Sự khác nhau giữa UNIQUE và PRIMARY KEY constraints là gì? </summary>

| SS         | UNIQUE         | PRIMARY KEY                      |
| :----------- | :--------------: | -------------------------: |
| số lượng trong 1 table | nhiều | một  |
| mục đích sử dụng    | đảm bảo tính duy nhất   | đảm bảo tính duy nhất và không được phép NULL |


</details>

<details>
<summary>Sự khác nhau giữa LIKE và IN</summary>

</details>

<details>
<summary>Sự khác nhau giữa HAVING và WHERE </summary>

</details>



