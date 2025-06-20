---
title: Cách tạo Pull Request
description: Hướng dẫn gửi Pull Request cho EC-CUBE và các lưu ý cần thiết.
keywords: Githubflow
tags: [contribution-guide, guideline]
permalink: contribution-guide/pull-request
folder: contribution-guide
---

Hướng dẫn gửi Pull Request cho EC-CUBE và các lưu ý cần thiết.

## Clone mã nguồn về local

Fork repository <a href="https://github.com/EC-CUBE/ec-cube" target="_blank">ec-cube</a> về tài khoản Github của bạn, sau đó <a href="https://help.github.com/ja/github/creating-cloning-and-archiving-repositories/cloning-a-repository" target="_blank">clone</a> về local.

## Cài đặt package phụ thuộc

Cài đặt các package phụ thuộc:

```sh
$ composer install
```

## Thêm remote

Thêm repository gốc của ec-cube làm remote. Ở đây đặt tên là `upstream`, bạn có thể đặt tên khác nếu muốn.

```sh
$ git remote add upstream https://github.com/EC-CUBE/ec-cube.git
```

## Cập nhật branch main local

EC-CUBE sử dụng branch 4.2 làm branch chính.

```sh
$ git pull upstream 4.2
```

## Tạo branch phát triển

```sh
$ git checkout -b [tên branch tuỳ ý] upstream/4.2
```

## Đẩy lên repository của bạn

Sau khi commit thay đổi trên branch vừa tạo, hãy push lên repository của bạn.

```sh
$ git push origin [tên branch tuỳ ý]
```

## Gửi Pull Request

Từ trang repository của bạn trên Github, tạo Pull Request tới <a href="https://github.com/EC-CUBE/ec-cube" target="_blank">ec-cube</a>.

- Tạo Pull Request từ repository của bạn lên repository chính

### Điều kiện merge Pull Request

Pull Request sẽ được merge vào "Master" khi đáp ứng các điều kiện sau:

1. Được developer/committer review
2. Check CI thành công
    - Travis: Unit test
    - AppVeyor: Unit test (môi trường Windows)
    - Scrutinizer: Phân tích mã nguồn tĩnh

### Lưu ý khi gửi Pull Request

Hãy gộp các commit không cần thiết lại với nhau. Nếu bạn đã quen với `git rebase`, hãy sử dụng để gộp commit.

Ví dụ, nếu bạn có các commit như sau, hãy gộp `112233445` đến `334455667` lại:
```sh
$ git log --pretty=format:"%h - %an : %s"
334455667 - myself : Sửa chức năng A
223344556 - myself : Sửa chức năng A
112233445 - myself : Thêm chức năng A
001122334 - other_user : Commit của người khác
```
Chạy `git rebase` để gộp commit:
```sh
$ git rebase -i 001122334
pick 112233445 Thêm chức năng A
squash 223344556 Sửa chức năng A
squash 334455667 Sửa chức năng A
```
Sau khi gộp, log sẽ như sau:
```sh
$ git log --pretty=format:"%h - %an : %s"
445566778 - myself : Thêm chức năng A
001122334 - other_user : Commit của người khác
$ git push origin master
$ ...
```

Tuy nhiên, nếu bạn sửa theo comment review, hãy giữ lại lịch sử để dễ theo dõi, không nên gộp quá nhiều:
```sh
$ git log --pretty=format:"%h - %an : %s"
667788990 - myself : Sửa lại do sai sót
556677889 - myself : Phản hồi kết quả review
445566778 - myself : Thêm chức năng A
001122334 - other_user : Commit của người khác
```
Sau khi commit `445566778` và gửi Pull Request, nếu có sửa theo review thì chỉ gộp các commit sửa review lại với nhau, không gộp với commit chính.

Không gộp các commit đã được merge.
