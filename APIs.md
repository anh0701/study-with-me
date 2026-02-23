---
layout: default
title: 8. APIs
nav_order: 2
description: ""
---

### APIs
API (Application Programming Interface) 
là một giao diện lập trình ứng dụng, cho phép các phần mềm hoặc dịch vụ giao tiếp và tương tác với nhau.API hoạt động như một cầu nối, giúp các ứng dụng có thể truy cập và sử dụng các chức năng hoặc dữ liệu từ một ứng dụng hoặc dịch vụ khác một cách dễ dàng.
#### Vì sao cần API?
- Tăng cường khả năng tích hợp: cho phép các hệ thống khác nhau kết nối và làm việc cùng nhau.
- Tiết kiệm thời gian và công sức: giúp các nhà phát triển không cần phải viết lại các chức năng từ đầu.
- Tăng cường bảo mật: API có thể kiểm soát quyền truy cập và bảo vệ dữ liệu.
- Tạo điều kiện cho sự đổi mới: cho phép các nhà phát triển xây dựng các ứng dụng mới dựa trên các dịch vụ hiện có.
#### Cách API hoạt động
API hoạt động dựa trên mô hình client-server:
1. Client gửi yêu cầu đến server thông qua API
2. Server nhận yêu cầu, xử lý và gửi phản hồi lại cho client
3. Client nhận phản hồi và sử dụng dữ liệu hoặc chức năng được cung cấp.
#### Authentication
##### 1. JWT
JWT (JSON Web Token) là một chuẩn mở (RFC 7519) dùng để tạo ra các token truyền tải thông tin giữa các bên một cách an toàn dưới dạng JSON.

**Cấu trúc của JWT**

JWT gồm ba phần chính, được phân tách bởi dấu chấm (.):
- Header: Chứa thông tin về kiểu token và thuật toán mã hóa, VD: `{"alg": "HS256", "typ": "JWT"}`
- Payload: Chứa dữ liệu (claims) mà bạn muốn truyền tải, VD: `{"sub": "1234567890", "name": "John Doe", "admin": true}`
- Signature: Được tạo ra bằng cách mã hóa header và payload với một khóa bí mật hoặc một cặp khóa công khai/riêng tư

**Làm sao JWT hoạt động?**

Khi một người dùng đăng nhập, server sẽ tạo một JWT với các thông tin cần thiết và gửi lại cho client. Client sẽ lưu trữ JWT này, thường là trong local storage hoặc session storage.Khi client thực hiện các yêu cầu tiếp theo, JWT sẽ được gửi kèm theo (thường là trong header của HTTP request).Server sẽ kiểm tra JWT để xác thực và phân quyền.

**Ưu điểm của JWT**
- Độc lập: JWT không phụ thuộc vào cơ sở dữ liệu hoặc session server-side để xác thực.
- Bảo mật: được mã hóa, giúp bảo vệ thông tin trong payload.
- Tiện lợi: JWT có thể chứa nhiều thông tin và dễ dàng truyền tải giữa các hệ thống khác nhau.

**Khi nào dùng JWT**
- Xác thực người dùng (authentication): thường được sử dụng để xác thực người dùng trong các ứng dụng web và di động.
- Ủy quyền (Authorization): có thể được sử dụng để phân quyền truy cập vào các tài nguyên cụ thể dựa trên thông tin trong payload.
##### 2. OAuth
OAuth (Open Authorization) là một chuẩn mở cho phép các ứng dụng của bên thứ ba có thể truy cập một số thông tin của người dùng trên một dịch vụ mà không cần phải cung cấp mật khẩu. Đây là một trong những phương pháp xác thực hiện đại giúp bảo mật và tiện lợi hơn.

**Cách hoạt động** 

 OAuth cho phép bạn cấp quyền truy cập cho ứng dụng bằng cách sử dụng một token thay vì chia sẻ mật khẩu của bạn.
1. Người dùng yêu cầu dịch vụ cấp quyền truy cập: Người dùng sẽ được chuyển hướng đến trang đăng nhập của dịch vụ yêu cầu xác thực (VD: Google, Facebook)
2. Người dùng đăng nhập và cấp quyền: Người dùng đăng nhập và cho phép ứng dụng truy cập các thông tin cụ thể.
3. Dịch vụ trả về token: Sau khi xác thực và cấp quyền, dịch vụ sẽ trả về một token cho ứng dụng.
4. Ứng dụng sử dụng token để truy cập: Ứng dụng sử dụng token này để truy cập các thông tin đã được người dùng cho phép.

**Lợi ích**
- Bảo mật: Người dùng không cần chia sẻ mật khẩu của họ với ứng dụng, giảm nguy cơ mất mật khẩu.
- Tiện lợi: Người dùng có thể dễ dàng cấp quyền truy cập mà không cần phải tạo tài khoản mới.
- Kiểm soát: Người dùng có thể quản lý và thu hồi quyền truy cập của các ứng dụng bất kì lúc nào.

**Các phiên bản của OAuth**
- OAuth 1.0a: Phiên bản đầu tiên, khá phức tạp và ít sử dụng hiện nay.
- OAuth 2.0: Phiên bản mới nhất, đơn giản hơn và được sử dụng rộng rãi.
##### 3. Basic Authentication
Là một phương thức xác thực đơn giản trong HTTP, trong đó user gửi tên đăng nhập và mật khẩu được mã hóa cơ bản (Base64) cùng với mỗi yêu cầu HTTP.Đây là một trong những phương thức xác thực phổ biến nhất nhưng cũng là 1 trong những phương thức ít an toàn nhất.

**Cách hoạt động**
1. Client gửi yêu cầu: Khi client gửi yêu cầu tới server, server sẽ trả về mã trạng thái 401 Unauthorized cùng với tiêu đề WWW-Authenticate yêu cầu xác thực.
2. Client gửi thông tin đăng nhập: Client sẽ mã hóa tên đăng nhập và mật khẩu bằng Base64 và gửi chúng trong tiêu đề Authorization của yêu cầu tiếp theo.
3. Server xác thực: Server xác thực: Server giải mã Base64 để lấy tên đăng nhập và mật khẩu, sau đó xác thực chúng để quyết định cấp quyền truy cập hay từ chối.

**Cú pháp của Basic Authentication**
```shell  
    Authorization: Basic base64(username:password)  
    #  ví dụ username = admin, password = password GET /protected-resource HTTP/1.1
    Host: example.comAuthorization: Basic YWRtaW46cGFzc3dvcmQ=
```
**Ưu điểm**
- Đơn giản và dễ triển khai: không yêu cầu cấu hình phức tạp hay cài đặt thêm phần mềm.
- Phổ biến: hỗ trợ rộng rãi trên các trình duyệt và ứng dụng.

**Nhược điểm**
- Không an toàn nếu không sử dụng HTTPS: thông tin đăng nhập có thể bị đánh cắp nếu không sử dụng kết nối bảo mật.
- Không hỗ trợ các tính năng bảo mật nâng cao: Như xác thực hai yếu tố hay token-based authentication.

**Cách cải thiện bảo mật**
- Sử dụng HTTPS: Đảm bảo kết nối an toàn để mã hóa thông tin đăng nhập.
- Sử dụng phương thức xác thực khác: Như OAuth, JWT hoặc token-based authentication để tăng cường bảo mật.
##### 4. Token Authentication
Là một phương thức xác thực an toàn và hiện đại, trong đó server tạo ra 1 token cho người dùng sau khi xác thực thành công.Token này này được sử dụng để xác thực các yêu cầu tiếp theo mà không cần phải gửi lại thông tin đăng nhập như tên người dùng và mật khẩu.

**Cách token authentication hoạt động**
1. Client gửi thông tin đăng nhập: client gửi yêu cầu đăng nhập cùng thông tin đăng nhập (tên người dùng và mật khẩu) tới server.
2. Server xác thực thông tin đăng nhập: server kiểm tra thông tin đăng nhập, nếu đúng sẽ tạo ra một token.
3. Client nhận token: client lưu trữ token này (thường là trong bộ nhớ tạm thời hoặc cookies).
4. Client gửi yêu cầu với token: trong các yêu cầu tiếp theo, client gửi token này trong header của yêu cầu HTTP.
5. Server kiểm tra token: server xác minh token nếu hợp lệ thì xử lý yêu cầu, không thì từ chối.
##### 5. Cookie Based Auth

là một phương pháp xác thực phổ biến trong các ứng dụng web

vì sao cần dùng ?

- xác thực người dùng: đảm bảo người đang đăng nhập là người có quyền truy cập.
- tránh đăng nhập lại: giúp người dùng không phải đăng nhập lại mỗi khi truy cập các page khác trong ứng dụng.
- dễ dàng triển khai: dễ dàng tích hợp vào các framework và thư viện hiện tại.

cách hoạt động?

- Đăng nhập: người dùng nhập thông tin đăng nhập: username, password
- Tạo cookie: server xác thực thông tin đăng nhập và tạo cookie chứa thông tin xác thực
- Gửi cookie: server gửi cookie đến trình duyệt người dùng.
- Lưu cookie: trình duyệt lưu cookie.
- Yêu cầu tiếp theo: Với mỗi yêu cầu tiếp theo của trình duyệt, cookie sẽ được gửi kèm đến server
- Kiểm tra cookie: server sẽ kiểm tra cookie và xác thực người dùng

Ưu điểm?

- Dễ triển khai: dễ tích hợp vào các ứng dụng web hiện tại.
- Trải nghiệm người dùng tốt: người dùng không phải đăng nhập lại mỗi khi gửi request
- Xác thực nhanh chóng: xác thực người dùng nhanh chóng đối với mỗi yêu cầu.

Hạn chế?

- An toàn hạn chế: Cookie có thể bị lộ nếu bị tấn công man-in-the-middle hoặc cookie hijacking.
- Không thích hợp cho ứng dụng di động: Không phù hợp với các ứng dụng di động hoặc API.

<details>
  <summary>Vì sao không tương thích với ứng dụng di động?</summary>

- Bảo mật và lưu trữ:

  - Trình duyệt web có cơ chế tự động quản lý và bảo mật cookie tốt hơn so với các ứng dụng di động.
  - Các ứng dụng di động phải tự mình lưu trữ và quản lý cookie, điều này có thể dẫn đến các vấn đề bảo mật nếu không được triển khai đúng cách.
- Cơ chế hoạt động của ứng dụng di động:

    - Ứng dụng di động thường có nhiều phiên bản khác nhau, nên việc đồng bộ và quản lý cookie trở nên phức tạp hơn.
    - Cookie có thể bị mất khi ứng dụng bị đóng hoặc cập nhật, dẫn đến việc người dùng phải đăng nhập lại thường xuyên.

- Khả năng tương tác với API:

    - Các ứng dụng di động thường giao tiếp với API thông qua các token như JWT (JSON Web Token) vì tính tiện lợi và bảo mật cao hơn.
    - JWT có thể được lưu trữ và sử dụng dễ dàng trong ứng dụng di động, giúp bảo mật và quản lý phiên làm việc tốt hơn so với cookie.

</details>

Giải pháp:

- Sử dụng HTTPS: Đảm bảo rằng tất cả các giao tiếp giữa trình duyệt và server đều sử dụng HTTPS để bảo vệ cookie.
- Sử dụng token-based authentication: Thay thế hoặc kết hợp với token-based authentication (ví dụ: JWT) để tăng tính an toàn.

##### 6. OpenID

- là một hệ thống xác thực đa dạng cho phép người dùng sử dụng một tài khoản để đăng nhập vào nhiều dịch vụ khác nhau mà không cần phải đăng nhập nhiều lần.
Một phương pháp phổ biến để giảm bớt việc nhớ và quản lý nhiều tài khoản đăng nhập.

Cơ chế hoạt động

OpenID hoạt động dựa trên một hệ thống xác thực đa dạng. Khi người dùng muốn đăng nhập vào một dịch vụ, họ sẽ được yêu cầu cung cấp tài khoản OpenID của mình. 
Dịch vụ này sẽ liên hệ với cơ sở dữ liệu OpenID để xác thực tài khoản và trả về kết quả. Nếu xác thực thành công, người dùng sẽ được chuyển đến trang chính của dịch vụ mà không cần phải nhập lại thông tin đăng nhập.

Lý do sử dụng OpenID

- Tiện lợi: người dùng không cần phải nhớ nhiều tài khoản đăng nhập
- An toàn: giảm thiểu rủi ro mất mát thông tin đăng nhập
- Tiết kiệm thời gian: giảm bớt thời gian đăng nhập vào các dịch vụ khác nhau.

Nhược điểm:

- Phụ thuộc vào dịch vụ OpenID: Nếu dịch vụ OpenID gặp sự cố người dùng có thể không thể truy cập vào các  dịch vụ liên quan.
- Rủi ro bảo mật: Nếu tài khoản OpenID bị truy cập trái phép, người dùng có thể mất quyền truy cập vào nhiều dịch vụ.

Giải pháp khắc phục:

- Sử dụng mật khẩu phức tạp: đảm bảo rằng tài khoản OpenID của bạn có mật khẩu phức tạp và không dễ dàng đoán.
- Sử dụng 2FA (Two-Factor Authentication): bổ sung một lớp bảo mật khác như OTP (One-Time Password) hoặc biometric.
- Theo dõi và kiểm tra: thường xuyên kiểm tra hoạt động tài khoản và thông báo bất thường nếu có.

##### 7. SAML

> Giả sử bạn đăng nhập vào một hệ thống quản lý công việc (IdP) và sau đó truy cập vào một ứng dụng CRM (SP).
> Khi bạn nhấp vào biểu tượng CRM, hệ thống gửi yêu cầu xác thực đến hệ thống quản lý công việc. Hệ thống quản lý công việc sẽ trả về một SAML Assertion chứa thông tin về bạn đã được xác thực.
> CRM sẽ kiểm tra và nếu hợp lệ, bạn sẽ được chứng thực và truy cập vào ứng dụng mà không cần phải nhập lại thông tin đăng nhập.

- SAML (Security Assertion Markup Language) được sử dụng để xác thực và chứng thực quyền truy cập của người dùng giữa các phần mềm khác nhau.
- Đây là 1 cách để thực hiện Single Sign-On (SSO), cho phép người dùng đăng nhập vào một ứng dụng và được tự động đăng nhập vào các ứng dụng khác mà không cần phải nhập lại thông tin đăng nhập.

Cách SAML hoạt động:

    1. Identity Provider (IdP): Đây là phần mềm hoặc dịch vụ chịu trách nhiệm xác thực người dùng. Khi người dùng đăng nhập vào IdP, họ được xác thực và chứng thực.
    2. Service Provider(SP): Đây là ứng dụng mà người dùng muốn truy cập. SP yêu cầu xác thực từ IdP để xác minh người dùng.
    3. SAML Assertion: Khi người dùng đăng nhập vào IdP, IdP tạo ra một SAML Assertion (một tài liệu XML) chứa thông tin về người dùng đã được xác thực.
    4. SAML Response: Khi người dùng cố gắng truy cập vào SP, SP sẽ gửi một yêu cầu xác thực đến IdP. IdP sẽ trả về SAML Response chứa SAML Assertion.
    5. Xác minh và truy cập: SP kiểm tra SAML Assertion và nếu hợp lệ, người dùng được chứng thực và truy cập vào ứng dụng.


#### REST
##### 1. JSON APIs
##### 2. SOAP
##### 3. gRPC
##### 4. GraphQL
#### HATEOAS
#### Open API Specs
