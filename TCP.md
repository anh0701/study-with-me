---
layout: default
title: 01. TCP
description: ""
---

### TCP

**TCP (Transmission Control Protocol)** là một giao thức truyền tải dữ liệu quan trọng trên Internet. Nó đảm bảo rằng dữ liệu được truyền tải một cách tin cậy và theo đúng thứ tự giữa các thiết bị mạng.

#### Cách hoạt động của TCP

1. **Thiết lập kết nối (Three-way Handshake)**:
    - **SYN**: Máy khách gửi một gói SYN (synchronize) để yêu cầu kết nối.
    - **SYN-ACK**: Máy chủ phản hồi bằng gói SYN-ACK (synchronize-acknowledge) để xác nhận yêu cầu.
    - **ACK**: Máy khách gửi lại gói ACK (acknowledge) để hoàn tất quá trình thiết lập kết nối.
2. **Truyền dữ liệu**:
    - Dữ liệu được chia thành các phân đoạn (segment) nhỏ hơn.
    - Mỗi phân đoạn được đánh số thứ tự để đảm bảo dữ liệu đến đúng thứ tự.
    - TCP sử dụng cơ chế kiểm tra lỗi và xác nhận để đảm bảo dữ liệu được truyền tải mà không bị mất mát hoặc lỗi.
3. **Kiểm soát luồng dữ liệu**:
    - TCP sử dụng cơ chế cửa sổ trượt (sliding window) để điều chỉnh lượng dữ liệu được truyền đi, giúp tránh tình trạng quá tải mạng.
4. **Kết thúc kết nối**:
    - Khi việc truyền dữ liệu hoàn tất, kết nối TCP được ngắt bằng cách gửi các gói FIN (finish) từ cả hai phía.

TCP là một phần không thể thiếu của bộ giao thức TCP/IP, giúp đảm bảo việc truyền tải dữ liệu trên Internet một cách hiệu quả và tin cậy.