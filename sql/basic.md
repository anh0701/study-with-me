---
layout: default
title: 22. SQL
nav_order: 2
description: ""
---

# Tối ưu câu lệnh truy vấn

1. Chỉ SELECT những cột cần thiết: thay vì SELECT * thì chỉ SELECT các cột cần thiết để giảm lượng data truyền về, giảm chi phí CPU/mạng.
2. Dùng index đúng chỗ
   
   - trên cột WHERE, JOIN, ORDER BY, GROUP BY
   - đặt index cho các câu lệnh truy vấn nặng, lặp lại nhiều lần
   - tránh đặt index cho cột thường xuyên thay đổi (cột thường thay đổi => đánh index bảng lại nhiều lần)
   - index nhiều quá sẽ làm chậm INSERT, UPDATE, DELETE, vì phải đánh lại index bảng.
3. Tránh dùng hàm lên cột được đánh index trong WHERE (trừ khi DB hỗ trợ function-based index): thay vì dùng YEAR(created_date) = 2024 thì ghi là created_date >= ... and ....<= .... vì dùng hàm thì sẽ tính toán hàm trước ( sẽ quét toàn bộ bảng => mất hiệu lực của index)
4. Dùng LIMIT để phân trang hoặc giới hạn kết quả
5. Join đúng kiểu, đúng điều kiện
6. Tránh subquery lồng quá sâu, dùng JOIN thay
7. Dùng các bảng tạm / materialized view nếu truy vấn nặng
8. Tránh OR trong WHERE dùng UNION ALL nếu được
9. Luôn kiểm tra bằng EXPLAIN/ EXPLAIN ANALYST
10. Dùng Catching nếu truy vấn lặp lại nhiều lần
