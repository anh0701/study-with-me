---
layout: default
title: 07. Database
description: ""
---

### Database

#### Relational Databases

##### MySQL

##### MarialDB

##### MS SQL

##### Oracle

##### SQLite

#### More about Database

##### ORMs

ORM (Object-Relational Mapping) là một kĩ thuật lập trình giúp ánh xạ các cấu trúc của cơ sở dữ liệu quan hệ vào các đối tương trong phần mềm được viết bằng các ngôn ngữ hướng đối tượng.
Điều này giúp các nhà phát triển tương tác với cơ sở dữ liệu một cách dễ dàng và tiện lợi hơn.

**Vì sao cần dùng ORM**

1. Tăng năng suất: ORM giúp giảm thời gian và công sức cần thiết để viết các truy vấn dữ liệu bằng cách cung cấp 1 API đơn giản để tạo, đọc, cập nhật và xóa dữ liệu.
2. Cải thiện khả năng bảo trì: Logic truy vấn dữ liệu được tách biệt khỏi code nghiệp vụ, giúp code dễ đọc, dễ hiểu, dễ bảo trì hơn.
3. Giảm thiểu lỗi: ORM tự động xử ký việc thoát các ký tự đặc biệt, giúp giảm nguy cơ lỗi SQL injection.
4. Tính độc lập với cơ sở dữ liệu: ORM có khả năng ánh xạ với các hệ quản trị cơ sở dữ liệu khác nhau, giúp code ứng dụng trở nên độc lập hơn với cơ sở dữ liệu underlying.

**Cách ORM hoạt động**

Khi sử dụng ORM, các lớp đối tượng được định nghĩa bởi người phát triển và được ánh xạ vào các bảng dữ liệu trong cơ sở dữ liệu. 
Khi các đối tượng được tạo ra hoặc được truy xuất, ORM sẽ tự động tạo hoặc tìm kiếm các bản ghi trong cơ sở dữ liệu và đưa chúng vào các đối tượng.


##### ACID

viết tắt của bốn thuộc tính quan trọng: Atomicity (Nguyên tử), Consistency(Nhất quán), Isolation (Cô lập), Durability (Bền vững).

**Vì sao cần ACID**

1. Atomicity (Nguyên tử): Đảm bảo rằng tất cả các bước trong 1 transaction đều phải hoàn thành hoặc không có bước nào được thực hiện.
Nếu có lỗi xảy ra, toàn bộ transaction sẽ bị hủy bỏ và dữ liệu sẽ trở về trạng thái ban đầu.
2. Consistency (Nhất quán): Đảm bảo rằng 1 transaction sẽ đưa cơ sở dữ liệu từ 1 trạng thái hợp lệ này sang 1 trạng thái hợp lệ khác, duy trì các quy tắc và ràng buộc của dữ liệu.
3. Isolation (Cô lập): Đảm bảo rằng các transaction đồng thời không ảnh hưởng lẫn nhau. Mỗi transaction sẽ được thực hiện như thể nó là transaction duy nhất trong hệ thống.
4. Durability (Bền vững): Đảm bảo rằng khi một transaction đã được xác nhận hoàn tất, các thay đổi của nó sẽ được lưu trữ vĩnh viễn, ngay cả khi hệ thống gặp sự cố.

**Cách nó hoạt động**

- Atomicity: Sử dụng các cơ chế như log transaction để đảm bảo rằng các thay đổi được thực hiện toàn bộ hoặc không thực hiện gì cả.
- Consistency: Áp dụng các ràng buộc và quy tắc dữ liệu để đảm bảo rằng mọi giao dịch đều duy trì tính nhất quán của cơ sở dữ liệu.
- Isolation: Sử dụng các kĩ thuật như khóa (locking) và phiên bản (versioning) để đảm bảo rằng các giao dịch không can thiệp lẫn nhau.
- Durability: Sử dụng các cơ chế lưu trữ bền vững như ghi log và sao lưu để đảm bảo rằng dữ liệu không bị mất sau khi transaction hoàn tất.

##### Transactions

Transactions là một tập hợp các thao tác dữ liệu được thực hiện như một đơn vị công việc duy nhất. 
Nếu bất kỳ thao tác nào trong transactions thất bại, toàn bộ transactions sẽ bị hủy bỏ (rollback), đảm bảo rằng cơ sở dữ liệu không bao giờ ở trạng thái không nhất quán.

**Vì sao cần dùng Transactions?**

- Đảm bảo tính toàn vẹn của dữ liệu: bảo vệ dữ liệu khỏi các lỗi hoặc mất mát.
- Đảm bảo tính nhất quán: Các thay đổi dữ liệu chỉ có hiệu lực khi tất cả các thao tác trong transactions thành công.
- Bảo vệ dữ liệu: Ngăn chặn truy cập dữ liệu không hợp lệ hoặc truy cập dữ liệu một cách đồng thời.

**Cách thức hoạt động của Transactions**

1. BEGIN TRANSACTION: Bắt đầu transactions.
2. Thực hiện các thao tác: Thực hiện các thao tác dữ liệu như Insert, Update, Delete.
3. COMMIT TRANSACTION: Xác nhận và ghi nhận các thay đổi, kết thúc Transactions.
4. ROLLBACK TRANSACTION: Hủy bỏ transactions nếu có lỗi xảy ra.


##### N+1 Problem

Là vấn đề hiệu suất thường gặp trong các ứng dụng sử dụng cơ sở dữ liệu quan hệ. 
Vấn đề xảy ra khi 1 truy vấn bắt đầu (1 query) dẫn đến N truy vấn bổ sung => việc thực hiện N+1 truy vấn bổ sung để lấy dữ liệu cần thiết.
=> gây ra nhiều truy vấn không cần thiết, làm chậm hiệu suất ứng dụng.

Ví dụ bảng `Author` và `Book` liên kết với nhau, muốn lấy tất cả tác giả và sách của họ
- query dẫn đến N+1 problems
```sql
    -- Query 1: Lấy tất cả các tác giả
    SELECT * FROM authors;
    
    -- Query N: Với mỗi tác giả, lấy các cuốn sách của họ
    SELECT * FROM books WHERE author_id = 1;
    SELECT * FROM books WHERE author_id = 2;

```

Giải pháp:
```sql
    SELECT authors.author_id, authors.author_name, books.book_id, books.title
    FROM authors
    JOIN books ON authors.author_id = books.author_id;

```

**Vì sao cần tránh N+1 problems**
- Hiệu suất: Giảm số lượng truy vấn cần thực hiện, tăng hiệu suất hệ thống.
- Tải hệ thống: Giảm tải cho cơ sở dữ liệu, giúp hệ thống hoạt động ổn định hơn.

**Vì sao join tốn ít chi phí hơn**

1. việc tối ưu hóa của cơ sở dữ liệu: hệ quản trị cơ sở dữ liệu (DBMS) thường có các cơ chế tối ưu hóa nâng cao cho các lệnh JOIN.
Khi sử dụng lệnh JOIN, DBMS có thể tận dụng các chỉ số (indexes) và kĩ thuật tối ưu hóa khác để thực hiện truy vấn một cách hiệu quả nhất.
2. giảm số lượng truy vấn: thay vì phải gửi nhiều truy vấn riêng lẻ từ ứng dụng đến cơ sở dữ liệu (một cho mỗi bản ghi), bạn chỉ cần gửi một truy vấn duy nhất với JOIN.
Điều này giúp giảm chi phí giao tiếp giữa ứng dụng và cơ sở dữ liệu, tiết kiệm băng thông mạng và thời gian xử lý.
3. giảm thiểu overhead: Khi gửi nhiều truy vấn riêng lẻ, mỗi truy vấn đều phải xử lý từng bước như phân tích cú pháp (parsing), lập kế hoạch thực hiện (execution planning) và thực hiện (execution).
Với một truy vấn JOIN duy nhất, các bước này chỉ cần thực hiện một lần, giảm thiểu overhead.
4. tối ưu hóa bộ nhớ đệm: DBMS có thể tối ưu hóa việc sử dụng bộ nhớ đệm (cache) khi thực hiện truy vấn JOIN, giảm thiểu việc truy xuất đĩa. Nhiều truy vấn riêng lẻ có thể gây ra tình trạng sử dụng bộ nhớ đệm không hiệu quả.
Nhiều truy vấn riêng lẻ có thể gây ra tình trạng sử dụng bộ nhớ đệm không hiệu quả, dẫn đến việc truy xuất đĩa nhiều hơn và làm chậm quá trình xử lý.

##### Normalization

##### Failure Modes

##### Profiling Perfor

##### Migrations