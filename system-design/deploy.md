---
layout: default
title: 25.1 Deploy không downtime
parent: 25. System Design
description: ""
permalink: /deploy-khong-downtime/
---

# Deploy không downtime

> Làm sao deploy code mà hệ thống không downtime một giây?

- Vấn đề việc phiên bản mới chứa lỗi nghiêm trọng, việc quay lại phiên bản cũ chậm chạp.
- **Giải pháp 1**: Blue and Green: có 2 môi trường giống hệt nhau và một công tắc. Thay vì cố sửa chiếc xe trên đường cao tốc, thì chúng ta chế tạo một chiếc xe y hệt hòan hảo bên cạnh nó. Nghĩa là chúng ta có 2 môi trường sản xuất giống hệt nhau, một cái tên là blue, một cái là green, cùng hoạt động song song.

    - Đầu tiên môi trường Blue hoạt động phục vụ người dùng, cùng lúc đó trong nhà kho, phiên bản mới được triển khai lên môi trường Green và được kiểm thử cực kì kĩ lưỡng, và mọi thứ đã sẵn sàng, chúng ta chỉ cần bật công tắc, chuyển mọi người dùng (traffic) từ Blue sang Green ngay lập tức. Khi có lỗi, chỉ cần chuyển traffic về Blue là xong.
    - Ưu điểm: Không downtime khi deploy, Rollback tức thì không rủi ro
    - Nhược điểm: Yêu cầu gấp đôi cơ sở hạ tầng, gây tốn kém chi phí

- **Giải pháp 2**: Canary: Tung ra phiên bản mới theo % người dùng để đảm bảo an toàn trước khi mở rộng ra toàn bộ. Từ 1% -> 5% -> 10% -> 20% -> ... -> 100%. Nếu có lỗi thì chỉ một số người dùng nhỏ ảnh hưởng và rollback rất dễ dàng
    - Ưu điểm: Cực kì an toàn, giảm thiểu rủi ro, phát hiện lỗi với phạm vi ảnh hưởng nhỏ
    - Nhược điểm: quá trình rollout (triển khai thực tế) khá dài, đòi hỏi hệ thống giám sát thời gian thực.

> Nên chọn chiến lược nào??

- Blue and Green: Nếu chuyển 100% traffic một lần phù hợp cập nhật lớn cần rollback nhanh.
- Canary: Phát hành theo % người dùng phù hợp cập nhật nhỏ, thường xuyên, cần giảm thiểu rủi ro là ưu tiên hàng đầu.
