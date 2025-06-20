---
title: Giao diện dòng lệnh (CLI)
keywords: CLI
tags: [quickstart, cli]
permalink: quickstart/cli
folder: quickstart
---

EC-CUBE cung cấp nhiều lệnh tiện ích có thể thực thi qua dòng lệnh.
Bạn có thể thực hiện như sau:

```bash
$ cd [thư mục gốc ec-cube]
$ php bin/console eccube:install
```

Tên lệnh có thể được rút gọn. Ví dụ, với lệnh `eccube:install`, bạn có thể dùng `e:i`.

```bash
$ php bin/console e:i
```

## Danh sách lệnh do EC-CUBE cung cấp

Bảng dưới đây liệt kê các lệnh và mô tả ngắn gọn:

| Tên lệnh                                | Mô tả                                                                                      |
|-----------------------------------------|-------------------------------------------------------------------------------------------|
| eccube:install                          | Cài đặt EC-CUBE.                                                                          |
| eccube:plugin:install                   | Cài đặt plugin EC-CUBE.                                                                   |
| eccube:plugin:enable                    | Kích hoạt plugin EC-CUBE.                                                                 |
| eccube:plugin:disable                   | Vô hiệu hóa plugin EC-CUBE.                                                               |
| eccube:plugin:uninstall                 | Gỡ plugin EC-CUBE.                                                                        |
| eccube:composer:install                 | Cài plugin EC-CUBE qua Owners Store dựa trên composer.lock.                               |
| eccube:composer:require                 | Cài plugin EC-CUBE qua Owners Store.                                                      |
| eccube:composer:update                  | Cập nhật plugin EC-CUBE qua Owners Store.                                                 |
| eccube:composer:remove                  | Gỡ plugin EC-CUBE qua Owners Store.                                                       |
| eccube:composer:require-already-installed | Cập nhật composer.json và composer.lock theo trạng thái cài đặt plugin.                  |
| eccube:plugin:generate                  | Tạo khung plugin EC-CUBE.                                                                 |
| eccube:generate:proxies                 | Tạo file proxy khi sử dụng mở rộng Entity.                                                |
| eccube:fixtures:load                    | Nạp dữ liệu khởi tạo.                                                                     |
| eccube:fixtures:generate                | Nạp dữ liệu mẫu cho sản phẩm, hội viên.                                                   |
| eccube:delete-carts                     | Xóa các bản ghi `dtb_cart` trước ngày chỉ định.                                           |

## Các lệnh do Symfony và Doctrine cung cấp

Bảng dưới đây liệt kê các lệnh chính:

| Tên lệnh               | Mô tả                                                          |
|------------------------|---------------------------------------------------------------|
| cache:clear            | Xóa cache. Nên dùng thêm `--no-warmup`.                       |
| cache:warmup           | Sinh cache.                                                    |
| server:run             | Khởi động web server cho phát triển.                           |
| debug:router           | Xem danh sách routing.                                         |
| doctrine:database:create | Tạo database.                                                |
| doctrine:database:drop   | Xóa database.                                                |
| doctrine:schema:create   | Tạo bảng dựa trên mapping Entity.                            |
| doctrine:schema:drop     | Xóa bảng dựa trên mapping Entity.                            |
| doctrine:schema:update   | Cập nhật bảng dựa trên mapping Entity.                       |

## Tham khảo

Ngoài các lệnh trên, còn rất nhiều lệnh khác.

Bạn có thể xem danh sách lệnh bằng:

```bash
$ php bin/console list
```

Hoặc xem hướng dẫn sử dụng từng lệnh:

```bash
$ php bin/console [tên lệnh] --help
```
