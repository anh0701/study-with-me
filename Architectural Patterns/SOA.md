---
layout: default
title: 13.3 SOA
parent: 13. Architectural Patterns
description: ""
permalink: /soa/
---

### SOA

SOA architectural patterns là những mẫu thiết kế cơ bản được sử dụng trong kiến trúc phần mềm theo kiểu dịch vụ (Service-Oriented Architecture - SOA).
Những mẫu này giúp xây dựng các hệ thống phức tạp, tăng cường tái sử dụng và khả năng tương thích giữa các thành phần phần mềm.

#### Một số mẫu kiến trúc SOA phổ biến

1. Aggregator Pattern: kết hợp các message riêng lẻ thành một đơn vị duy nhất để xử lý.
2. Broker Pattern: Sử dụng một trung gian (broker) để quản lý giao tiếp giữa các dịch vụ và người dùng.
3. Service Registry Pattern: Lưu trữ các dịch vụ trong một danh sách để dễ dàng tìm kiếm và sử dụng lại.
4. Facade Pattern: Cung cấp một giao diện đơn giản cho một nhóm các dịch vụ phức tạp.
5. Publish/Subscribe Pattern: Các dịch vụ gửi thông tin (publish) và các dịch vụ khác nhận thông tin (subscribe) thông qua một trung gian.
6. Request/Reply Pattern: một dịch vụ nhận yêu cầu từ người dùng và trả lời ngay lập tức.

#### Lợi ích của SOA architectural patterns:

- Tính tái sử dụng cao: Các dịch vụ có thể được sử dụng lại trong nhiều ứng dụng khác nhau.
- Khả năng tương thích: Các dịch vụ có thể giao tiếp với nhau qua các giao thức và ngôn ngữ khác nhau.
- Tự động hóa: Giảm thiểu sự phụ thuộc giữa các ứng dụng và dễ dàng triển khai thay đổi.

