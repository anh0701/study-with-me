---
layout: default
title: 13.1 Monolithic
parent: Architectural Patterns
description: ""
---

#### Đặc điểm của ứng dụng Monolithic:
- Tất cả trong một khối: Tất cả các tính năng của ứng dụng đều được gói gọn trong một mã nguồn duy nhất.
- Triển khai đồng nhất: Khi thay đổi hoặc nâng cấp bất kỳ tính năng nào, toàn bộ ứng dụng sẽ cần phải được triển khai lại.
- Đơn giản trong giai đoạn đầu: Với kích thước nhỏ và cấu trúc đơn giản, ứng dụng monolithic dễ dàng phát triển và triển khai ban đầu.
- Quản lý mã nguồn dễ dàng: Tất cả mã nguồn được lưu trong một kho chứa, giúp dễ dàng kiểm soát và quản lý.
#### Ưu điểm:
- Đơn giản và dễ triển khai: Không cần phải lo lắng về việc quản lý các dịch vụ khác nhau hoặc các giao tiếp giữa các dịch vụ.
- Dễ dàng phát triển ban đầu: Thích hợp cho các ứng dụng nhỏ hoặc khi nhóm phát triển có ít kinh nghiệm.
- Ít yêu cầu về hạ tầng: Không cần cấu hình phức tạp cho việc giao tiếp giữa các dịch vụ như trong kiến trúc microservices.
#### Nhược điểm:
- Khó mở rộng: Khi ứng dụng trở nên lớn hơn, việc mở rộng và bảo trì sẽ trở nên khó khăn vì mọi thứ đều được chứa trong một ứng dụng duy nhất.
- Khó cập nhật và triển khai: Nếu một phần của ứng dụng thay đổi, bạn sẽ phải triển khai lại toàn bộ ứng dụng, dẫn đến rủi ro cao hơn.
- Không linh hoạt: Việc sử dụng các công nghệ khác nhau cho các phần khác nhau của ứng dụng sẽ khó khăn hơn vì tất cả các phần đều phải được triển khai chung một nền tảng.
#### Khi nào nên dùng ứng dụng Monolithic?
- Khi dự án nhỏ hoặc mới bắt đầu và đội phát triển chưa đủ lớn.
- Khi ứng dụng không yêu cầu khả năng mở rộng hoặc phân chia thành nhiều phần nhỏ.
- Khi bạn muốn đơn giản hóa việc phát triển và triển khai trong giai đoạn đầu của dự án.
> Tuy nhiên, khi ứng dụng phát triển, việc chuyển sang một kiến trúc như Microservices (dịch vụ vi mô) có thể là một lựa chọn hợp lý để cải thiện khả năng mở rộng và bảo trì
