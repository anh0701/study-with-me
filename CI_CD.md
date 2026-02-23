---
layout: default
title: 12. CI/CD
nav_order: 2
description: ""
---

### CI/CD

- CI/CD viết tắt của Continuous Integration (Tích hợp liên tục) và Continuous Delivery/Deployment (Triển khai liên tục).
Đây là một phương pháp phát triển phần mềm hiện đại giúp tăng cường tự động hóa và cải thiện quy trình phát triển, thử nghiệm và triển khai phần mềm.

#### Continuous Integration (CI)

CI là quá trình tự động tích hợp các thay đổi mã nguồn từ nhiều nhà phát triển vào một nhánh chung nhiều lần trong ngày. 
Mục tiêu của CI là phát hiện sớm và khắc phục các lỗi trong mã nguồn bằng cách liên tục xây dựng và kiểm thử ứng dụng.
- Lợi ích:

  - Phát hiện sớm lỗi: Giúp phát hiện sớm các lỗi phát sinh khi tích hợp mã.
  - Tăng cường cộng tác: Giúp các nhà phát triển làm việc cùng nhau trên cùng một nhánh mã.
  - Tự động hóa: Giảm bớt thời gian kiểm thử bằng cách tự động hóa quá trình xây dựng và kiểm thử.
  
#### Continuous Delivery/Deployment (CD)

CD bao gồm Continuous Delivery và Continuous Deployment.

- Continuous Delivery: Qúa trình tự động hóa việc xây dựng, kiểm thử và chuẩn bị phần mềm để triển khai. 
Mục tiêu của Continuous Delivery là đảm bảo rằng phần mềm luôn sẵn sàng để triển khai bất cứ lúc nào.
- Continuous Deployment: là một bước tiến xa hơn của Continuous Delivery, trong đó các thay đổi được tự động triển khai vào môi trường sản xuất mà không cần sự can thiệp thủ công.
- Lợi ích: 
  - Triển khai nhanh chóng: giúp triển khai các thay đổi nhanh chóng và thường xuyên hơn.
  - Giảm rủi ro: Triển khai từng phần nhỏ giúp giảm thiểu rủi ro và dễ dàng phát hiện lỗi.
  - Phản hồi nhanh: Giúp phản hồi nhanh chóng với phản hồi của người dùng và thay đổi yêu cầu.

#### Quy trình CI/CD cơ bản:

1. Commit Code: Nhà phát triển commit mã nguồn vào hệ thống kiểm soát phiên bản (như Git).
2. Build: Hệ thống CI tự động xây dựng ứng dụng từ mã nguồn.
3. Test: Hệ thống CI tự động chạy các kiểm thử đơn vị (unit test) và kiểm thử tích hợp.
4. Deploy: Hệ thống CD tự động triển khai ứng dụng vào các môi trường kiểm thử và sản xuất.

#### Công cụ phổ biến cho CI/CD

- Jenkins: Một công cụ CI/CD mã nguồn mở phổ biến.
- GitLab CI/CD: Tích hợp sẵn trong GitLab và hỗ trợ cả CI và CD
- CircleCI: một dịch vụ CI/CD mạnh mẽ và dễ sử dụng.
- Travis CI: một dịch vụ CI/CD phổ biến khác dành cho các dự án mã nguồn mở và doanh nghiệp.

> CI/CD giúp nâng cao hiệu suất làm việc, tăng cường tính tự động hóa và giảm bớt thời gian triển khai ứng dụng.
