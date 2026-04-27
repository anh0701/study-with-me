---
layout: default
title: 30. Spring boot
description: ""
has_toc: side_bar 
---

# Spring boot

## 1. Phân biệt **@Controller** và **@RestController**

- `@Controller`: Dùng chủ yếu cho Spring MVC truyền thống — tức là trả về view (JSP, Thymeleaf, Freemarker…).
- `@RestController`: Dùng cho REST API, tức là trả về data (JSON/XML/plain text) trực tiếp.

- `@RestController` = `@Controller` + `@ResponseBody`

> Có dùng `@Controller` để trả JSON được không?

- Có, và phải viết thêm `@ResponseBody` <=> `@RestController` là cách viết ngắn gọn

```java
@Controller
public class TestController {

    @ResponseBody
    @GetMapping("/test")
    public User test() {
        return new User();
    }
}
```

> Sai lầm phổ biến cho rằng @RestController mạnh hơn @Controller.
>
> Hoàn toàn không đúng, hai cái chỉ khác mục đích sử dụng.

## 2. Trong JPA/Hibernate, khái niệm Lazy Loading? Khi nào thì nó có thể gây ra lỗi "N+1 query" kinh điển?

### 2.1 Lazy Loading

- Lazy Loading là cơ chế trì hoãn việc tải dữ liệu liên quan (related entities) cho đến khi thực sự cần dùng.

```java
@Entity
class Order {
    @OneToMany(mappedBy = "order", fetch = FetchType.LAZY)
    private List<OrderItem> items;
}

// Ở đây khi query `Order`, Hibernate chỉ lấy dữ liệu của bảng `order` trước, còn `items` chưa được load ngay.

Order order = orderRepository.findById(1L).get();

// lúc này chỉ có: SELECT * FROM orders WHERE id = 1
// chỉ khi gọi: 

order.getItems().size(); 

// thì Hibernate mới chạy tiếp: SELECT * FROM order_items WHERE order_id = 1;

```

- Mục tiêu chính của Lazy loading là:

1. giảm lượng data load không cần thiết
2. tối ưu hiệu năng query ban đầu
3. tránh join quá nhiều bảng gây nặng hệ thống

Không phải lúc nào cũng cần lấy toàn bộ graph object. VD: xem danh sách đơn hàng thì thường chỉ cần: mã đơn, ngày tạo, trạng thái, chứ chưa cần toàn bộ `OrderItem`, `Product`, `Customer`, ...

### 2.2 N+1 query

- Lỗi phổ biến khi dùng ORM

```java
List<Order> orders = orderRepository.findAll();

// Hibernate chạy: SELECT * FROM orders;
// Giả sử có 100 orders, sau đó trong code:

for (Order order : orders) {
    System.out.println(order.getCustomer().getName());
}

// Nếu `customer` là LAZY

@ManyToOne(fetch = FetchType.LAZY)
private Customer customer;

// thì mỗi lần `getCustomer()` sẽ phát sinh thêm 1 query: SELECT * FROM customer WHERE id = ?
// Tổng: 1 query lấy orders + 100 query lấy customer

```

- N + 1 query problem là: 1 query chính, N query phụ, rất tệ cho performance
- Cách xử lý:

1. JOIN FETCH

```java

@Query("""
    SELECT o
    FROM Order o
    JOIN FETCH o.customer
""")
List<Order> findAllWithCustomer();

// Hibernate sẽ dùng JOIN để lấy luôn
```

2. @EntityGraph

```java
@EntityGraph(attributePaths = {"customer"})
List<Order> findAll();

// đỡ viết JPQL thủ công
```

3. DTO projection

```java
SELECT new OrderDto(o.id, c.name)
// query thẳng DTO thay vì Entity, thường tốt hơn cho read-heavy system
```

4. Batch Fetching

```sh
hibernate.default_batch_fetch_size=50
# Hibernate gom nhiều query thành batch, không giải quyết tận gốc nhưng cải thiện tốt
```

> Sai lầm phổ biến cho rằng đổi hết sang EAGER là xong
>
> Sai. EAGER thường còn nguy hiểm hơn  
>
> - query phình to
> - cartesian product
> - memory tăng mạnh
> - khó kiểm soát SQL
> Senior dev thường mặc định dùng LAZY, chủ động fetch đúng nơi cần, chứ không dùng EAGER bừa bãi

## 3. LazyInitializationException là gì?

LazyInitializationException là lỗi rất hay gặp khi dùng JPA/Hibernate, đặc biệt liên quan đến Lazy Loading.

### 3.1 Khái niệm

- Đây là exception xảy ra khi Hibernate cố gắng load một association được đánh dấu LAZY, nhưng lúc đó Session (Persistence Context) đã bị đóng.

### 3.2 Ví dụ

```java
@Entity
public class User {
    @OneToMany(mappedBy = "user", fetch = FetchType.LAZY)
    private List<Order> orders;
}

//  
@Transactional
public User getUser(Long id) {
    return userRepository.findById(id).get();
}

// Trong Controller
User user = userService.getUser(1L);

System.out.println(user.getOrders().size());

// Giải thích:
// Trong `getUser()`: hibernate mở session, lấy `User`, nhưng không lấy `orders` ngay vì `LAZY`
// Nó chỉ tạo proxy: Khi nào cần thì tôi mới query
// Sau khi method kết thúc: transaction đóng, session đóng
// Lúc này ở Controller gọi: `user.getOrders()`, hibernate mới nói: Ok để tôi query DB lấy orders...
// nhưng: session đâu rồi? -> không thấy -> `LazyInitializationException` 

```

### 3.3 Bản chất vấn đề

- Không phải lỗi của **LAZY** mà là: truy cập dữ liệu lazy ngoài transaction/session

### 3.4 Cách xử lý đúng

- Load luôn ``user.getOrders().size();`` trong transaction
- Dùng **JOIN FETCH** (cách chuẩn nhất)

```java
@Query("""
    SELECT u FROM User u
    JOIN FETCH u.orders
    WHERE u.id = :id
""")
User findUserWithOrders(Long id);
```

### 3.5 Cách xử lý sai hay gặp

- Nhiều người đổi sang **FetchType.EAGER** để hết lỗi. Nhưng cách này chỉ để chữa cháy vì: gây query thừa, dễ tạo N+1 query, giảm performance mạnh

- Oen Session In View (OSIV): Spring boot thường bật mặc định, nó giữ session mở đến tận view layer, nên controller gọi lazy vẫn chạy được. Nhưng che giấu vấn đề thiết kế và có thể gây ra: query lung tung, khó debug performance, DB connection giữ lâu

### 3.6 Tóm tắt

LazyInitializationException xảy ra khi Hibernate cố gắng truy cập một LAZY association sau khi Persistence Context đã đóng.

Nguyên nhân là entity chỉ giữ proxy thay vì dữ liệu thật, và khi cần load thì session không còn tồn tại.

Cách xử lý tốt nhất là fetch dữ liệu cần thiết trong transaction bằng JOIN FETCH, EntityGraph hoặc map sang DTO trong service layer, thay vì chuyển sang EAGER hoặc phụ thuộc vào OSIV.

## 4. vì sao **@Transactional** ảnh hưởng tới lazy loading?

**@Transactional** ảnh hưởng tới Lazy Loading vì nó quyết định Hibernate Session (Persistence Context) còn sống hay không.

- @Transactional → quản lý transaction
- transaction thường gắn với → Session / EntityManager
- Lazy Loading cần → Session còn mở để query thêm dữ liệu

> Nhiều người nghĩ có **@Transactional** là để chống lỗi Lazy Loading
>
> Sai. Mục đích chính của nó là đảm bảo tính toàn vẹn của transaction, Lazy Loading chỉ là hệ quả phụ

## 5. Open Session In View là gì?

## 6. phân biệt JOIN, JOIN FETCH, EntityGraph

## 7. Khi Backend (Java) và Frontend (React) "nói chuyện" với nhau qua REST API: Làm thế nào để đảm bảo an toàn cho các API này? Nếu Frontend gửi một request lên và Backend trả về lỗi 403 Forbidden, sẽ kiểm tra những yếu tố nào đầu tiên để debug?

> Khi Java Backend (thường là Spring Boot) và React Frontend giao tiếp qua REST API, “an toàn” không chỉ là chặn người lạ gọi API, mà còn là đảm bảo:
>
> - đúng người (Authentication)
> - đúng quyền (Authorization)
> - đúng dữ liệu (Validation)
> - đúng nguồn gọi (CORS, CSRF tùy ngữ cảnh)
> - đúng cách truyền dữ liệu nhạy cảm (HTTPS, token handling)

### 7.1 Đảm bảo an toàn cho REST API

#### a. Authentication - Xác thực người dùng

- Phổ biến nhất: JWT token, OAuth2, Session + Cookie

#### b. Authorization – Phân quyền

- 403 thường xảy ra mạnh nhất ở đây.

#### c. Validation – Validate input

- Frontend không đáng tin.
- Sai lầm phổ biến: “Frontend đã validate rồi nên backend khỏi cần”

#### d. HTTPS

- Nếu dùng HTTP thường: token dễ bị sniff, password bị lộ
- Production bắt buộc HTTPS.

#### e. CORS

- React (localhost:3000) gọi Backend (localhost:8080), Khác origin → browser chặn nếu backend không cho phép
- CORS lỗi thường không phải 403 business-level, mà browser block.

#### f. CSRF

- Nếu dùng Session + Cookie → cần CSRF
- Nếu dùng JWT stateless → thường disable CSRF

### 7.2 Khi bị 403 Forbidden → debug gì đầu tiên?

- 401 = chưa xác thực
- 403 = đã xác thực nhưng không đủ quyền
- Bước 1: Token có được gửi không?
- Bước 2: Token backend có parse được không?
- Bước 3: User có đúng role không?
- Bước 4: Prefix ROLE_ có đúng không?
- Bước 5: Cấu hình Security matcher có sai không?
- Bước 6: CSRF có đang chặn không?
- Bước 7: CORS có thật sự là vấn đề không?
- Bước 8: Method Security (@PreAuthorize) có chặn không?
