---
layout: default
title: React
parent: 31. Frontend
description: ""
has_toc: side_bar 
---

# React

## 1. Nền tảng Frontend

Hãy tưởng tượng xây dựng một trang web giống như xây nhà.

- **HTML (HyperText Markup Language)**: Là khung xương. Nó xác định cấu trúc: đâu là tiêu đề, đâu là đoạn văn, đâu là nút bấm.
- **CSS (Cascading Style Sheets)**: Là nội thất và sơn tường. Nó quyết định màu sắc, kích thước, vị trí và độ đẹp mắt của ngôi nhà.
- **JavaScript (JS)**: Là hệ thống điện nước. Nó tạo ra sự tương tác: khi bấm công tắc thì đèn sáng, khi mở vòi thì nước chảy.

### Mô hình DOM (Document Object Model)

Khi trình duyệt đọc code HTML của bạn, nó tạo ra một "cây" gọi là DOM. JavaScript sẽ tác động vào cây này để thay đổi nội dung trang web mà không cần tải lại toàn bộ trang.

## 2. Tại sao lại là React?

Khi ứng dụng web trở nên phức tạp, việc quản lý hàng nghìn dòng code JavaScript thuần (Vanilla JS) để cập nhật DOM trở thành một cơn ác mộng. React ra đời với hai triết lý cốt lõi:

- **Component-Based (Dựa trên thành phần)**: Chia nhỏ giao diện thành các mảnh độc lập (như miếng ghép Lego). Bạn có thể tái sử dụng `Button`, `Navbar`, hay `UserCard` ở bất cứ đâu.
- **Declarative (Lập trình khai báo)**: Bạn chỉ cần mô tả giao diện bạn muốn trông như thế nào ở một trạng thái nhất định, React sẽ lo việc cập nhật DOM thật hiệu quả.

## 3. Các khái niệm trong React

## 4. Hooks - Sức mạnh của React hiện đại

## 5. Lộ trình tư duy (Mindset) cho người mới

## 6. Some question

### 1. Trong React, khi nào sẽ ưu tiên dùng useEffect? nêu một ví dụ mà nếu dùng hook này không khéo sẽ dẫn đến tình trạng "infinite loop" (lặp vô tận)

### 2. Giữa việc truyền dữ liệu qua Props và sử dụng Context API, dựa trên tiêu chí nào để quyết định nên dùng cách nào?
