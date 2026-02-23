---
layout: default
title: 4. Hosting, Domain, DNS
description: ""
---

### Hosting, Domain, DNS

#### Hosting

- Hosting còn được gọi là Web Hosting **là một dịch vụ giúp trang web hay ứng dụng web của bạn có thể truy cập được trên Internet**
- Hosting dùng để lưu trữ toàn bộ những nội dung của website. Nếu như không có hosting thì trang web chỉ có thể hoạt động trên máy tính của bạn mà thôi. Chỉ mỗi mình bạn nhìn thấy và sử dụng website đó. Nếu website có hosting cộng với tên miền hoặc một địa chỉ IP, những người khác như khách hàng, đối tác, nhân viên hoàn toàn dễ dàng tìm kiếm và truy cập vào website của bạn.
- Website cũng giống như ngôi nhà và hosting giống như một chiếc móng nhà vậy. Nếu bạn muốn website hoạt động ổn định, chứa được lượng data khổng lồ thì hosting của bạn phải thật mạnh, dung lượng lưu trữ phải lớn thì mới có thể khiến website của bạn hoạt động trơn tru, ổn định được

#### Domain
Lý do cần có domain name:

- **Dễ nhớ và dễ truy cập**: Tên miền giúp người dùng dễ dàng truy cập vào website của bạn mà không cần nhớ địa chỉ IP phức tạp
- **Xây dựng thương hiệu**: Một tên miền độc đáo và dễ nhớ giúp xây dựng và củng cố thương hiệu của bạn trên Internet
- **Tạo sự chuyên nghiệp**: Sở hữu một tên miền riêng giúp bạn trông chuyên nghiệp hơn trong mắt khách hàng và đối tác
- **Kiểm soát sự hiện diện trực tuyến**: Bạn có toàn quyền kiểm soát nội dung và thiết kế của website khi sở hữu tên miền riêng
- **Bảo vệ danh tính**: Đăng ký tên miền giúp bảo vệ danh tính và thương hiệu của bạn khỏi việc bị người khác chiếm đoạt

#### DNS

(Domain Name System) là hệ thống phân giải tên miền, giúp chuyển đổi tên miền dễ nhớ (như www.example.com) thành địa chỉ IP (như 192.0.2.1) mà máy tính sử dụng để xác định và giao tiếp với nhau trên mạng Internet

 **Cách DNS hoạt động:**

1. **Truy vấn DNS**: Khi bạn nhập một tên miền vào trình duyệt, trình duyệt sẽ gửi một truy vấn DNS để tìm địa chỉ IP tương ứng.
2. **Tìm kiếm trong cache**: Trình duyệt và hệ điều hành sẽ kiểm tra bộ nhớ tạm (cache) để xem liệu địa chỉ IP đã được lưu trữ trước đó hay chưa.
3. **Liên hệ với DNS server**: Nếu không tìm thấy trong cache, truy vấn sẽ được gửi đến DNS server của nhà cung cấp dịch vụ Internet (ISP).
4. **Phân giải tên miền**: DNS server sẽ liên hệ với các server khác (như Root DNS Server, TLD Nameserver, và Authoritative Nameserver) để tìm địa chỉ IP chính xác.
5. **Trả về kết quả**: Khi tìm thấy địa chỉ IP, DNS server sẽ trả kết quả về cho trình duyệt, và trình duyệt sẽ sử dụng địa chỉ IP này để kết nối đến website

