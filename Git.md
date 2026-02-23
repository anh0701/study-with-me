---
layout: default
title: 6. Git
nav_order: 2
description: ""
---

### GIT

Git là một hệ thống quản lý phiên bản phân tán (Distributed Version Control System - DVCS) mã nguồn mở và miễn phí. Nó được thiết kế để xử lý mọi thứ từ các dự án nhỏ đến rất lớn một cách nhanh chóng và hiệu quả.

#### Cách hoạt động

Git lưu trữ dữ liệu dưới dạng các ảnh chụp nhanh (snapshots) của toàn bộ dự án tại các thời điểm khác nhau.
Khi bạn thực hiện các thay đổi commit, Git sẽ chụp lại trạng thái hiện tại của dự án và lưu trữ nó. Nếu không có thay đổi, Git chỉ lưu trữ tham chiếu đến ảnh chụp trước đó.

#### Vì sao chúng ta cần dùng Git

- Quản lý phiên bản hiệu quả: giúp bạn theo dõi mọi thay đổi trong mã nguồn, cho phép bạn quay lại các phiên bản trước đó nếu cần.
- Hỗ trợ làm việc nhóm: cho phép nhiều người cùng làm việc trên một dự án mà không lo xung đột mã nguồn.
- Tính toàn vẹn dữ liệu: đảm bảo rằng mọi thay đổi đều được ghi lại và không thể thay đổi mà không bị phát hiện.
- Linh hoạt và phân tán: mỗi lập trình viên có một bản sao đầy đủ của kho lưu trữ, giúp làm việc offline và đồng bộ hóa dễ dàng khi có kết nối mạng.

#### Git, GitHub, GitLab

**GitHub**: là một dịch vụ lưu trữ kho Git dựa trên web. Nó cung cấp các tính năng như quản lý dự án, wiki, và tích hợp CI để hỗ trợ phần mềm.
GitHub nổi tiếng với cộng đồng lớn và là nơi lưu trữ nhiều dự án mã nguồn mở.

**Gitlab**: là một dịch vụ lưu trữ khi Git dựa trên web, nhưng nó có thêm nhiều tính năng quản lý dự án và DevOps. 
GitLab cung cấp các công cụ như theo dõi vấn đề, quản lý nhóm, và lộ trình phát triển. 

> **Git**: công cụ quản lý phiên bản phân tán. <br>
> **GitHub**: là dịch vụ lưu trữ kho Git và các tính năng cộng đồng, và quản lý dự án. <br>
> **Gitlab**: là dịch vụ lưu trữ kho Git và các tính năng quản lý dự án và DevOps.

#### Quy trình làm việc với Git

1. Sử dụng nhánh (branch):
- Main branch: Nhánh chính, thường là nhánh ổn định nhất và chứa mã nguồn đã được kiểm tra kỹ lưỡng.
- Feature branches: Nhánh phát triển tính năng mới. Mỗi tính năng mới nên được phát triển trên một nhánh riêng biệt để tránh xung đột mã nguồn.
- Release branches: Nhánh chuẩn bị cho việc phát hành phiên bản mới. Nhánh này giúp kiểm tra và sửa lỗi trước khi hợp nhất vào nhánh chính.
- Hotfix branches: Nhánh sửa lỗi khẩn cấp. Khi phát hiện lỗi trong phiên bản đã phát hành, bạn có thể tạo nhánh hotfix để sửa lỗi mà không ảnh hưởng đến các nhánh khác1.

2. Code Review:
- Thực hiện kiểm tra mã nguồn (code review) trước khi hợp nhất (merge) các nhánh. Điều này giúp phát hiện lỗi sớm và đảm bảo chất lượng mã nguồn.

3. Continuous Integration (CI):
- Sử dụng các công cụ CI để tự động kiểm tra và xây dựng mã nguồn mỗi khi có thay đổi. Điều này giúp phát hiện lỗi sớm và đảm bảo mã nguồn luôn ở trạng thái ổn định.


#### Các lệnh cơ bản

![img.png](images/img_git_workflow.png)

1. Cấu hình Git

```shell 
    git config --global user.name "Tên của bạn": Đặt tên người dùng.
    git config --global user.email "email@example.com": Đặt email người dùng.
```
2. Khởi tạo và quản lý kho lưu trữ
```shell
   git init: Khởi tạo một kho lưu trữ Git mới.
   git clone <URL>: Sao chép một kho lưu trữ từ xa về máy tính của bạn.
```
3. Làm việc với các tệp
```shell
   git add <tên_tệp>: Thêm tệp vào khu vực staging.
   git commit -m "Thông điệp commit": Lưu các thay đổi trong khu vực staging vào kho lưu trữ với một thông điệp mô tả.
```
4. Kiểm tra trạng thái và lịch sử
```shell
   git status: Kiểm tra trạng thái hiện tại của kho lưu trữ.
   git log: Xem lịch sử commit.
```
5. Làm việc với nhánh
```shell
   git branch: Liệt kê các nhánh hiện có.
   git checkout <tên_nhánh>: Chuyển đổi sang một nhánh khác.
   git merge <tên_nhánh>: Hợp nhất nhánh được chỉ định vào nhánh hiện tại.
```
6. Làm việc với kho lưu trữ từ xa
```shell
   git remote add origin <URL>: Thêm một kho lưu trữ từ xa.
   git push origin <tên_nhánh>: Đẩy các thay đổi lên kho lưu trữ từ xa.
   git pull origin <tên_nhánh>: Kéo các thay đổi từ kho lưu trữ từ xa về máy tính của bạn.
```
7. Khác
```shell
   git stash: Lưu tạm thời các thay đổi chưa commit.
   git stash pop: Khôi phục các thay đổi đã lưu tạm thời.
```

#### Git convenient

Git convention, hay còn gọi là Conventional Commits, là một quy ước nhẹ nhàng trên các thông điệp commit trong Git. Quy ước này giúp tạo ra một lịch sử commit rõ ràng và dễ hiểu, đồng thời hỗ trợ việc viết các công cụ tự động hóa dựa trên lịch sử commit đó.
Cấu trúc của một commit theo Conventional Commits:

    <type>[optional scope]: <description>
    [optional body]
    [optional footer(s)]

Các loại commit phổ biến:

    fix: Sửa lỗi trong mã nguồn.
    feat: Thêm tính năng mới.
    BREAKING CHANGE: Thay đổi lớn ảnh hưởng đến API.

Ví dụ:

    feat(parser): add ability to parse arrays
    fix: prevent racing of requests
    docs: correct spelling of CHANGELOG


#### Một số TH khi làm việc với git

> Project được contribute bởi nhiều thành viên, mỗi thành viên sẽ làm việc trên một branch riêng và merge vào develop. 
> Điều gì xảy ra khi bạn clone project xuống và checkout tạo nhánh mới giống hệt nhánh của bạn trên origin?

- Tạo nhánh mới: Khi bạn checkout -b để tạo nhánh mới từ develop, Git sẽ tạo một nhánh mới local với tên bạn chỉ định. Nhánh này sẽ có cùng lịch sử commit với nhánh develop tại thời điểm bạn tạo nó.
- Push lên origin: Khi bạn push nhánh mới này lên origin, Git sẽ kiểm tra xem nhánh đó đã tồn tại trên origin hay chưa. Nếu nhánh đó đã tồn tại (vì bạn nói tên nhánh giống với nhánh của bạn trên origin), Git sẽ cố gắng cập nhật nhánh đó với các commit mới từ nhánh local của bạn.
- Fast-forward hoặc Non-fast-forward: Nếu nhánh trên origin không có commit mới nào kể từ khi bạn clone, việc push sẽ diễn ra suôn sẻ (fast-forward). Tuy nhiên, nếu nhánh trên origin đã có commit mới mà bạn chưa pull về, bạn sẽ gặp lỗi non-fast-forward và cần phải pull các thay đổi mới nhất từ origin trước khi push.
- Conflict (Xung đột): Nếu có bất kỳ xung đột nào giữa các commit của bạn và commit trên origin, bạn sẽ cần phải giải quyết xung đột trước khi push thành công.
- Merge vào develop: Sau khi bạn đã push thành công nhánh của mình lên origin, bạn có thể tạo một merge request để merge nhánh của bạn vào develop. Quá trình này sẽ được xem xét và phê duyệt bởi các thành viên khác trong team (nếu có quy trình review).

>  Vì một số lý do nào đó, bạn muốn di chuyển project của mình từ github sang gitlab và muốn giữ nguyên lịch sử commit.
> Vậy thì phải làm sao?

- Clone repository từ GitHub:

```shell
    git clone https://github.com/username/repository.git
    cd repository
```

- Thêm remote mới cho GitLab:

```shell
    git remote add gitlab https://gitlab.com/username/repository.git
```

- Push toàn bộ các nhánh lên GitLab:

```shell
    git push gitlab --all
```

- Push các tags lên GitLab:

```shell
    git push gitlab --tags
```

- Kiểm tra remote để đảm bảo đã thêm đúng:

```shell
    git remote -v
```

> Khi nào cần config git global?

Việc cấu hình tài khoản Git ở chế độ global trên Windows hay Linux là không bắt buộc; nó tùy thuộc vào cách bạn muốn quản lý cấu hình Git của mình.
1. Git global configuration: Là cấu hình được áp dụng cho tất cả các dự án Git trên máy tính của bạn. Điều này thuận tiện nếu bạn sử dụng cùng một tài khoản cho nhiều dự án.
```shell
    git config --global user.name "Your Name"
    git config --global user.email "your.email@example.com"
```
2. Local configuration: Áp dụng riêng cho từng dự án. Hữu ích khi bạn muốn sử dụng thông tin khác nhau cho các dự án khác nhau.
```shell
    git config user.name "Your Name"
    git config user.email "your.email@example.com"

```

>  Trong trường hợp bạn đang làm việc trên một nhánh riêng biệt và nhánh develop đã có nhiều thay đổi từ các thành viên khác, khả năng xung đột (conflict) rất cao khi bạn cố gắng merge. 
> Cách giải quyết vấn đề trên là gì?

Ví dụ nhánh của bạn là `feature-branch`

```shell
    # Đảm bảo nhánh develop được cập nhật mới nhất
    git checkout develop
    git pull origin develop
    
    # Chuyển về nhánh của bạn
    git checkout feature-branch
    
    # Merge develop vào nhánh của bạn
    git merge develop
    
    # Giải quyết xung đột (nếu có), sau đó commit
    git add .
    git commit -m "Resolved merge conflicts"
    
    # Đẩy thay đổi lên remote
    git push origin feature-branch
    
    # Tạo PR từ feature-branch vào develop

```

>

