---
layout: default
title: 7.6 Một số bài toán
parent: 07. Database
description: ""
---

# Một số bài toán

## Việc hàng nghìn giao dịch (transaction) ập đến cùng lúc hoặc nhiều người cùng mua online sản phẩm cuối cùng của giỏ hàng

> Để trả lời câu hỏi "Cái nào thành công?", chúng ta cần hiểu rằng Database không để mặc cho các giao dịch "đấm đá" nhau. Nó sử dụng một cơ chế gọi là Locking (Khóa) và các Isolation Levels (Cấp độ cô lập) để làm trọng tài.

### Cơ chế "Cái ghế duy nhất" (Locking)

- Hãy tưởng tượng Database là một rạp chiếu phim và chỉ còn đúng 1 ghế trống cuối cùng
- Transaction A: ấn nút đặt ghế
- Transaction B: cũng ấn nút đặt ghế vào đúng micro giây đó
- Nguyên tắc "First-come, First-served" (Đến trước phục vụ trước): Database sẽ cấp một cái "Exclusive Lock" (Khóa độc quyền) cho người nhanh tay hơn (giả sử là A).
- Khi A đang giữ khóa, B sẽ rơi vào trạng thái Waiting (chờ đợi). B không thể sửa, thậm chí tùy cấu hình mà không thể đọc cái ghế đó.
- Nếu A thành công (Commit): Ghế đã có chủ. B hết chờ và nhận thông báo: "Ghế này đã bị đặt mất rồi!" (Giao dịch B thất bại hoặc phải xử lý logic khác).
- Nếu A gặp lỗi (Rollback): A nhả khóa ra. Lúc này B mới được nhảy vào chiếm lấy ghế và thực hiện tiếp.
- Kết luận: Không bao giờ có chuyện cả hai cùng "thành công" trên cùng một tài nguyên nếu tính Isolation được thực thi nghiêm ngặt. Một cái sẽ thắng, cái còn lại phải chờ hoặc thất bại.

### "Nút vặn" Isolation Levels (Cấp độ cô lập)

> Trong thực tế, việc bắt mọi người phải chờ nhau (Serializable) sẽ làm hệ thống rất chậm. Vì vậy, người ta chia Isolation thành 4 cấp độ (giống như nút vặn điều chỉnh độ "khó" của trọng tài):

#### Cấp 1: Read Uncommitted (Hỗn loạn)

- A đang sửa dữ liệu nhưng chưa xác nhận (chưa Commit).
- B vẫn vào đọc được dữ liệu "nháp" đó của A.
- Rủi ro: Nếu A sau đó hủy lệnh (Rollback), dữ liệu B vừa đọc là dữ liệu rác (Dirty Read).

#### Cấp 2: Read Committed (Tiêu chuẩn - Phổ biến nhất)

- B chỉ được đọc những gì A đã xác nhận (Commit) xong xuôi.
- Đây là mức mặc định của nhiều DB như PostgreSQL, SQL Server. Nó tránh được dữ liệu rác nhưng vẫn có thể gặp hiện tượng dữ liệu thay đổi nếu B đọc đi đọc lại nhiều lần.

#### Cấp 3: Repeatable Read (Nhất quán)

- Nếu B đã đọc một dòng dữ liệu, thì trong suốt quá trình B làm việc, dòng đó sẽ không đổi, dù A có nhảy vào sửa và Commit đi chăng nữa.
- Mức này giúp B yên tâm làm việc mà không sợ bị "đánh úp" giữa chừng.

#### Cấp 4: Serializable (Nghiêm ngặt nhất)

- Các giao dịch xếp hàng một. A làm xong mới tới lượt B.
- An toàn tuyệt đối nhưng chậm kinh khủng. Thường chỉ dùng cho các giao dịch cực kỳ quan trọng như chốt sổ tài chính cuối năm.

### Tóm lại: Ai thắng?

- Pessimistic Locking (Khóa bi quan): Bạn khóa luôn dòng dữ liệu ngay khi có người chạm vào. Người đến sau phải chờ. Người đến trước luôn thắng/ưu tiên thực hiện trước.
- Optimistic Locking (Khóa lạc quan): Bạn cho cả hai cùng đọc, cùng sửa. Nhưng khi đến bước lưu (Save), hệ thống sẽ kiểm tra: "Dữ liệu này có giống lúc nãy bạn đọc không?".

    - A lưu trước -> Thành công.

    - B lưu sau -> Hệ thống thấy dữ liệu đã bị A đổi rồi -> B thất bại và phải thực hiện lại từ đầu (Retry).

### Mẹo ghi nhớ

> Tính Isolation giống như việc bạn đang đi vệ sinh công cộng vậy

- Isolation tốt: Có khóa cửa, người ngoài không vào được, bạn yên tâm làm việc.
- Isolation kém: Đang làm việc mà có người đẩy cửa ngó vào (Dirty Read) hoặc thậm chí xông vào đuổi bạn ra (Concurrency issue).
