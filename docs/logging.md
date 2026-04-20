---
layout: default
title: 26. Logging
description: ""
---

<div class="my-right-toc" markdown="1">
1. TOC
{:toc}
</div>

## 5 loại logging quan trọng trong hệ thống backend

### 1. Request / Response Log

- Log toàn bộ request và response của API.
- Mục đích: debug API, trace user action, phát hiện request lỗi

```sh
{
  "timestamp": "2026-03-11T10:00:01Z",
  "requestId": "abc123",
  "method": "POST",
  "path": "/api/orders",
  "userId": 1024,
  "requestBody": {
    "productId": 10,
    "quantity": 2
  },
  "statusCode": 200,
  "responseTimeMs": 120
}

```

- Dùng khi: API gateway, microservice, public API
- Không log: password, token, credit card

### 2. Business logic log

- Không phải log kiểu: `NullPointException`, mà log theo ngữ cảnh business.

```sh
Order failed: product out of stock
productId=10
userId=1024
```

- Mục tiêu log để hiểu chuyện gì xảy ra chứ không chỉ biết có lỗi.

### 3. Latency log (độ trễ)

- log thời gian xử lý của từng phần hệ thống

```sh
{
  "requestId": "abc123",
  "service": "order-service",
  "latencyMs": 120
}
```

- Dùng để phát hiện bottleneck, slow database, slow API.

### 4. business event log

- log sự kiện business không phải lỗi

```sh
{
  "event": "OrderCreated",
  "orderId": 9012,
  "userId": 1024,
  "total": 120000
}
```

- dùng để analytics, audit, BI, fraud detection

### 5. retry & circuit breaker log

- log khả năng chịu lỗi của hệ thống

```sh
{
  "service": "payment-service",
  "action": "retry",
  "attempt": 2
}
```

## Logging chuẩn

### 1. structured logging

- log dạng json: dễ search, dễ phân tích

### 2. Correlation ID

- mỗi request có requestId
- log ở mội service, nhờ vậy trace được toàn bộ request

### 3. Centralized logging

- log không để local, đẩy vài hệ thống như: elasticsearch, logstash, kibana
- stack này gọi là ELK stack
