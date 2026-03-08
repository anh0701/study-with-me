---
layout: default
title: 23.1.1 C# core
parent: 23. MES
description: ""
permalink: /csharp-tips/
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
