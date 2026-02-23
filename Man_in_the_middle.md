---
layout: default
title: 20. Man in the middle (MitM)
nav_order: 2
description: ""
---

### Man in the middle (MitM)
> Bạn đang gửi một bức thư cho bạn của mình, nhưng trước khi bức thư đến tay bạn của bạn, một kẻ xấu đã mở thư, đọc nó, và có thể thay đổi nội dung trước khi gửi tiếp.
> => Đó là cách MitM hoạt động.

MitM là một kiểu tấn công mạng trong đó kẻ tấn công chèn mình vào giữa hai bên đang giao tiếp để đánh cắp hoặc thay đổi thông tin mà hai bên đang trao đổi.

#### Cơ chế hoạt động
1. Chèn vào giữa: kẻ tấn công chèn mình vào giữa hai bên đang giao tiếp (VD: bạn và một trang web).
2. Chặn và đọc dữ liệu: kẻ tấn công chặn và đọc tất cả dữ liệu mà hai bên đang trao đổi.
3. Thay đổi dữ liệu: kẻ tấn công có thể thay đổi dữ liệu trước khi gửi tiếp đến bên nhận.

#### Tác hại của MitM

- Đánh cắp thông tin: Kẻ tấn công có thể đánh cắp thông tin nhạy cảm như mật khẩu, số thẻ tín dụng, và thông tin cá nhân.
- Giả mạo danh tính: Kẻ tấn công có thể giả mạo danh tính của một bên để lừa đảo bên còn lại.
- Thay đổi thông tin: Kẻ tấn công có thể thay đổi thông tin để gây hại hoặc lừa đảo.

#### Đặc điểm của MitM

- Khó phát hiện: MitM thường rất khó phát hiện vì kẻ tấn công có thể làm việc một cách âm thầm.
- Hiệu quả cao: Kẻ tấn công có thể thu thập được nhiều thông tin nhạy cảm.
- Phụ thuộc vào lỗ hổng bảo mật: MitM chỉ hoạt động hiệu quả khi có lỗ hổng bảo mật trong hệ thống.
- Rủi ro pháp lý: Kẻ tấn công có thể bị truy tố pháp lý nếu bị phát hiện.

#### Giải pháp khắc phục

- Sử dụng HTTPS: đảm bảo rằng tất cả các giao tiếp trên web đều sử dụng HTTPS để mã hóa dữ liệu.
- Sử dụng VPN: sử dụng VPN để mã hóa toàn bộ lưu lượng mạng.
- Cảnh giác với Wifi công cộng: tránh sử dụng wifi công cộng không an toàn để truy cập các dịch vụ.

[So sánh MitM và Hijacking](Hijacking.md#so%20sanh%20mitm%20va%20hijacking)




