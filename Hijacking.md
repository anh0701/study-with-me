---
layout: default
title: 20.1 Hijacking
parent: 20. Man in the middle (MitM)
---

### Hijacking

là một kiểu tấn công mạng trong đó kẻ tấn công lấy trộm hoặc chiếm hữu quyền kiểm soát một thiết bị, hệ thống hoặc thông tin mà không có sự cho phép của chủ sở hữu. Đây là một hình thức tấn công phổ biến và có thể gây nhiều hậu quả nghiêm trọng.

#### Cơ chế hoạt động:

1. Lấy trộm quyền kiểm soát: kẻ tấn công sử dụng các phương pháp như tán công man-in-the-middle, tấn công lừa đảo hoặc tấn công vào hệ thống để lấy trộm quyền kiểm soát.
2. Sử dụng quyền kiểm soát: Sau khi lấy trộm quyền kiểm soát, kẻ tấn công có thể sử dụng nó để truy cập, thay đổi hoặc xâm phạm thông tin mà không bị phát hiện.

#### Tác hại

- Đánh cắp thông tin: kẻ tấn công có thể đánh cắp thông tin nhạy cảm như mật khẩu, số thẻ tín dụng và thông tin cá nhân.
- Giả mạo danh tính: kẻ tấn công có thể giả mạo danh tính của một bên để lừa đảo bên còn lại.
- Thay đổi thông tin: kẻ tấn công có thể thay đổi thông tin để gây hại hoặc lừa đảo.

#### Đặc điểm 

- Khó phát hiện: MitM thường rất khó phát hiện vì kẻ tấn công có thể làm việc một cách âm thầm.
- Hiệu quả cao: kẻ tấn công có thể thu thập được nhiều thông tin nhạy cảm.
- Phụ thuộc vào lỗ hổng bảo mật: MitM chỉ hoạt động hiệu quả khi có lỗ hổng bảo mật trong hệ thống.

#### Cách khắc phục
- Sử dụng HTTPS
- Sử dụng VPN
- Cảnh giác với wifi công cộng.

#### Phân loại
1. Session Hijacking:
- kẻ tấn công đánh cắp session ID của người dùng để giả mạo danh tính và chiếm quyền truy cập vào hệ thống hoặc dịch vụ.
- cách khắc phục: sử dụng HTTPS, session timeout, và thường xuyên làm mới session ID.
2. Email Hijacking:
- kẻ tấn công chiếm quyền kiểm soát tài khoản email của người dùng, có thể gửi email lừa đảo hoặc đánh cắp thông tin nhạy cảm.
- cách khắc phục: sử dụng xác thực hai yếu tố (2FA) và mật khẩu mạnh.
3. Browser Hijacking:
- kẻ tấn công thay đổi cài đặt của trình duyệt (ví dụ: trang chủ, công cụ tìm kiếm) mà không có sự đồng ý của người dùng.
- cách khắc phục: cài đặt phần mềm bảo mật và tránh cài đặt các plugin hoặc tiện ích mở rộng không rõ nguồn gốc.
4. DNS Hijacking:
- kẻ tấn công thay đổi bản ghi DNS để chuyển hướng lưu lượng mạng đến trang web giả mạo hoặc độc hại.
- cách khắc phục: sử dụng DNSSEC (DNS Security Extensions) và các biện pháp bảo mật mạng.
5. Wifi Hijacking:
- kẻ tấn công sử dụng mạng wifi không bảo mật để đánh cắp thông tin hoặc thực hiện các cuộc tấn công man-in-the-middle.
- cách khắc phục: sử dụng mạng wifi bảo mật với mật khẩu mạnh và WPA3
6. IP Spoofing:
- kẻ tấn công giả mạo địa chỉ IP để che giấu danh tính hoặc thực hiện các cuộc tấn công man-in-the-middle.
- cách khắc phục: sử dụng các biện pháp bảo mật mạng và giám sát lưu lượng mạng để phát hiện hành vi đáng ngờ.
#### So sánh MitM và Hijacking

Sự tương đồng:
- mục tiêu chung: cả hai đều nhằm chiếm đoạt thông tin hoặc quyền truy cập không được phép.
- phương pháp tấn công: đều có thể sử dụng kĩ thuật tán công giống nhau như phising, exploitation, hoặc malware.

Sự khác biệt:

- Phạm vi tấn công: MitM tập trung vào việc chèn mình vào giữa luồng giao tiếp, trong khi hijacking tập trung vào chiếm đoạt quyền kiểm soát hoặc truy cập vào phiên làm việc hoặc thiết bị.
- Kết quả tấn công: MitM thường nhằm chặn và thay đổi thông tin trong khi hijacking nhằm chiếm đoạt quyền kiểm soát hoặc truy cập.

