---
layout: default
title: 22.1.1 C# core
parent: 22. MES
description: ""
permalink: /csharp-tips/
has_toc: side_bar 
---

# Async nâng cao

## ValueTask - tối ưu performance

- Thông thường async trả về `Task`, `Task<T>`
- Vấn đề là `Task` là `object`, mỗi lần gọi async sẽ tạo object mới nên GC phải dọn, nếu API được gọi hàng triệu lần thì GC sẽ tốn tài nguyên
- Giải pháp là `ValueTask`, ValueTask là struct, không cần allocation trong nhiều trường hợp
- Khi nào dùng ValueTask: Khi method thường trả kết quả ngay lập tức

```sh
    public ValueTask<User> GetUser()
    {
        if (cacheHit)
            return new ValueTask<User>(cachedUser);

        return new ValueTask<User>(LoadFromDb());
    }
```

- Khi nào không nên dùng: Nếu method luôn async

```sh
    await httpClient.GetAsync()
```

## IAsyncEnumerable - stream async

- Trước đây: `List<User> users = await GetUsers();`, nhược điểm phải load toàn bộ data trước

- Async stream:

```sh
    public async IAsyncEnumerable<int> GenerateNumbers()
    {
        for (int i = 0; i < 5; i++)
        {
            await Task.Delay(1000);
            yield return i;
        }
    }

    await foreach (var n in GenerateNumbers())
    {
        Console.WriteLine(n);
    }

    # 0
    # 1
    # 2
    # 3
    # 4
    # Mỗi lần xuất hiện sau 1 giây
```

- Dùng rất nhiều trong: đọc database lớn, đọc file lớn, streaming API

## Parallel.ForEachAsync

- .NET có API rất mạnh: `Parallel.ForEachAsync`
- Ví dụ:

```sh
await Parallel.ForEachAsync(urls, async (url, ct) =>
{
    var html = await httpClient.GetStringAsync(url);
    Console.WriteLine(html.Length);
});

# Tự động chạy song song
# Giới hạn concurrency
```

- Ví dụ thực tế

```sh
# Download 100 URL
await Parallel.ForEachAsync(urls, async (url, ct) =>
{
    await Download(url);
});
# Nhanh hơn nhiều so với:
foreach (var url in urls)
{
    await Download(url);
}
```

## Tóm tắt async nâng cao

| Kỹ thuật                | Dùng khi          |
| ----------------------- | ----------------- |
| `ValueTask`             | tối ưu allocation |
| `IAsyncEnumerable`      | stream dữ liệu    |
| `Parallel.ForEachAsync` | xử lý song song   |

## Một số lỗi async

### 1. Fire-and-forget async

- Ví dụ:

```sh
    public async void SendEmail()
    {
        await smtp.SendAsync(...);
    }
```

- hoặc:

```sh
    # không await
    SendEmailAsync(); 
```

- Vấn đề:

    - exception sẽ bị mất
    - task có thể chết giữa chừng
    - không ai biết

- Ví dụ:

```sh
    public async Task SendEmailAsync()
    {
        throw new Exception("fail");
    }

    SendEmailAsync();
    # Exception không được catch
```

- Cách đúng:

```sh
    await SendEmailAsync();
    # hoặc lưu task:
    var task = SendEmailAsync();
```

### 2. Tạo quá nhiều Task

```sh
    var tasks = new List<Task>();

    foreach (var item in items)
    {
        tasks.Add(Process(item));
    }

    await Task.WhenAll(tasks);

    # Nếu items = 1,000,000 thì sẽ tạo 1 triệu task, dẫn đến:
    # Ram tăng, scheduler quá tải, performance giảm mạnh
```

- Cách đúng, giới hạn concurrency: `SemaphoreSlim / Parallel.ForEachAsync`
- Ví dụ:

```sh
await Parallel.ForEachAsync(items, async (item, ct) =>
{
    await Process(item);
});
```

### 3. Async method nhưng không async thật

```sh
public async Task<User> GetUser()
{
    return db.Users.First();
}
```

- Vấn đề: method async nhưng code bên trong sync, thread vẫn bị block
- Đúng:

```sh
public async Task<User> GetUser()
{
    return await db.Users.FirstAsync();
}
```

### 4. Await trong loop (làm code chậm 10x)

```sh
foreach (var id in ids)
{
    await GetUser(id);
}
# 100 request, mỗi request 200ms, tổng 20s
```

```sh
var tasks = ids.Select(id => GetUser(id));

await Task.WhenAll(tasks);
# thời gian khoảng 200ms
```

### 5. Blocking async code

```sh
Task.Delay(1000).Wait();
Thread.Sleep(1000);
# trong async code điều này block thread, phá lợi ích async
```

```sh
public async Task Test()
{
    Thread.Sleep(2000);
}
# method async nhưng vẫn block
```

- Đúng `await Task.Delay(2000);`

### Tóm tắt 5 lỗi nguy hiểm

| Lỗi              | Hậu quả                     |
| ---------------- | --------------------------- |
| fire-and-forget  | mất exception               |
| quá nhiều task   | memory + scheduler overload |
| async giả        | thread bị block             |
| await trong loop | code chậm                   |
| blocking async   | mất lợi ích async           |

## Phân biệt Task vs Thread vs async
