---
layout: default
title: 23.1 C# core
parent: 23. MES
description: ""
permalink: /csharp/
---

# C# Core

## Cú pháp cơ bản

- Kiểu dữ liệu: int (số nguyên), double/float (số thực), string (chuỗi), bool (true/false).

```csharp
string tenMay = "May Cat Laser";
int soLuongDat = 150;
double nhietDoHienTai = 45.8;
bool dangHoatDong = true;
```

- câu lệnh điều kiện

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

- vòng lặp:

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

- Mảng (Array) và Danh sách (List)

```csharp
using System.Collections.Generic;

List<string> danhSachLoi = new List<string>();
danhSachLoi.Add("Loi ket noi PLC");
danhSachLoi.Add("Het nguyen lieu");

Console.WriteLine($"So luong loi hien tai: {danhSachLoi.Count}");
```


## OOP

## LINQ

## Xử lý bất đồng bộ (async/await)
