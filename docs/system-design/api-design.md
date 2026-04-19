---
layout: default
title: 24.2 Thiết kế API
parent: 24. System Design
description: ""
permalink: /api-design/
---

# Thiết kế API

- Đặc tính của API tốt: rõ ràng, nhất quán, dễ hiểu, tách biệt tài nguyên.
- Tổ chức API xoay quanh các tài nguyên (danh từ), thay vì các hành động (động từ).
- Đặt version cho API
- Sử dụng phân trang
- Idemotency-Key

- Ví dụ:

| Hành động | Endpoint API |
| --- | --- |
| Lấy tất cả bài đăng | GET /v1/posts |
| Tạo một bài đăng mới | POST /v1/posts |
| Bình luận vào bài đăng | POST /v1/posts/{id}/comments |
| Thích một bài đăng | POST /v1/posts/{id}/likes |
| Tải feed người dùng | GET /v1/users/{id}/feed?limit=20 |
