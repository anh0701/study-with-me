---
layout: default
title: Draft
# parent: 31. Frontend
description: ""
# has_toc: side_bar 
---

# React

### 1. `useEffect` dùng để làm gì?

> `useEffect` dùng để xử lý các side effect trong component, tức là những việc xảy ra ngoài quá trình render UI.
> Ví dụ như gọi API, đăng ký event listener, timer hoặc theo dõi một giá trị thay đổi.
> Nó chạy sau khi component render và có thể có cleanup function để dọn dẹp.

Ví dụ:

```tsx
useEffect(() => {
  fetchUsers();

  return () => {
    // cleanup
  };
}, []);
```

Nếu interviewer hỏi thêm dependency:

> Dependency array quyết định khi nào effect chạy lại. `[]` thì thường chạy một lần sau lần render đầu tiên, còn `[userId]` thì chạy lại khi `userId` thay đổi.

---

### 2. Khi nào component re-render?

> Component có thể re-render khi **state thay đổi**, **props thay đổi**, hoặc **component cha re-render**. Ngoài ra, khi context mà component đang sử dụng thay đổi thì component cũng có thể re-render.

Ví dụ:

```tsx
const [count, setCount] = useState(0);

setCount(count + 1);
```

→ state thay đổi → component render lại.

Có thể nói thêm:

> Re-render không có nghĩa là toàn bộ DOM hoặc toàn bộ UI đều bị tạo lại; React sẽ tính toán phần nào thực sự cần update.

---

### 3. `useMemo` và `useCallback` khác nhau như nào?

Câu này nên trả lời **rất rõ**:

> `useMemo` dùng để memoize **kết quả của một phép tính**, còn `useCallback` dùng để memoize **function**.

Ví dụ:

```tsx
const total = useMemo(() => {
  return calculateTotal(products);
}, [products]);
```

`total` → giá trị được memoize.

```tsx
const handleClick = useCallback(() => {
  doSomething(id);
}, [id]);
```

`handleClick` → function được memoize.

Có thể chốt:

> `useMemo` nhớ **value**, `useCallback` nhớ **function**.

---

### 4. Props và State khác nhau như nào?

> Props là dữ liệu được truyền từ component cha xuống component con và component con không nên tự thay đổi props đó.
>
> State là dữ liệu thuộc về component và có thể thay đổi thông qua setter, khi state thay đổi thì component có thể re-render.

Ví dụ:

```tsx
<UserCard name="Anh" />
```

`name` là props.

```tsx
const [isOpen, setIsOpen] = useState(false);
```

`isOpen` là state.

Một câu dễ nhớ:

> **Props dùng để truyền dữ liệu, State dùng để quản lý dữ liệu có thể thay đổi.**

---

# React Native

### 5. React Native khác ReactJS như nào?

Đây là câu **rất quan trọng** với JD bạn đang nhắm tới.

> ReactJS chủ yếu dùng để xây dựng web UI, còn React Native dùng React để xây dựng ứng dụng mobile Android và iOS.
>
> ReactJS render ra HTML như `div`, `button`, còn React Native sử dụng các component như `View`, `Text`, `Image`, `Pressable`.
>
> Tuy nhiên cả hai đều sử dụng React concepts như component, props, state, hooks và lifecycle.

Có thể nói thêm:

> Vì vậy nếu đã biết React thì việc học React Native sẽ dễ hơn vì phần tư duy React có thể dùng lại.

---

### 6. React Native giao tiếp với native code như thế nào?

Trả lời junior:

> React Native có một lớp kết nối giữa JavaScript và native platform. JavaScript có thể gọi các native API thông qua các native module hoặc native libraries.
>
> Ví dụ những chức năng như camera, GPS, Bluetooth hoặc một số API của Android/iOS có thể được expose cho JavaScript để sử dụng.

Nếu interviewer hỏi sâu về architecture:

> Các phiên bản React Native hiện đại sử dụng kiến trúc mới với **JSI, Fabric và TurboModules**, giúp việc giao tiếp giữa JavaScript và native hiệu quả hơn.

**Không cần tự lao vào giải thích JSI nếu interviewer không hỏi tiếp.**

---

### 7. Vì sao app React Native có thể chạy Android và iOS?

> Vì phần business logic và UI code có thể được viết bằng JavaScript/TypeScript và React Native cung cấp các abstraction cho Android và iOS.
>
> React Native sẽ sử dụng implementation tương ứng của từng platform để render và thực hiện các chức năng native.

Ví dụ:

```tsx
<View>
  <Text>Hello</Text>
</View>
```

Cùng code có thể chạy trên Android và iOS.

Nhưng nên thêm:

> Tuy nhiên không có nghĩa là 100% code luôn giống nhau. Những chức năng đặc thù của từng platform đôi khi vẫn cần viết hoặc cấu hình native code riêng.

---

### 8. Khi nào cần native module?

> Khi React Native không cung cấp API cần thiết hoặc khi mình cần sử dụng một chức năng native đặc thù mà JavaScript không thể xử lý trực tiếp.
>
> Ví dụ như một SDK Android/iOS riêng, Bluetooth đặc biệt, một thư viện camera native hoặc một chức năng cần tối ưu native.

Câu này rất ổn:

> Nếu đã có một thư viện React Native ổn định hỗ trợ chức năng đó thì em sẽ ưu tiên sử dụng thư viện thay vì tự viết native module.

---

# API

### 9. Bạn xử lý token hết hạn như nào?

Câu này nên trả lời theo flow:

> Khi access token hết hạn, API thường trả về `401`.
>
> App sẽ dùng refresh token để gọi API refresh token và lấy access token mới.
>
> Sau đó cập nhật access token và retry request ban đầu.
>
> Nếu refresh token cũng hết hạn hoặc không hợp lệ thì đưa người dùng về màn hình login.

Flow:

```text
API request
    ↓
401
    ↓
Refresh token
    ↓
Get new access token
    ↓
Retry request
```

---

### 10. Access token và refresh token khác nhau như nào?

> Access token dùng để xác thực các request đến API và thường có thời gian sống ngắn.
>
> Refresh token dùng để lấy access token mới khi access token hết hạn và thường có thời gian sống dài hơn.
>
> Vì access token được gửi thường xuyên nên thời gian sống ngắn giúp giảm rủi ro nếu token bị lộ.

---

### 11. Nếu API đang loading thì UI làm gì?

> Em sẽ thể hiện trạng thái loading để người dùng biết hệ thống đang xử lý, đồng thời hạn chế những thao tác có thể tạo request trùng.
>
> Tùy trường hợp có thể dùng loading indicator, skeleton hoặc disable button.

Ví dụ:

```tsx
if (loading) {
  return <ActivityIndicator />;
}
```

Với button:

```tsx
<Button
  title="Login"
  disabled={loading}
/>
```

---

### 12. Nếu API trả 401 thì xử lý như nào?

> Em sẽ kiểm tra nguyên nhân 401. Nếu access token hết hạn thì thực hiện refresh token và retry request.
>
> Nếu refresh token không còn hợp lệ thì clear authentication state và đưa user về login.

**Không nên nói:** cứ 401 là logout ngay.

Vì có thể access token chỉ vừa hết hạn và refresh được.

---

# Mobile

### 13. GPS cần permission như nào?

> GPS cần quyền truy cập vị trí của người dùng. Android và iOS đều có cơ chế permission riêng.
>
> App cần khai báo permission và request permission trong runtime trước khi lấy location.
>
> Nếu user từ chối thì app cần xử lý trường hợp không có quyền thay vì crash.

Có thể nói thêm:

> Với một số trường hợp như background location thì permission còn chặt chẽ hơn foreground location.

---

### 14. Push notification hoạt động như nào?

Bạn có thể trả lời đơn giản:

> App thường đăng ký với notification service để lấy device token.
>
> Token được gửi lên backend. Khi cần gửi notification, backend gửi message đến push notification service, sau đó service chuyển notification đến thiết bị.
>
> App có thể xử lý notification khi app đang foreground, background hoặc được mở từ notification.

Flow:

```text
Mobile App
    ↓
Device Token
    ↓
Backend
    ↓
Push Notification Service
    ↓
Android / iOS
```

Ví dụ service thường gặp là FCM trên Android và APNs trên iOS.

---

### 15. Camera lấy ảnh rồi upload server như nào?

> Đầu tiên app request camera permission, sau đó sử dụng camera API hoặc thư viện camera để chụp ảnh.
>
> Sau khi có file ảnh, app có thể tạo `FormData` và upload lên server thông qua REST API.
>
> Server thường trả về URL hoặc ID của file sau khi upload thành công.

Ví dụ concept:

```text
Camera
 ↓
Image file
 ↓
FormData
 ↓
POST /upload
 ↓
Server
 ↓
Image URL
```

---

### 16. `FlatList` khác `ScrollView` như nào?

Đây là câu **rất nên nhớ**.

> `ScrollView` thường render toàn bộ các phần tử trong danh sách, nên phù hợp với nội dung ít.
>
> `FlatList` được tối ưu cho danh sách lớn bằng cách chỉ render những item cần thiết trong vùng hiển thị, đồng thời hỗ trợ các tính năng như virtualization, pagination và pull-to-refresh.

### Khi nào dùng FlatList?

> Khi em có một danh sách có nhiều item hoặc số lượng item có thể lớn thì em sẽ ưu tiên `FlatList`.

Ví dụ:

```tsx
<FlatList
  data={users}
  renderItem={({ item }) => <UserItem user={item} />}
  keyExtractor={(item) => item.id}
/>
```

Còn:

```tsx
<ScrollView>
  <Text>...</Text>
  <Text>...</Text>
  <Text>...</Text>
</ScrollView>
```

→ nội dung ít, không phải list lớn.

**Câu chốt rất tốt khi phỏng vấn:**

> Nếu là danh sách vài item cố định thì em có thể dùng `ScrollView`, còn danh sách lớn hoặc dynamic thì em ưu tiên `FlatList` để tối ưu memory và performance.

---

# Performance

### 17. Tại sao app bị lag khi scroll?

Có nhiều nguyên nhân, nhưng nếu interviewer hỏi thì trả lời:

> Một số nguyên nhân có thể là render quá nhiều item, component item quá nặng, xử lý logic hoặc tính toán trong mỗi lần render, ảnh có kích thước lớn, hoặc tạo lại function/object không cần thiết.
>
> Với `FlatList`, nếu cấu hình hoặc cách render item không phù hợp thì scrolling cũng có thể bị lag.

---

### 18. Làm thế nào tối ưu `FlatList`?

Đừng cố liệt kê 20 thứ. Nói khoảng 4–5 thứ:

> Em sẽ:
>
>   - Dùng `keyExtractor` ổn định.
>   - Tối ưu component item, có thể dùng `React.memo`.
>   - Tránh tạo object/function không cần thiết trong render.
>   - Cấu hình `initialNumToRender`, `windowSize` phù hợp.
>   - Nếu item có kích thước cố định thì có thể dùng `getItemLayout`.
>   - Tối ưu kích thước và việc load ảnh.

Ví dụ:

```tsx
const UserItem = React.memo(({ user }) => {
  return <Text>{user.name}</Text>;
});
```

---

### 19. Vì sao nhiều ảnh khiến app chậm?

> Vì ảnh có thể chiếm nhiều memory, đặc biệt nếu ảnh có độ phân giải lớn.
>
> Khi có nhiều ảnh cùng lúc, app phải tải, decode và render nhiều dữ liệu nên có thể gây tốn memory và ảnh hưởng scrolling.
>
> Em sẽ tối ưu bằng cách resize/compress ảnh, dùng thumbnail, lazy loading và cache ảnh khi phù hợp.

Có thể nói thêm:

> Đặc biệt trên mobile, memory có giới hạn nên việc quản lý image size khá quan trọng.

---

### 20. Làm sao giảm unnecessary re-render?

> Trước tiên em xác định component nào đang re-render không cần thiết. Sau đó có thể dùng `React.memo` cho component phù hợp, `useMemo` cho những phép tính tốn chi phí và `useCallback` khi cần giữ reference của function ổn định.
>
> Ngoài ra em cũng tránh đưa state không cần thiết lên component cha vì khi state của cha thay đổi có thể khiến nhiều component con render lại.

Một điểm quan trọng:

> Không nên lạm dụng `useMemo` và `useCallback`, vì bản thân chúng cũng có overhead. Chỉ dùng khi thực sự có lợi.

Câu này **ghi điểm khá tốt** vì thể hiện bạn hiểu chứ không phải học thuộc.

---

# Release

### 21. APK và AAB khác nhau như nào?

Trả lời:

> APK là package có thể cài trực tiếp lên Android device.
>
> AAB, Android App Bundle, là format được Google Play sử dụng để nhận bundle của ứng dụng và sau đó tạo ra APK phù hợp với từng thiết bị.
>
> Vì vậy khi phát hành Google Play thì thường build AAB, còn APK thường tiện cho việc cài đặt hoặc testing trực tiếp.

Có thể nhớ:

```text
APK → cài trực tiếp

AAB → upload Google Play
       ↓
Google Play tạo APK phù hợp
```

---

### 22. Bạn đã từng release app chưa?

Nếu **chưa**, đúng như bạn nói thì **đừng nhận đã từng release**.

Mình sẽ chỉnh câu của bạn một chút để nghe tự nhiên hơn khi phỏng vấn:

> **Em chưa trực tiếp phát hành ứng dụng production lên Google Play hoặc App Store. Tuy nhiên em đã tìm hiểu về quy trình build release, signing và deployment của React Native. Em cũng có thể tự setup project và thực hành quy trình build release để hiểu rõ hơn về quá trình này.**

Nếu interviewer hỏi:

**"Vậy em có biết build Android release không?"**

Bạn có thể nói:

> **Dạ có tìm hiểu. Với Android thì có thể build release APK hoặc AAB, đồng thời cần cấu hình signing keystore trước khi phát hành. Nếu là Google Play thì em sẽ ưu tiên AAB.**

Nếu hỏi tiếp:

**"Còn iOS?"**

> **iOS cần cấu hình signing, certificate và provisioning profile, sau đó có thể archive app và upload lên App Store Connect để thực hiện quá trình phát hành. Em chưa trực tiếp làm production release nhưng em hiểu các bước chính của quy trình.**

---

| Câu | Ý chính cần nhớ |
| --- | --- |
| `useEffect` | Side effect |
| Re-render | State / props / parent / context thay đổi |
| `useMemo` | Memoize **value** |
| `useCallback` | Memoize **function** |
| Props vs State | Props truyền vào, State quản lý dữ liệu thay đổi |
| RN vs ReactJS | Mobile vs Web |
| Native module | Khi cần native API/chức năng đặc thù |
| 401 | Refresh token → retry → nếu fail thì login |
| FlatList | List lớn, virtualization |
| APK vs AAB | APK cài trực tiếp, AAB cho Play Store |
