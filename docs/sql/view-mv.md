---
layout: default
title: 7.4 View vs Materialized View
parent: 07. Database
description: ""
has_toc: side_bar 
---

# View vs Materialized View

> Một query JOIN 5 bảng chạy 3 giây -> giảm còn 30ms mà không cần sửa code backend?

## 1. Khái niệm

1. View: là một "query được đặt tên", không lưu dữ liệu
2. Materialized View: là "query được tính trước", lưu kết quả thành một bảng
3. Ứng dụng: Tăng tóc báo cáo và analytics cho hệ thống read-heavy.

| Tính năng | View | Materialized View |
| --- | --- | --- |
| Lưu dữ liệu | Không | Có |
| Tốc độ truy vấn | Chậm | Cực nhanh |
| Cần làm mới | Không | Có |
| Tối ưu hiệu suất | Không | Rất mạnh |

## 2. Ưu/Nhược điểm của Materialized View

- Ưu điểm:

    - Tăng tốc query cực lớn (vd: 3s -> 30s)
    - Giảm tải cho cơ sở dữ liệu
    - Hoàn hảo cho dashboard & analytics
    - Không cần thay đổi code ứng dụng

- Nhược điểm:

    - Dữ liệu không real-time, cần làm mới
    - Phù hợp cho dữ liệu ít thay đổi
    - Quá trình làm mới có thể tốn kém
    - Không phải CSDL nào cũng hỗ trợ

## 3. Khi nào nên dùng?

- Nên dùng khi:

    - Dashboard & Analytics
    - Báo cáo định kỳ (ngày, tuần, tháng)
    - Hệ thống read-heavy (đọc nhiều)
    - Query phức tạp (nhiều JOINs, tổng hợp)

- Không nên dùng khi:

    - Cần dữ liệu real-time tuyệt đối
    - Dữ liệu thay đổi liên tục (ghi nhiều)
    - Logic cần phân tán (microservices)
    - Muốn tránh quản lý việc làm mới
