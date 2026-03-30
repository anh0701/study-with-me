---
layout: default
title: 27.3 Responsive Design
parent: 27. CSS
description: ""
---

# Responsive Design

## 1. Media Queries

### 1. Khái niệm

- dùng để thay đổi giao diện theo kích thước màn hình hoặc thiết bị

### 2. Cú pháp cơ bản

```css
@media (điều_kiện) {
  /* CSS áp dụng khi điều kiện đúng */
}

/* 
VD:
- Nếu màn hình <= 768px (tablet/mobile)
- Thì nền sẽ chuyển sang màu đỏ
*/
@media (max-width: 768px) {
  body {
    background-color: red;
  }
}

```

### 3. Các loại

1. `max-width` (mobile-first)

    ```css
    /* css áp dụng khi màn hình nhỏ hơn 768px */
    @media (max-width: 768px){
    /* css */
    }
    ```

2. `min-width`

    ```css
    /** áp dụng khi màn hình lớn hơn 768px */
    @media (min-width: 768px){

    }
    ```

### 4. Tư duy

- Mobile first

    - Viết css cho mobile trước
    - Sau đó mở rộng cho màn hình lớn

### 5. Ví dụ

```html
<div class="box">Hello</div>

<style>
    .box {
        width: 100%;
        background: blue;
    }

    /* Tablet */
    @media (min-width: 768px) {
        .box {
            width: 50%;
            background: green;
        }
    }

    /* Desktop */
    @media (min-width: 1024px) {
        .box {
            width: 25%;
            background: orange;
        }
    }
</style>
```

- Kết quả:

| Thiết bị | Width | Màu        |
| -------- | ----- | ---------- |
| Mobile   | 100%  | xanh dương |
| Tablet   | 50%   | xanh lá    |
| Desktop  | 25%   | cam        |

### 6. Breakpoints phổ biến

```css
/* Mobile */
@media (max-width: 767px)

/* Tablet */
@media (min-width: 768px)

/* Laptop */
@media (min-width: 1024px)

/* Large screen */
@media (min-width: 1280px)

```

### 7. Media Queries cho chiều cao / xoay màn hình

```css
/* khi xoay ngang điện thoại */
@media (orientation: landscape) {
  body {
    background: pink;
  }
}
```

## 2. Relative Units

### 1. Khái niệm

- Relative Units = đơn vị phụ thuộc vào một thứ khác

    - `px` → cố định
    - `em`, `rem`, `%`, `vw`, `vh` → co giãn theo context

### 2. Vì sao phải dùng

- Vì web phải chạy trên điện thoại, tablet, desktop
- Nếu dùng toàn `px`: layout cứng, không responsive, khó scale UI

### 3. Các loại quan trọng

1. `em` - phụ thuộc vào parent

    - 1em = kích thước font của thẻ cha

    ```css
    .parent {
        font-size: 20px;
    }

    /** .child = 40px */
    .child {
        font-size: 2em;
    }

    /* grandchild = 80px */
    .grandchild {
        font-size: 2em;
    }

    ```

    - Nhược điểm: Dễ bị "phóng to dây chuyền"

2. `rem`

    - 1rem = font-size của html (root)

    ```css
    html {
    font-size: 16px;
    }

    /* h1 = 32px */
    h1 {
    font-size: 2rem;
    }

    ```

    - Ưu điểm: không bị ảnh hưởng bởi parent, dễ kiểm soát toàn hệ thống

    ```css
    /* 1rem = 10px → dễ tính */
    html {
    font-size: 62.5%;
    }
    ```

3. `%` — theo kích thước cha

    - Dùng nhiều cho layout

    ```css
    /** = 50% của parent */
    .box {
        width: 50%;
    }
    ```

    - width → theo parent width
    - height → nhiều khi KHÔNG hoạt động nếu parent không có height

4. `vw / vh` — theo màn hình

    | Unit  | Nghĩa                  |
    | ----- | ---------------------- |
    | `1vw` | 1% chiều rộng màn hình |
    | `1vh` | 1% chiều cao màn hình  |

    ```css
    /** full màn hình */
    .hero {
        width: 100vw;
        height: 100vh;
    }
    ```

5. `vmin / vmax`

    | Unit   | Nghĩa                         |
    | ------ | ----------------------------- |
    | `vmin` | lấy nhỏ hơn giữa width/height |
    | `vmax` | lấy lớn hơn                   |

### 4. So sánh nhanh

| Unit  | Phụ thuộc vào | Nên dùng khi          |
| ----- | ------------- | --------------------- |
| em    | parent        | component nhỏ         |
| rem   | root          | font, spacing toàn hệ |
| %     | parent        | layout                |
| vw/vh | viewport      | full screen           |

### 5. Tư duy đúng

- Font -> rem
- Layout -> %
- Full screen -> vh/vw
- Component nhỏ -> em

## 3. Mobile First Workflow

### 1. Tại sao phải dùng Mobile first

- Cách sai phổ biến: design desktop trước -> rồi fix cho mobile. Kết quả: code rối, css bị override lung tung, responsive khó kiểm soát

- Cách đúng (mobile first): bắt đầu từ màn hình nhỏ nhất, layout đơn giản nhất, sau đó thêm tính năng cho màn hình lớn hơn

### 2. Workflow chuẩn

- B1: code cho mobile (không dùng media query)
- B2: mở rộng cho tablet
- B3: Desktop

```css
/* mobile = 1 cột */
.container {
  width: 100%;
}

.item {
  width: 100%;
}

/* tablet = 2 cột */
@media (min-width: 768px) {
  .item {
    width: 50%;
  }
}

/* desktop = 4 cột */
@media (min-width: 1024px) {
  .item {
    width: 25%;
  }
}
```
