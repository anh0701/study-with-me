---
layout: default
title: 18. Web Servers
description: ""
---

<div class="my-right-toc" markdown="1">
1. TOC
{:toc}
</div>

# Web Servers

> Hãy tưởng tượng bạn đang đi vào một nhà hàng:  
> 1. Bạn (**Client/Trình duyệt**): Người gọi món.   
> 2. Menu (**URL/Địa chỉ web**): Danh sách những thứ nhà hàng có.  
> 3. Người phục vụ (**Web Server**): Người tiếp nhận yêu cầu, vào bếp lấy món và mang ra tận bàn cho bạn.

## 1. Web Server thực chất là gì?

- **Về phần cứng**: Nó là một máy tính vật lý (thường rất mạnh) lưu trữ các file thành phần của một trang web (như ảnh, văn bản, file HTML, CSS, JavaScript). Nó kết nối với Internet để trao đổi dữ liệu.

- **Về phần mềm**: Nó là một chương trình máy tính kiểm soát cách người dùng truy cập vào các file đó. Nó hiểu được các yêu cầu gửi đến qua giao thức HTTP (giao thức truyền tải siêu văn bản).

## 2. Quy trình hoạt động

- Khi bạn gõ `google.com` và nhấn Enter, quy trình sẽ diễn ra như sau:

1. **Gửi yêu cầu**: Trình duyệt của bạn gửi một yêu cầu đến Web Server thông qua địa chỉ IP của nó.
2. **Xử lý**: Web Server nhận yêu cầu, nó tìm kiếm trong "kho lưu trữ" của mình xem file bạn cần nằm ở đâu.
3. **Phản hồi**:
    - Nếu thấy: Nó gửi file đó về cho trình duyệt.
    - Nếu không thấy: Nó gửi về một thông báo lỗi (ví dụ lỗi 404 Not Found).
4. **Hiển thị**: Trình duyệt nhận file và vẽ lên màn hình giao diện đẹp đẽ mà bạn thấy

## 3. Các loại Web Server phổ biến hiện nay

| Tên Server | Đặc điểm chính |
| --- | --- |
| Apache | Lâu đời, ổn định, cực kỳ phổ biến và dễ tùy biến. |
| Nginx | Tốc độ rất nhanh, chịu được lượng người truy cập lớn cùng lúc, hiện đang rất được ưa chuộng. |
| IIS | Sản phẩm của Microsoft, chuyên dùng cho các hệ thống chạy Windows. |
