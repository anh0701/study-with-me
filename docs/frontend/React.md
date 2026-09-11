---
layout: default
title: 31.1. React
parent: 31. Frontend
description: ""
has_toc: side_bar 
---

# React

## 1. Nền tảng Frontend

Hãy tưởng tượng xây dựng một trang web giống như xây nhà.

- **HTML (HyperText Markup Language)**: Là khung xương. Nó xác định cấu trúc: đâu là tiêu đề, đâu là đoạn văn, đâu là nút bấm.
- **CSS (Cascading Style Sheets)**: Là nội thất và sơn tường. Nó quyết định màu sắc, kích thước, vị trí và độ đẹp mắt của ngôi nhà. [Xem thêm](../css/index.md)
- **JavaScript (JS)**: Là hệ thống điện nước. Nó tạo ra sự tương tác: khi bấm công tắc thì đèn sáng, khi mở vòi thì nước chảy.

### Mô hình DOM (Document Object Model)

Khi trình duyệt đọc code HTML của bạn, nó tạo ra một "cây" gọi là DOM. JavaScript sẽ tác động vào cây này để thay đổi nội dung trang web mà không cần tải lại toàn bộ trang.

## 2. Tại sao lại là React?

Khi ứng dụng web trở nên phức tạp, việc quản lý hàng nghìn dòng code JavaScript thuần (Vanilla JS) để cập nhật DOM trở thành một cơn ác mộng. React ra đời với hai triết lý cốt lõi:

- **Component-Based (Dựa trên thành phần)**: Chia nhỏ giao diện thành các mảnh độc lập (như miếng ghép Lego). Bạn có thể tái sử dụng `Button`, `Navbar`, hay `UserCard` ở bất cứ đâu.
- **Declarative (Lập trình khai báo)**: Bạn chỉ cần mô tả giao diện bạn muốn trông như thế nào ở một trạng thái nhất định, React sẽ lo việc cập nhật DOM thật hiệu quả.

## 3. Các khái niệm trong React

### A. JSX (JavaScript XML)

JSX cho phép chúng ta viết HTML ngay trong JavaScript.

```jsx
const element = <h1>Chào mừng bạn đến với lớp học React!</h1>;
```

### B. Props & State (Dữ liệu)

- **Props (Properties)**: Là dữ liệu truyền từ ngoài vào Component (giống như tham số hàm). Props là bất biến (read-only) đối với Component nhận nó.
- **State**: Là "trạng thái" nội bộ của Component. Khi State thay đổi, React sẽ tự động vẽ lại (re-render) Component đó trên màn hình.

### C. Virtual DOM (DOM ảo)

Thay vì sửa trực tiếp vào DOM thật của trình duyệt (vốn rất chậm), React tạo ra một bản sao nhẹ hơn. Khi có thay đổi, nó so sánh bản cũ và bản mới, sau đó chỉ cập nhật đúng những chỗ khác biệt vào DOM thật.

## 4. Hooks

- **useState**: Để quản lý trạng thái. Ví dụ: Một biến đếm số lần click chuột.
- **useEffect**: Để xử lý "tác dụng phụ" (side effects). Ví dụ: Gọi API lấy dữ liệu từ server, thiết lập đồng hồ, hoặc thay đổi tiêu đề trang web.

## 5. Lộ trình tư duy (Mindset) cho người mới

- **Chia nhỏ bài toán**: Nhìn vào một thiết kế, hãy phân tích xem nó gồm bao nhiêu Component nhỏ.
- **Luồng dữ liệu một chiều**: Trong React, dữ liệu chảy từ cha xuống con thông qua Props.

## 6. Some question

### 1. Trong React, khi nào sẽ ưu tiên dùng useEffect? nêu một ví dụ mà nếu dùng hook này không khéo sẽ dẫn đến tình trạng "infinite loop" (lặp vô tận)

Hãy coi useEffect như một "cánh cổng" kết nối thế giới thuần khiết của React với thế giới bên ngoài đầy biến động.

#### a. Khi nào ưu tiên dùng useEffect?

Bạn nên dùng useEffect khi cần thực hiện các Side Effects (tác dụng phụ) — tức là những việc nằm ngoài phạm vi vẽ giao diện của React. Cụ thể trong 3 trường hợp phổ biến:

- **Đồng bộ với hệ thống bên ngoài (API/Data Fetching)**: Khi Component vừa hiển thị, bạn cần gọi API để lấy dữ liệu từ server về.
- **Đăng ký các sự kiện (Subscriptions)**: Thiết lập kết nối WebSocket, hoặc lắng nghe các sự kiện của trình duyệt như scroll, resize, keydown.
- **Thao tác trực tiếp với DOM (hiếm gặp)**: Khi bạn cần sử dụng các thư viện bên thứ ba không thuộc về React (như khởi tạo bản đồ Google Maps, biểu đồ Chart.js) lên một phần tử HTML cụ thể.

#### b. Ví dụ về "Infinite Loop" (Lặp vô tận)

##### Kịch bản lỗi

```js
import React, { useState, useEffect } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    // Ý định: Mỗi lần render thì tăng count lên 1
    setCount(count + 1); 
  }, [count]); // <--- THỦ PHẠM Ở ĐÂY

  return <div>Số lần render: {count}</div>;
}
```

##### Tại sao nó lại gây lặp vô tận?

- **Bước 1**: Component render lần đầu, count bằng 0.
- **Bước 2**: **useEffect** chạy vì nó thấy count được liệt kê trong mảng phụ thuộc (dependency array).
- **Bước 3**: Bên trong **useEffect**, bạn gọi setCount(count + 1). Điều này làm thay đổi state.
- **Bước 4**: Vì state thay đổi, React bắt buộc phải render lại Component.
- **Bước 5**: Sau khi render lại, count bây giờ là 1. React kiểm tra mảng phụ thuộc và thấy count đã thay đổi (từ 0 lên 1).
- **Bước 6**: **useEffect** lại được kích hoạt... và quay lại Bước 3.

Kết quả là trình duyệt của bạn sẽ bị treo hoặc báo lỗi _"Maximum update depth exceeded"_ vì vòng lặp này diễn ra hàng nghìn lần mỗi giây.

##### Làm sao để tránh bẫy này?

Có 3 quy tắc vàng để không bao giờ rơi vào vòng lặp vô tận:

- Kiểm tra mảng phụ thuộc (Dependency Array)

> Nếu bạn chỉ muốn chạy **useEffect** một lần duy nhất khi Component vừa "mọc" ra (mount), hãy để mảng rỗng: [].
>
> Nếu bạn dùng một biến bên trong **useEffect**, hãy chắc chắn biến đó có trong mảng phụ thuộc, nhưng đừng thay đổi chính biến đó bên trong **useEffect** trừ khi có điều kiện dừng.

- Sử dụng Functional Update

> Nếu bạn chỉ muốn tăng giá trị dựa trên giá trị cũ mà không muốn đưa chính biến đó vào mảng phụ thuộc:
>
> useEffect(() => {  
>   setCount(prev => prev + 1);  
> }, []); // Chỉ chạy 1 lần, nhưng vẫn cập nhật được state đúng cách

- Tư duy lại: Có thực sự cần **useEffect** không?

> Rất nhiều trường hợp người mới dùng **useEffect** để tính toán dữ liệu từ một dữ liệu khác. Thay vào đó, bạn có thể tính trực tiếp trong lúc render.
>
> Sai: Dùng **useEffect** để tính fullName từ firstName và lastName.
> 
> Đúng: const fullName = firstName + ' ' + lastName; (Viết trực tiếp trong thân Component).

### 2. Giữa việc truyền dữ liệu qua Props và sử dụng Context API, dựa trên tiêu chí nào để quyết định nên dùng cách nào?

Hãy coi Props là việc "gửi bưu điện" (phải qua từng trạm) và Context API là "phát sóng radio" (ai bật đài lên là nghe được). Dưới đây là 4 tiêu chí cốt lõi để bạn ra quyết định:

#### a. Độ sâu của cây Component (Cấp bậc truyền tải)

#### b. Bản chất của dữ liệu (Global vs Local)

#### c. Tần suất thay đổi dữ liệu (Performance)

#### d. Khả năng tái sử dụng Component

### 3. Luồng dữ liệu một chiều: Trong React, dữ liệu chảy từ cha xuống con thông qua Props. Vậy chiều ngược lại thì sao?

Trong React, dữ liệu vẫn luôn tuân thủ nguyên tắc Unidirectional Data Flow (Luồng dữ liệu một chiều). Tuy nhiên, để "gửi" thông tin từ con lên cha, chúng ta sử dụng một kỹ thuật gọi là **Callback Functions**.

#### a. Cơ chế Callback Function

Hãy tưởng tượng cha là một Giám đốc và con là Thư ký.

- **Chiều xuôi (Props)**: Giám đốc đưa cho Thư ký một cái phong bì (dữ liệu).
- **Chiều ngược**: Giám đốc đưa cho Thư ký một cái máy bộ đàm và bảo: "Khi nào khách đến, hãy bấm nút này để báo cho tôi".

Trong React, "máy bộ đàm" chính là một hàm (function) được định nghĩa ở Component cha và truyền xuống Component con dưới dạng một Prop.

```js
// Component Cha
function Parent() {
  const handleChildClick = (data) => {
    console.log("Dữ liệu nhận được từ con:", data);
  };

  return (
    <div style={{ border: '1px solid black', padding: '20px' }}>
      <h2>Tôi là Cha</h2>
      {/* Truyền hàm handleChildClick xuống con qua prop tên là "onNotify" */}
      <Child onNotify={handleChildClick} />
    </div>
  );
}

// Component Con
function Child({ onNotify }) {
  return (
    <div style={{ border: '1px dotted red', padding: '10px' }}>
      <h3>Tôi là Con</h3>
      <button onClick={() => onNotify("Con đã làm xong bài tập!")}>
        Báo cáo cho Cha
      </button>
    </div>
  );
}
```

#### b. Tại sao React lại làm như vậy? Tại sao không cho phép Component con sửa thẳng dữ liệu của cha?

- **Dễ kiểm soát (Predictability)**: Nếu con có thể tự ý sửa dữ liệu của cha, và bạn có 10 Component con cùng sửa một biến, bạn sẽ không bao giờ biết lỗi phát sinh từ đâu (đây gọi là "side effects" khó kiểm soát).
- **Dễ gỡ lỗi (Debugging)**: Dữ liệu chỉ thay đổi tại nơi nó "sinh ra" (nơi đặt state). Nếu có lỗi, bạn chỉ cần kiểm tra Component cha.

#### c. Các cách liên lạc "nâng cao" khác

Khi ứng dụng của bạn phình to ra, việc truyền hàm qua 5-7 tầng Component (gọi là Prop Drilling) sẽ rất mệt mỏi. Lúc đó chúng ta có các giải pháp:

- **Lifting State Up (Nâng trạng thái lên)**: Nếu hai Component anh em muốn nói chuyện với nhau, chúng ta đặt dữ liệu chung ở Component cha của cả hai.
- **Context API**: Tạo ra một "vùng phủ sóng wifi" toàn cầu. Bất cứ Component con nào (dù sâu đến đâu) cũng có thể kết nối và lấy dữ liệu/hàm mà không cần truyền qua từng cấp.
- **State Management (Zustand, Redux...)**: Một kho chứa dữ liệu riêng biệt nằm ngoài cây Component, nơi bất kỳ ai cũng có thể gửi tín hiệu và nhận dữ liệu.
