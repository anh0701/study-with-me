---
layout: default
title: 30. Spring boot
description: ""
---

# Spring boot

## 1. Phân biệt `@Controller` và `@RestController`

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
> - query phình to
> - cartesian product
> - memory tăng mạnh
> - khó kiểm soát SQL
> Senior dev thường mặc định dùng LAZY, chủ động fetch đúng nơi cần, chứ không dùng EAGER bừa bãi

## 3. LazyInitializationException là gì?

## 4. vì sao @Transactional ảnh hưởng tới lazy loading?

## 5. Open Session In View là gì?

## 6. phân biệt JOIN, JOIN FETCH, EntityGraph
