---
layout: default
title: 7.1 SQL basic
parent: 07. Database
description: ""
---

# Database

## 1. SQL là gì? kiến thức cơ bản

- **Mục đích:**

    - **Tạo** cơ sở dữ liệu & bảng
    - **Thêm / Sửa / Xóa / Tìm kiếm** dữ liệu
    - **Phân tích & tổng hợp** dữ liệu

- **Các lệnh cơ bản**

| Nhóm | Mục đích            | Ví dụ                                  |
| ---- | ------------------- | -------------------------------------- |
| DDL  | Định nghĩa cấu trúc | `CREATE`, `ALTER`, `DROP`              |
| DML  | Thao tác dữ liệu    | `SELECT`, `INSERT`, `UPDATE`, `DELETE` |
| DCL  | Quyền truy cập      | `GRANT`, `REVOKE`                      |
| TCL  | Transaction         | `COMMIT`, `ROLLBACK`                   |

> Thứ tự thực hiện trong câu lệnh SQL:
>
> **FROM** -> **ON** -> **JOIN** -> **WHERE** -> **GROUP BY** -> **HAVING** -> **SELECT** -> **DISTINCT** -> **ORDER BY** -> **LIMIT/OFFSET(TOP)**

### 1.1. SELECT – Truy vấn dữ liệu

```sql
SELECT name, age FROM users WHERE age > 20 ORDER BY age DESC;
```

### 1.2. Toán tử & điều kiện

- So sánh: =, <>, >, <, >=, <=

- Logic: AND, OR, NOT

- Template: LIKE, IN, BETWEEN, IS NULL

### 1.3. JOIN – Kết nối bảng

- *Các loại join:*

    - INNER JOIN: chỉ lấy trùng

    - LEFT JOIN: lấy tất cả bên trái

    - RIGHT JOIN: lấy tất cả bên phải

    - FULL JOIN: lấy tất cả 2 bên

### 1.4. Subquery – Truy vấn lồng

```sql
SELECT name FROM users
WHERE id IN (SELECT user_id FROM orders WHERE amount > 1000);

```

### 1.5. View, Index, Function

### 1.6. Transaction – Đảm bảo tính toàn vẹn

### 1.7. CTE (WITH ... AS)

### 1.8. Window Functions (ROW_NUMBER, RANK, OVER(PARTITION BY ...))

### 1.9. Stored Procedure & Trigger

### 1.10. Optimization (EXPLAIN, Index tuning)

### 1.11. SQL vs NoSQL

## 2. explain analyze mysql

## 3. hash table vs hash map

- dùng hash map với trường hợp trường dữ liệu lớn (ví dụ url)

## 4. primary key và foreign key

## 5. Sự khác biệt giữa DELETE, TRUNCATE và DROP

## 6. Trigger là gì ?

## 7. Có những cách nào để tối ưu 1 câu SQL nếu tốc độ truy cập của nó chậm ?

## 8. Sự khác nhau giữa UNIQUE và PRIMARY KEY constraints là gì?

| SS         | UNIQUE         | PRIMARY KEY                      |
| :----------- | :--------------: | -------------------------: |
| số lượng trong 1 table | nhiều | một  |
| mục đích sử dụng    | đảm bảo tính duy nhất   | đảm bảo tính duy nhất và không được phép NULL |

## 9. Sự khác nhau giữa LIKE và IN

## 10. Sự khác nhau giữa HAVING và WHERE
