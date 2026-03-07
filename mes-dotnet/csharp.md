---
layout: default
title: 23.1 C# core
parent: 23. MES
description: ""
permalink: /csharp/
---

# C# Core

## 1. Cú pháp cơ bản

### 1.1. Kiểu dữ liệu

- int (số nguyên), double/float (số thực), string (chuỗi), bool (true/false).

```csharp
string tenMay = "May Cat Laser";
int soLuongDat = 150;
double nhietDoHienTai = 45.8;
bool dangHoatDong = true;
```

### 1.2. câu lệnh điều kiện

```csharp
// if else
double nhietDoToiDa = 100.0;
double nhietDoThucTe = 105.2;

if (nhietDoThucTe > nhietDoToiDa) 
{
    Console.WriteLine("CANH BAO: Nhiet do qua cao! Dung may ngay lap tuc.");
} 
else 
{
    Console.WriteLine("Trang thai: On dinh.");
}

// else if
int time = 22;
if (time < 10) 
{
  Console.WriteLine("Good morning.");
} 
else if (time < 20) 
{
  Console.WriteLine("Good day.");
} 
else 
{
  Console.WriteLine("Good evening.");
}
// Outputs "Good evening."

// switch case
switch(expression) 
{
  case x:
    // code block
    break;
  case y:
    // code block
    break;
  default:
    // code block
    break;
}

```

### 1.3. vòng lặp

```csharp
// for thường dùng khi biết trước số lượng
for (int i = 1; i <= 5; i++) 
{
    Console.WriteLine($"Dang kiem tra san pham thu: {i}");
}

// while: chạy đến khi không đúng điều kiện nữa
int i = 0;
while (i < 5) 
{
  Console.WriteLine(i);
  i++;
}

```

### 1.4. Mảng (Array) và Danh sách (List)

```csharp
using System.Collections.Generic;

List<string> danhSachLoi = new List<string>();
danhSachLoi.Add("Loi ket noi PLC");
danhSachLoi.Add("Het nguyen lieu");

Console.WriteLine($"So luong loi hien tai: {danhSachLoi.Count}");
```

## 2. OOP

### 2.1. Lớp (Class) và Đối tượng (Object)

- Class (Lớp): Là cái khuôn, bản thiết kế (ví dụ: Bản vẽ kỹ thuật của xe hơi).
- Object (Đối tượng): Là thực thể tạo ra từ khuôn đó (ví dụ: Chiếc Toyota màu đỏ của bạn, chiếc BMW màu xanh của hàng xóm).

```csharp
class Car 
{
    public string model; // Thuộc tính
    public void Drive()  // Hành động (Phương thức)
    {
        Console.WriteLine("Xe đang chạy...");
    }
}

Car myCar = new Car();
myCar.model = "VinFast";
myCar.Drive();
```

### 2.2. 4 tính chất của OOP

- Đóng gói (Encapsulation): Mục tiêu: Bảo mật và kiểm soát dữ liệu.
- Kế thừa (Inheritance): Mục tiêu: Tái sử dụng code.
- Đa hình (Polymorphism): Ví dụ: Cả "Chó" và "Mèo" đều có hành động Speak(), nhưng Chó thì "Gâu gâu", còn Mèo thì "Meo meo".
- Trừu tượng (Abstraction): Mục tiêu: Giảm sự phức tạp, chỉ hiển thị những gì cần thiết.

## 3. LINQ

- LINQ (viết tắt của Language Integrated Query) là một công cụ trong ngôn ngữ C# giúp bạn tìm kiếm, sắp xếp và lọc dữ liệu từ nhiều nguồn khác nhau (như danh sách trong code, cơ sở dữ liệu, hay file XML) bằng một cách viết duy nhất.

```sh
var ketQua = from s in danhSachSo
             where s > 5
             select s;
```

| Từ khóa | Công dụng | Ví dụ đời thực |
| --- | --- | --- |
| Where | Lọc dữ liệu theo điều kiện | Lấy ra những học sinh có điểm > 8. |
| OrderBy | Sắp xếp dữ liệu | Sắp xếp danh sách tên theo bảng chữ cái. |
| Select | Chọn ra thông tin cụ thể | Chỉ lấy "Tên" của nhân viên, bỏ qua ngày sinh, địa chỉ. |
| First/FirstOrDefault | Lấy phần tử đầu tiên | Tìm người đầu tiên trong hàng đợi. |
| Count | Đếm số lượng | Đếm xem có bao nhiêu mặt hàng đã bán. |
| Sum/Max/Min | Tính toán số học | Tính tổng hóa đơn hoặc tìm món rẻ nhất. |

```sh
List<string> traiCay = new List<string> { "Tao", "Nho", "Le", "Chuoi" };

var ketQua = traiCay.Where(q => q.Length > 3)
                    .OrderBy(q => q);

// Kết quả sẽ là: "Chuoi", "Tao"
```

## 4. Xử lý bất đồng bộ (async/await)

### 4.1. Vì sao cần?

```sh
public void DownloadData()
{
    Console.WriteLine("Start downloading...");

    Thread.Sleep(5000); // giả lập tải dữ liệu 5s

    Console.WriteLine("Finished!");
}

# Start downloading...
# (đứng im 5 giây)
# Finished!
```

Vấn đề:

- Trong 5s đó thread block
- UI app sẽ đơ
- Server sẽ tốn thread vô ích

Ví dụ:

- Gọi API
- đọc file
- query database
- gọi web service  

=> Việc này chủ yếu là chờ I/O, không cần CPU

### 4.2. Ý tưởng của async

- Thay vì `làm việc -> chờ -> làm tiếp` thì ta làm `làm việc -> nhờ hệ thống xử lý -> khi xong thì báo lại`. Giống như: bạn đặt đồ ăn, không đứng đợi bếp, khi xong họ gọi bạn, trong thời gian đó bạn có thể làm việc khác.

### 4.3. async/await là gì?

- async: đánh dấu method có thể chạy bất đồng bộ
- await: nói với C# rằng chờ task này xong nhưng không block thread

### 4.4. ví dụ đơn giản nhất

- synchronous:

```sh
public void Work()
{
    Thread.Sleep(3000);
    Console.WriteLine("Done");
}
```

- asynchronous:

```sh
public async Task WorkAsync()
{
    await Task.Delay(3000);
    Console.WriteLine("Done");
}
# Task.Delay = delay không block thread
```

### 4.5. Cách gọi async method

```sh
public async Task Run()
{
    Console.WriteLine("Start");

    await WorkAsync();

    Console.WriteLine("End");
}
# Start
# (3s)
# Done
# End
```

### 4.6. Task là gì?

- Trong C# async dùng Task. Task giống như một công việc sẽ hoàn thành trong tương lai Task = Promise
- Các dạng: 

```sh
Task           -> không trả kết quả
Task<T>        -> trả kết quả
```

### 4.7. Ví dụ Task <T>

```sh
public async Task<int> GetNumberAsync()
{
    await Task.Delay(2000);
    return 10;
}

int x = await GetNumberAsync();

Console.WriteLine(x);
```

### 4.8. Ví dụ thực tế: gọi API

```sh
using System.Net.Http;

public async Task<string> GetGoogle()
{
    HttpClient client = new HttpClient();

    string result = await client.GetStringAsync("https://google.com");

    return result;
}
#  Trong lúc chờ server trả về thread không bị block
```

### 4.9. Ví dụ song song

```sh
# Giả sử có 3 API
await CallApi1();
await CallApi2();
await CallApi3();
# Nếu chạy tuần tự thời gian sẽ là 2s + 2s + 2s = 6s

var t1 = CallApi1();
var t2 = CallApi2();
var t3 = CallApi3();

await Task.WhenAll(t1, t2, t3);
# Nếu chạy song song thì thời gian là 2s

```

### 4.10. Quy tắc quan trọng

- Rule 1: method async phải trả Task `async Task async Task<T>` tránh `async void` trừ event
- Rule 2: method async phải await

### 4.11. Sai lầm phổ biến

- block async

```sh
var result = GetDataAsync().Result;
GetDataAsync().Wait();
# có thể gây deadlock, luôn dùng await
```

### 4.12. async không phải multithreading

- Nhiều người hiểu sai: async không có nghĩa là chạy thread khác, nó chỉ không block thread khi chờ I/O

### 4.13. So sánh trực quan

```sh
# sync
Thread
  |
  |---- call API ---- (chờ 2s) ---- tiếp tục

# async
Thread
  |
  |---- call API ----
          |
          | (I/O chạy)
          |
Thread rảnh làm việc khác
          |
API xong → tiếp tục
```

### 4.14. Tóm tắt dễ nhớ

- `async`  -> method có thể await
- `await`  -> chờ task xong nhưng không block thread
- `Task`   -> công việc trong tương lai

### 4.15. Thực tế trong .NET

- async dùng ở:

  - ASP.NET API
  - gọi database
  - đọc file
  - HTTP call
  - microservices
