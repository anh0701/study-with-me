---
layout: default
title: 16. Message Brokers
description: ""
---

# Message Brokers

## Routing message

## Filtering

## Publish/subcribe

## Retry

## Persistence

## Load balancing

## Transformation

## Message Queue

| Thuật ngữ      | Ý nghĩa                  |
| -------------- | ------------------------ |
| Message Queue  | Cơ chế hàng đợi message  |
| Message Broker | Phần mềm quản lý message |

> Vì sao khi bấm đặt hàng là mình nhận được ngay thông báo thành công. Trong khi rõ ràng ngay sau đó có cả tá việc cần xử lý?
> Những việc làm đó đã được gửi cho Message Queue.

- Message Queue hoạt động như phòng chờ thông minh cho các công việc, nó như một vách ngăn tách biệt yêu cầu chính khỏi công việc xử lý nền.

- Cơ chế hoạt động: The Producer (Người gửi tin nhắn) -> Queue (Nơi tin nhắn ngồi đợi chờ) -> Consumer (Người làm việc).

- Tại sao phải làm vậy?
    - Tạo cảm giác tức thời, và dễ mở rộng (chỉ cần gắn thêm consumer vào là hệ thống có thể gắn được nhiều việc hơn)
    - Độ tin cậy, đảm bảo không một yêu cầu nào bị bỏ xót
    - khả năng chịu tải đột biến, giúp hệ thống ổn định khi có một lượng lớn truy cập.
