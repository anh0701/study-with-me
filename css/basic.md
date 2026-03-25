---
layout: default
title: 27.1 CSS basic
parent: 27. CSS
description: ""
---

# CSS basic

## Selectors

- CSS Selectors: là các mẫu dùng để tìm và chọn các phần tử HTML cần định dạng kiểu dáng (style).

- Selector cơ bản:

    - Universal Selector (*): Chọn tất cả phần tử.
    - Type Selector (element): Chọn theo tên thẻ HTML (ví dụ: p, h1, div).
    - Class Selector (.className): Chọn các phần tử có thuộc tính class xác định (dùng dấu . trước tên class).
    - ID Selector (#idName): Chọn một phần tử duy nhất có thuộc tính ID xác định (dùng dấu # trước tên id).

- Selector kết hợp (Combinator):

    - Descendant (A B): Chọn phần tử B nằm trong phần tử A.
    - Child (A > B): Chọn phần tử B là con trực tiếp của phần tử A.
    - Adjacent Sibling (A + B): Chọn phần tử B ngay sau phần tử A.

- Pseudo-classes (:state): Chọn phần tử dựa trên trạng thái (ví dụ: :hover, :focus, :nth-child()).
- Pseudo-elements (::part): Chọn và tạo kiểu cho một phần cụ thể của phần tử (ví dụ: ::before, ::after, ::first-line).
- Attribute Selector ([attr]): Chọn phần tử dựa trên thuộc tính hoặc giá trị thuộc tính (ví dụ: [type="text"], [href]).

## Color & Typography

## The Box Model
