---
layout: default
title: 2. SSL/TLS
nav_order: 2
description: ""
---

### SSL/TLS

#### SSL

Chứng chỉ SSL sử dụng hai loại mã hóa chính: mã hóa đối xứng và mã hóa bất đối xứng. Dưới đây là cách chúng hoạt động:

1. **Mã hóa bất đối xứng (Asymmetric Encryption)**:
    - **Khóa công khai và khóa riêng**: Máy chủ sử dụng một cặp khóa, gồm khóa công khai (public key) và khóa riêng (private key). Khóa công khai được chia sẻ với mọi người, trong khi khóa riêng được giữ bí mật.
    - **Quá trình mã hóa**: Khi trình duyệt kết nối với máy chủ, máy chủ sẽ gửi khóa công khai của mình cho trình duyệt. Trình duyệt sử dụng khóa công khai này để mã hóa dữ liệu, và chỉ có khóa riêng của máy chủ mới có thể giải mã dữ liệu này.
2. **Mã hóa đối xứng (Symmetric Encryption)**:
    - **Khóa phiên (session key)**: Sau khi kết nối ban đầu được thiết lập và xác thực, trình duyệt và máy chủ sẽ tạo ra một khóa phiên đối xứng. Khóa này được sử dụng để mã hóa và giải mã tất cả dữ liệu truyền trong phiên làm việc đó.
    - **Quá trình mã hóa**: Khóa phiên được mã hóa bằng khóa công khai của máy chủ và gửi đến máy chủ. Máy chủ sau đó giải mã khóa phiên bằng khóa riêng của mình. Từ đó, cả hai bên sử dụng khóa phiên để mã hóa và giải mã dữ liệu.
3. **Quá trình bắt tay SSL (SSL Handshake)**:
    - **Bắt đầu kết nối**: Trình duyệt yêu cầu kết nối bảo mật với máy chủ.
    - **Gửi chứng chỉ**: Máy chủ gửi chứng chỉ SSL chứa khóa công khai của mình cho trình duyệt.
    - **Xác thực chứng chỉ**: Trình duyệt xác thực chứng chỉ để đảm bảo máy chủ là hợp pháp.
        - Chi tiết

          SSL xác thực chứng chỉ của trình duyệt thông qua một quá trình kiểm tra kỹ lưỡng, bao gồm các bước sau:

            1. **Gửi chứng chỉ**: Khi trình duyệt kết nối với một máy chủ, máy chủ sẽ gửi chứng chỉ SSL của mình cho trình duyệt.
            2. **Kiểm tra chứng chỉ**: Trình duyệt kiểm tra chứng chỉ này bằng cách xác minh chữ ký số của chứng chỉ. Chữ ký số này được tạo ra bởi một Certificate Authority (CA) uy tín, và chỉ có CA đó mới có thể tạo ra chữ ký hợp lệ.
            3. **Xác thực CA**: Trình duyệt kiểm tra xem CA phát hành chứng chỉ có nằm trong danh sách các CA tin cậy của mình hay không. Nếu CA không nằm trong danh sách này, trình duyệt sẽ cảnh báo người dùng rằng chứng chỉ không đáng tin cậy.
            4. **Kiểm tra tính toàn vẹn**: Trình duyệt cũng kiểm tra xem chứng chỉ có bị thay đổi hay không bằng cách so sánh chữ ký số với nội dung chứng chỉ. Nếu có bất kỳ thay đổi nào, chữ ký số sẽ không khớp và chứng chỉ sẽ bị coi là không hợp lệ.
            5. **Kiểm tra thời hạn**: Trình duyệt kiểm tra xem chứng chỉ có còn hiệu lực hay không bằng cách so sánh ngày hiện tại với ngày hết hạn của chứng chỉ.
    - **Tạo khóa phiên**: Trình duyệt tạo khóa phiên, mã hóa nó bằng khóa công khai của máy chủ và gửi lại cho máy chủ. 
    - **Mã hóa dữ liệu**: Máy chủ giải mã khóa phiên (bằng private key ⇒ chỉ máy chủ mới đọc được) và bắt đầu sử dụng nó để mã hóa dữ liệu truyền tải.

#### TLS (Transport Layer Security)

Đây là một giao thức mật mã cung cấp bảo mật đầu cuối cho dữ liệu được gửi giữa các ứng dụng qua Internet. TLS phát triển từ SSL (Secure Sockets Layer). TLS không bảo mật dữ liệu trên các hệ thống đầu cuối. Nó chỉ đảm bảo dữ liệu an toàn trên đường truyền qua internet, tránh khả năng bị nghe trộm hoặc thay đổi nội dung.

TLS bảo mật thông tin liên lạc bằng cách sử dụng asymmetric public key infrastrure (cơ sở hạ tầng khóa công khai bất đối xứng) để khởi tạo kết nối giữa client-server và sau đó sử dụng khóa đối xứng (symetric) để mã hóa trong phần còn lại của phiên truyền dữ liệu.

- Khóa riêng tư - **private key**: khóa này do chủ sở hữu trang web kiểm soát và nó được lưu giữ một cách riêng tư. Khóa này nằm trên máy chủ web và được sử dụng để giải mã thông tin được mã hóa bởi khóa công khai.
- Khóa công khai - **public key**: khóa này khả dụng cho tất cả những ai muốn tương tác với máy chủ theo cách an toàn. Thông tin được mã hóa bằng khóa công khai chỉ có thể được giải mã bằng khóa riêng tư.

Mã hóa đối xứng hiệu quả hơn về mặt tính toán so với mã hóa bất đối xứng, nhưng có một khóa bí mật chung có nghĩa là nó cần được chia sẻ một cách an toàn. Đó là lý do ban đầu ta cần sử dụng mã hóa bất đối xứng để trao đổi secet key nhưng sau đó lại dùng mã hóa đối xứng để trao đổi các dữ liệu lớn.

|       | SSL                                                                                                                                                                                                   | TLS                                                                                                                                  |
|-------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| Giống | là các giao thức giao tiếp mã hóa dữ liệu giữa các máy chủ, ứng dụng, người dùng và hệ thống. Các giao thức này xác thực hai bên được kết nối qua mạng để họ có thể trao đổi dữ liệu một cách bảo mật | Tương tự                                                                                                                             |
|       | đều sử dụng mã xác thực thông báo (MAC) - để xác minh tính xác thực và toàn vẹn của thông báo                                                                                                         |                                                                                                                                      |
| Khác  | Bắt tay SSL là kết nối rõ ràng và SSL có nhiều bước hơn quá trình TLS                                                                                                                                 | Bắt tay TLS là một kết nối ngầm, bằng cách loại bỏ các bước bổ sung và giảm tổng số bộ mã hóa => TLS đã tăng tốc quá trình này       |
|       | chỉ có hai loại thông báo báo động: cảnh báo và nghiêm trọng. Báo động SSL không được mã hóa                                                                                                          | TLS có thêm một loại thông báo nữa là thông báo đóng phiên (báo hiệu phiên kết thúc). Báo động TLS được mã hóa để tăng cường bảo mật |
|       | sử dụng thuật toán MD5 - hiện đã lỗi thời - để tạo ra MAC                                                                                                                                             | sử dụng hàm băm (HMAC) cho quá trình mã hóa và bảo mật phức tạp hơn                                                                  |
