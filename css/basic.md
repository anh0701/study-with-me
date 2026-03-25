---
layout: default
title: 27.1 CSS basic
parent: 27. CSS
description: ""
---

# CSS basic

## 1. Selectors

- **CSS Selectors**: là các mẫu dùng để tìm và chọn các phần tử HTML cần định dạng kiểu dáng (style).

- Selector cơ bản:

    - **Universal Selector (*)**: Chọn tất cả phần tử.
    - **Type Selector (element)**: Chọn theo tên thẻ HTML (ví dụ: `p`, `h1`, `div`).
    - **Class Selector (.className)**: Chọn các phần tử có thuộc tính class xác định (dùng dấu `. trước tên class`).
    - **ID Selector (#idName)**: Chọn một phần tử duy nhất có thuộc tính ID xác định (dùng dấu `# trước tên id`).

- Selector kết hợp (**Combinator**):

    - **Descendant (A B)**: Chọn phần tử B nằm trong phần tử A.
    - **Child (A > B)**: Chọn phần tử B là con trực tiếp của phần tử A.
    - **Adjacent Sibling (A + B)**: Chọn phần tử B ngay sau phần tử A.

- **Pseudo-classes (:state)**: Chọn phần tử dựa trên trạng thái (ví dụ: `:hover`, `:focus`, `:nth-child()`).
- **Pseudo-elements (::part)**: Chọn và tạo kiểu cho một phần cụ thể của phần tử (ví dụ: `::before`, `::after`, `::first-line`).
- **Attribute Selector ([attr])**: Chọn phần tử dựa trên thuộc tính hoặc giá trị thuộc tính (ví dụ: `[type="text"]`, `[href]`).

## 2. Color & Typography

### 2.1 Color Properties

- Thuộc tính chính để định màu cho văn bản là `color`, trong khi `background-color` được dùng để thiết lập màu nền. Có nhiều cách set màu.
- **Tên màu**: Sử dụng các tên màu định sẵn như *red, blue, green, lightgray*
- **Mã Hexadecimal**: Sử dụng mã 6 chữ số thập lục phân, ví dụ: `#FF0000 (đỏ)`, `#000000 (đen)`. Có thể dùng dạng viết tắt 3 chữ số cho các mã lặp lại (ví dụ: `#fff cho #ffffff`).
- **Giá trị RGB/RGBA**: Sử dụng hàm `rgb(red, green, blue)` hoặc `rgba(red, green, blue, alpha)`. Kênh alpha (từ 0 đến 1) kiểm soát độ trong suốt.
- **Giá trị HSL/HSLA**: Sử dụng hàm `hsl(hue, saturation, lightness)` hoặc `hsla(...)` để định nghĩa màu sắc

### 2.2 Typography Properties

- Typography trong CSS bao gồm các thuộc tính kiểm soát phông chữ, kích thước, trọng lượng và khoảng cách để đảm bảo văn bản dễ đọc và có tính thẩm mỹ.
- **font-family**: Xác định phông chữ ưu tiên để sử dụng. Nên cung cấp một danh sách các phông chữ dự phòng, kết thúc bằng một họ phông chữ chung (ví dụ: `serif`, `sans-serif`) để trình duyệt có thể chọn font phù hợp nếu font đầu tiên không khả dụng. Bạn cũng có thể sử dụng `Google Fonts` để có thêm nhiều lựa chọn phông chữ.
- **font-size**: Kiểm soát kích thước của văn bản, thường được xác định bằng `pixel (px)`, đơn vị tương đối `em` hoặc `rem`, hoặc các giá trị định sẵn (`small`, `large`).
- **font-weight**: Đặt độ đậm hoặc mỏng của chữ (ví dụ: `normal`, `bold`, `bolder`, hoặc giá trị số từ `100` đến `900`).
- **font-style**: Thường được dùng để xác định văn bản in nghiêng (`italic`, `oblique`) hoặc bình thường (`normal`).
- **line-height**: Điều chỉnh khoảng cách dọc giữa các dòng văn bản (dãn dòng).
- **letter-spacing**: Kiểm soát khoảng cách giữa các chữ cái.
- **text-align**: Căn chỉnh văn bản theo chiều ngang (ví dụ: `left`, `right`, `center`, `justify`).
- **text-decoration**: Thêm các đường kẻ vào văn bản (ví dụ: `underline`, `overline`, `line-through`, `none`).

## 3. The Box Model
