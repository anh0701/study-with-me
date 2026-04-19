---
layout: default
title: File Nháp
nav_exclude: true
---

# HTTP

## Các mô hình backend

### Client server

```sh
Client (browser, mobile app)
    ↓  request
Server (backend app)
    ↓
Database

```

- client gửi request, server xử lý logic trả về response
- Stateless: mỗi request độc lập

### 3-Tier Architecture

```sh
Presentation Layer (UI)
   ↓
Application Layer (Business logic)
   ↓
Data Layer (Database)
```

- Presentation layer: giao diện (frontend):

    - Là nơi người dùng tương tác: web UI, mobile app, desktop app.
    - Gửi request HTTP đến backend.
    - Hiển thị kết quả từ backend (HTML, JSON, View Model…).

- Business logic layer: xử lý nghiệp vụ (validation, rule, transaction):
    - Tầng này nằm trong backend.
    - Xử lý toàn bộ logic nghiệp vụ: Validate dữ liệu, Tính toán, xử lý rule, Gọi repository để truy vấn DB
    - Ví dụ trong Spring Boot: các class @Service, @Controller.

- Data access layer: đọc/ghi dữ liệu từ DB:
    - Là nơi giao tiếp với database hoặc external storage.
    - Chịu trách nhiệm lưu, truy xuất, chuyển đổi dữ liệu.
    - Ví dụ: @Repository trong Spring, DAO trong Java, ORM trong Laravel/Express.


### N-Tier Architecture

- Giống 3-tier, nhưng chia nhiều tầng hơn nếu hệ thống lớn:

    - API layer
    - Authentication layer
    - Business service layer
    - Data access layer
    - Caching layer

### Microservices Architecture

```sh

[User Service]      [Order Service]      [Payment Service]
       ↓                    ↓                    ↓
      DB1                  DB2                  DB3
```

- Mỗi service có DB riêng → không phụ thuộc nhau
- Giao tiếp bằng REST API, gRPC, Kafka, RabbitMQ...
- Triển khai độc lập, scale từng phần được

### Serverless Architecture

- Không có “server backend” cố định; bạn chỉ viết các function xử lý (lambda function) chạy khi có event.

```sh
Client → API Gateway → Lambda Function → Database
```

- Dùng trong: ứng dụng nhỏ, hệ thống event-driven.

### Event-driven Architecture

- Các service không gọi trực tiếp nhau, mà gửi “sự kiện” (event).
Ví dụ: khi “UserCreated” → gửi event → “EmailService” nhận và gửi email.
- Ưu điểm: giảm coupling, dễ mở rộng
- Nhược điểm: khó trace flow, cần hiểu rõ message queue

### Microfrontend + Backend-for-Frontend (BFF)

- Dành cho hệ thống có nhiều frontend (web, mobile, admin…).
- Mỗi loại client sẽ có backend riêng (BFF) để trả đúng dữ liệu cần thiết.
- Dùng trong: hệ thống có nhiều UI khác nhau.

> Khi bạn gõ facebook.com rồi nhấn Enter, chuyện gì xảy ra trong 1 giây đó?

## HTTP

```sh
# Cấu trúc 1 http request

GET /api/users HTTP/1.1         ← Status line
Host: example.com               ← Header
Authorization: Bearer <token>   ← Body

# Cấu trúc 1 response

HTTP/1.1 200 OK                 ← Status line
Content-Type: application/json  ← Header
Body: {"id":1,"name":"Anh"}     ← Body

```

- Status line: gồm method, path, protocol hoặc các status code
- Headers: Metadata của request/ response
    > request
    - Content-Type: kiểu dữ liệu gửi đi (JSON, XML, HTML, form-data…)
    - Authorization: token đăng nhập
    - Accept: client mong muốn nhận kiểu dữ liệu nào (JSON, HTML…)
    > response
    - Content-Type: kiểu dữ liệu trả về
    - Set-Cookie: gửi cookie mới cho client
    - Cache-Control: hướng dẫn cache

- Body: Phần dữ liệu chính (payload) hoặc Dữ liệu thật trả về (HTML, JSON, XML, v.v.)

> 1. Header và Body khác nhau ở điểm nào?
> 2. Khi nào dùng POST thay vì GET?

## Status code & RESTful API

> 1. Vì sao REST API nên stateless?
> 2. /api/users/1/orders diễn tả điều gì?

## Header, cookie, session

> 1. Nếu HTTP là stateless, tại sao ta vẫn “nhớ đăng nhập”?
> 2. Token và cookie khác gì nhau?

## Routing và Endpoint

> 1. Controller có nhiệm vụ gì trong backend?
> 2. Tại sao ta cần chia nhỏ endpoint?

## Câu hỏi tổng hợp

> 1. Response 201 khác gì 200?
> 2. Vì sao server trả về JSON chứ không phải HTML?
> 3. RESTful API là gì?
> 4. Stateless có nghĩa là gì?
> 5. Khi bạn gửi request, những phần nào của HTTP được gửi đi?
> 6. Header dùng để làm gì?