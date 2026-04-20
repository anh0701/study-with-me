---
layout: default
title: 29.1 Figma basic
parent: 29. UI/UX
description: ""
---

<div class="my-right-toc" markdown="1">
1. TOC
{:toc}
</div>

## 1. Figma Shortcuts & Basic Actions

### 1. Zoom

![zoom](../../../assets/images/zoom.png)

- Zoom in: Ctrl + hoặc Ctrl + Scroll
- Zoom out: Ctrl -
- Zoom một shape/frame/chi tiết nào đó: ấn giữ phím Z và chọn vào vật thể muốn zoom

### 2. Move / Scale / Hand Tool

![move](../../../assets/images/vhk-tool.png)

#### 2.1 Move Tool (V)

- Dùng để di chuyển object
- Resize không giữ tỉ lệ

#### 2.2 Scale Tool (K)

    - Dùng để resize giữ tỉ lệ
    - Phù hợp khi scale icon, UI

#### 2.3 Hand Tool (H)

    - Dùng để di chuyển canvas
    - Không làm lệch layout

### 3. Frame

![frame](../../../assets/images/frame.png)

![open](../../../assets/images/open-frame.png)

- Ấn `phím F` để mở, hoặc thanh menu bên dưới website

### 4. Chỉnh thuộc tính

![position](../../../assets/images/position.png)

#### 4.1 Xoay góc

![rotation](../../../assets/images/rotation.png)

#### 4.2 Bo góc

![bogoc](../../../assets/images/bogoc.png)

#### 4.3 Layout Guide

![layout guide](../../../assets/images/grid.png)

- bật lên để dễ vẽ

#### 4.4 Hòa trộn màu

![hoatron](../../../assets/images/hoatron.png)

- Muốn hòa trộn màu thì chọn màu cần hòa trộn ở `Fill`
- chọn hình `Giọt nước` ở `Appearance` -> `Overlay/...`

#### 4.5 Cắt giao diện

![slide](../../../assets/images/slide.png)

- Chức năng này giúp cắt giao diện thành các ảnh khi `Export`

### 5. Shape

![shapes](../../../assets/images/shapes.png)

- `Image/video...(Ctrl + Shift + K)`: dùng để thêm ảnh/video

![image-shape](../../../assets/images/shape-image.png)

- Chọn hình elip/hình chữ nhật/hình tam giác/... -> sau đó thêm ảnh

- Đổ màu vào ảnh: chọn shape -> thêm ảnh vào shape -> vẽ shape khác trên ảnh -> chọn `Fill` (màu để đổ vào ảnh) -> chọn các chế độ `overlay/multiply/...` (trong `Giọt nước` ở `Appearance`)

![stroke](../../../assets/images/stroke.png)

- Viền khung: `stroke`

![shadow](../../../assets/images/shadow.png)

- Đổ bóng: `Effect`

![arc](../../../assets/images/arc.png)

- Nút chấm đó để vẽ hình tròn khuyết

![char c](../../../assets/images/char-c.png)

- Cách tạo ra chữ C, nếu như chèn ảnh vào chữ C kia sẽ tạo hiệu ứng khá thú vị

![text style](../../../assets/images/text-style.png)

- Cách chỉnh text thành heading/body/...

### 6. Component

![component](../../../assets/images/component.png)

- Nên dùng khi: phần tử cần tái sử dụng nhiều lần (button, input field, icons, header/footer, card), thiết kế hệ thống đồng bộ (giúp thay đổi một lần ở Main Component toàn bộ instance trên các màn hình khác nhau sẽ tự cập nhật theo), làm việc nhóm (dễ dàng chia sẻ thư viên component/library cho các designer khác), prototype (cần tạo các tương tác phức tạp như: hover, click chuyển trạng thái)

- Chỉnh sửa ở con thì cha không thay đổi, chỉnh sửa ở cha thì tất cả con sẽ thay đổi. Nếu con thay đổi rồi, quay lại đổi cha thì con mới sửa không thay đổi theo cha nữa.

![detach instance](../../../assets/images/detach-instance.png)

- Để hủy component thì chọn component, chuột phải chọn detach instance. Lưu ý chỉ dùng được với component con

- Nếu dùng `auto layout` với component thì nó chỉnh sửa cho tất cả các component

![go to main component](../../../assets/images/go-to-main-component.png)

- Khi có quá nhiều component, cách để tìm component cha: chọn component -> chọn go to main component.

- Muốn tạo màu dễ dàng, thì đặt tên màu để dễ chọn

![color style](../../../assets/images/color-style-new.png)

- Tạo color style với màu mới

![color tu mau cu](../../../assets/images/tao-color-style-with-mau-cu.png)

- Tạo color style với màu cũ đã có

- Muốn tạo style text áp dụng nhiều chỗ, dễ dùng lại thì tạo text style

![create text style](../../../assets/images/text-style-new.png)

- Tạo text style mới

### 7. Constraint

- Giúp vị trí không thay đổi dù resize shape (căn lề ấy)

![constraint](../../../assets/images/constraint.png)
