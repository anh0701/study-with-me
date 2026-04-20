---
layout: default
title: 27.2 Layout
parent: 27. CSS
description: ""
---

<div class="my-right-toc" markdown="1">
1. TOC
{:toc}
</div>

# Layout

> là kỹ thuật sắp xếp các phần tử HTML thành bộ khung trang web (header, content, footer) bằng các thuộc tính CSS. Các công cụ chính bao gồm Flexbox (bố cục 1 chiều), Grid (bố cục 2 chiều), Position (định vị) và Float. Kiến thức này giúp website hiển thị chuẩn xác, Responsive trên mọi thiết bị.

## 1. Display property

- Quyết định cách phần tử hiển thị (block, inline, inline-block, none)

    - block: chiếm hết hàng
    - inline: nằm trên một hàng
    - inline-block: à sự kết hợp giữa inline và block, cho phép phần tử hiển thị nằm cạnh nhau trên cùng một dòng (như inline) nhưng vẫn có thể tùy chỉnh kích thước width, height, margin, và padding (như block). Nó giúp tạo bố cục ngang, thanh điều hướng (menu), hoặc lưới sản phẩm.

| Đặc điểm | inline | block | inline-block |
| --- | --- | --- | --- |
| Xuống dòng | Không | Có | Không |
| Width/Height | Không áp dụng được | Áp dụng được | Áp dụng được |
| Margin/Padding | Chỉ hỗ trợ trái/phải | Hỗ trợ tất cả | Hỗ trợ tất cả |

### 1.1. inline

- **Không ngắt dòng**: Các phần tử đứng liền kề nhau trên cùng một dòng ngang.
- **Chiều rộng/chiều cao**: width và height không có tác dụng.
- **Padding/Margin**: Chỉ có hiệu quả theo chiều ngang (trái/phải), margin/padding trên/dưới không làm thay đổi bố cục của các dòng khác.
- **Nội dung**: Chỉ bao bọc vừa khít nội dung bên trong (text, ảnh).
- Các phần tử mặc định là inline: `<span>, <a>, <strong>, <em>, <img>, <label>`

### 1.2. block

- **Ngắt dòng**: Luôn bắt đầu trên một hàng mới và đẩy phần tử tiếp theo xuống hàng.
- **Chiều rộng**: Mặc định chiếm toàn bộ chiều rộng của khung nhìn (width: 100%).
- **Kích thước**: Cho phép thiết lập các thuộc tính width, height, margin, và padding đầy đủ.
- Ví dụ phổ biến: Các thẻ `<header>, <footer>, <p>, <h1> - <h6>, <ul>, <div>` đều mặc định là block

### 1.3. inline-block

- **Hiển thị**: Các phần tử nằm trên một hàng, không xuống dòng tự động sau mỗi phần tử.
- **Kích thước**: Có thể thiết lập chiều rộng (width) và chiều cao (height).
- **Khoảng cách**: Hỗ trợ đầy đủ margin và padding (trên, dưới, trái, phải).
- **Mặc định**: Không chiếm toàn bộ chiều rộng của phần tử cha như display: block
- Nên dùng khi nào:
    
    - Tạo **menu/Navigation Bar**: Sắp xếp các thẻ `<a>` hoặc `<li>` nằm ngang hàng nhau.
    - Tạo **Grid/Layout**: Tạo các hộp (box) nội dung nằm cạnh nhau mà không muốn dùng Float hay Flexbox.
    - Nút bấm (**Buttons**): Tạo các nút có kích thước tùy chỉnh nhưng nằm trên cùng một dòng với văn bản.

> Một nhược điểm nhỏ là `inline-block` thường tạo ra khoảng trắng (white-space) giữa các phần tử do xuống dòng trong mã HTML, cần xử lý bằng CSS (font-size: 0 ở phần tử cha) hoặc loại bỏ khoảng trắng trong mã nguồn.

### 1.4. None

- có nhiệm vụ làm cho một phần tử ẩn đi. Khi sử dụng thuộc tính này với giá trị none, nó sẽ làm cho phần tử không còn chiếm không gian hiển thị, giống như nó chưa hề có mặt tại vị trí đó

## 2. Flexbox

- Tối ưu cho bố cục 1 chiều (hàng hoặc cột), giúp căn chỉnh, phân chia không gian giữa các phần tử cực tốt.
- Đặc điểm:
    
    - **Tính linh hoạt**: các thành phần con (flex items) có thể tự co giãn (tăng/giảm kích thước) để lấp đầy không gian trống hoặc thu nhỏ lại để tránh tràn màn hình.
    - **Sắp xếp một chiều (1D)**: hoạt động chủ yếu trên một trục: Trục chính (main axis) và trục phụ (cross axis)
    - **Dễ dàng căn chỉnh**: căn giữa theo cả hai chiều ngang và dọc dễ dàng bằng `justify-content` và a`lign-items`
    - **Thay đổi thứ tự**: có thể thay đổi thứ tự hiển thị của các phần tử mà không cần can thiệp vào mã HTML

- Các thành phần cơ bản:

    - **Flex container (khối cha)**: được thiết lập `display:flex;` hoặc `display: inline-flex;`
    - **Flex items (các phần tử con)**: các thành phần nằm ngay trong container

- Tại sao nên dùng flexbox:

    - **Thay thế float/position**: khắc phục nhược điểm của cách dàn trang truyền thống, giảm thiểu các thủ thuật phức tạp
    - **Responsive tốt**: dễ dàng điều chỉnh bố cục trên các kích thước màn hình khác nhau (điện thoại, máy tính bảng)

- Các thuộc tính phổ biến:

    - cho container: `display, flex-direction, justify-content, align-items, flex-wrap`
    - cho items: `flex-grow, flex-shrink, flex-basis, order`

## 3. CSS Grid

- Mạnh mẽ cho bố cục 2 chiều (cả hàng và cột), cho phép chia website thành các ô lưới cố định.
- Các đặc điểm:

    - **Bố cục hai chiều**: xử lý đồng thời hàng (row) và cột (column)
    - **grid container & items**: gồm một phần tử cha (container) và các phần tử con (items) được sắp xếp bên trong.
    - **sắp xếp linh hoạt**: dễ dàng căn chỉnh, thay đổi vị trí các phần tử mà không cần sửa HTML
    - **Responsive**: hỗ trợ tạo giao diện tương thích tốt trên các thiết bị khác nhau.

- Thuộc tính cơ bản:

    - `display: grid;`: khởi tạo grid container
    - `grid-template-columns`: định nghĩa số lượng và kích thước cột
    - `grid-template-rows`: định nghĩa số lượng và kích thước hàng
    - `gap` (hoặc `grid-gap`): khoảng cách giữa các ô

- So sánh nhanh:

    - **grid (2D)**: dùng cho bố cục tổng thể trang (layout-first)
    - **flexbox (1D)**: dùng cho bố cục thành phần nhỏ, hàng hoặc cột đơn lẻ (content-first)

## 4. Positioning

- Sử dụng position (static, relative, absolute, fixed, sticky) để định vị phần tử tại một điểm cụ thể trên trang.

## 5. Float & Clear

- Kỹ thuật cổ điển để đẩy phần tử sang trái/phải, thường dùng để bọc văn bản quanh hình ảnh.
