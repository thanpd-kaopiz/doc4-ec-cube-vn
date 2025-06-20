---
layout: single
title: Nâng cấp phiên bản 4.1
keywords: howto update
tags: [quickstart, getting_started]
permalink: update41x
summary : Hướng dẫn nâng cấp phiên bản 4.1.x.
---

Trước khi thực hiện nâng cấp trên môi trường sản xuất, hãy đảm bảo kiểm tra trước trên môi trường thử nghiệm.
{: .notice--danger}
Hướng dẫn này giả định rằng bạn đang sử dụng gói EC-CUBE tải về từ ec-cube.net.
{: .notice--danger}
Nếu bạn đã tùy chỉnh mã nguồn của EC-CUBE (các thư mục app/config/eccube, app/DoctrineMigrations, bin, src, html), các tệp sẽ bị ghi đè và bạn không thể nâng cấp theo hướng dẫn này. Hãy kiểm tra [sự khác biệt giữa các phiên bản](#sự khác biệt giữa các phiên bản) và tích hợp các thay đổi cần thiết.
{: .notice--danger}
Lỗ hổng bảo mật "Xử lý tiêu đề HTTP Host" được công bố vào ngày 21 tháng 2 năm 2022 sẽ không được sửa chữa ngay cả khi bạn nâng cấp EC-CUBE. Hãy tham khảo [trang chi tiết lỗ hổng bảo mật](https://www.ec-cube.net/info/weakness/20220221/) để thực hiện các cài đặt phù hợp.
{: .notice--danger}


## Quy trình công việc
1. Sao lưu trang web
1. Kích hoạt chế độ bảo trì
1. Cập nhật plugin
1. Thay thế các tệp nguồn của EC-CUBE bằng phiên bản đã nâng cấp
1. Thay thế tệp riêng lẻ
1. Cập nhật composer.json/composer.lock
1. Cập nhật schema/di chuyển
1. Cập nhật tệp mẫu giao diện
1. Vô hiệu hóa chế độ bảo trì

## Chi tiết các bước

### 1. Sao lưu trang web

Hãy sao lưu toàn bộ thư mục cài đặt của EC-CUBE.

Cũng hãy sao lưu toàn bộ cơ sở dữ liệu của bạn.

### 2. Kích hoạt chế độ bảo trì

Truy cập giao diện quản lý của EC-CUBE, từ "Quản lý nội dung" chọn "Quản lý bảo trì" và kích hoạt chế độ bảo trì.

Hoặc, bạn có thể kích hoạt chế độ bảo trì bằng cách tạo tệp ".maintenance" trong thư mục gốc của EC-CUBE.

```
[root]
  │
  ├──.maintenance
  │
```

※ Khi sử dụng chế độ bảo trì, nếu truy cập vào các trang ngoài giao diện quản lý, màn hình bảo trì sẽ được hiển thị.

### 3. Cập nhật plugin

Nếu có plugin đã cài đặt có thể cập nhật, hãy thực hiện cập nhật trước.

### 4. Thay thế các tệp nguồn của EC-CUBE bằng phiên bản đã nâng cấp

Về các tệp nguồn của EC-CUBE, hãy thay thế từng thư mục bằng các tệp nguồn đã nâng cấp. Các thư mục cần thay thế là những thư mục đã thay đổi trong lần nâng cấp này.
（`app/config/eccube` `app/DoctrineMigrations` `bin` `src` `html` `vendor` v.v...）

#### Thay thế ngoài thư mục `vendor`

Hãy xóa các thư mục cần thay thế và thay thế bằng các thư mục của phiên bản EC-CUBE đã nâng cấp.

（Không chỉ ghi đè lên các thư mục mục tiêu mà cần thay thế toàn bộ các tệp trong thư mục. Nếu các tệp cũ còn sót lại, có thể dẫn đến hoạt động không mong muốn, vì vậy hãy chắc chắn thay thế toàn bộ các tệp trong từng thư mục mục tiêu.）

```
[root]
  │
  ├──[app/config/eccube]
  ├──[app/DoctrineMigrations]
  ├──[bin]
  ├──[src]
  ├──[html]
  │
```

#### Thay thế thư mục `vendor`

Thư mục `vendor` không cần xóa, hãy ghi đè lên bằng thư mục `vendor` của phiên bản EC-CUBE đã nâng cấp.

（Nếu bạn sử dụng các plugin Web API hoặc Symfony bundle, việc xóa hoàn toàn thư mục `vendor` có thể gây ra lỗi trong các bước tiếp theo. Lệnh `bin/console eccube:composer:require-already-installed` trong bước (5) sẽ xóa các tệp không cần thiết trong thư mục `vendor`）

```
[root]
  │
  ├──[vendor]
  │
```

### 5. Thay thế tệp riêng lẻ

Đối với từng phiên bản, cần thay thế các tệp riêng lẻ.

Hãy kiểm tra các tệp cần thay thế từ dưới đây và ghi đè bằng các tệp mới nhất.

| Phiên bản nâng cấp | Tệp cần thay thế                                                                              |
|----------------------|---------------------------------------------------------------------------------------------------|
| 4.1.0 → 4.1.1        | composer.json<br>composer.lock<br>.htaccess<br>index.php<br>symfony.lock<br>package.json<br>package-lock.json|
| 4.1.1 → 4.1.2        | composer.json<br>composer.lock<br>.htaccess<br>index.php<br>symfony.lock<br>package.json<br>package-lock.json|
| 4.1.2 → 4.1.2-p1        | -|

※ Khi tải lên tệp qua FTP, có thể quyền truy cập sẽ bị thay đổi. Hãy tham khảo [cài đặt quyền truy cập](/quickstart/permission) để kiểm tra quyền truy cập.

Sau khi ghi đè, hãy xóa bộ nhớ đệm bằng lệnh dưới đây.

```
bin/console cache:clear --no-warmup
```

### 6. Cập nhật composer.json/composer.lock

Hãy thực hiện lệnh dưới đây.

```
bin/console eccube:composer:require-already-installed
```

Nếu bạn đã tự cài đặt các thư viện bên ngoài như packagist, hãy yêu cầu lại.

Ví dụ, nếu bạn đã cài đặt psr/http-message, hãy thực hiện lệnh dưới đây.

```
composer require psr/http-message
```

### 7. Cập nhật schema/di chuyển

Sử dụng chức năng cập nhật schema và di chuyển để nâng cấp cơ sở dữ liệu.

Hãy thực hiện lệnh dưới đây.

Cập nhật schema

```
bin/console doctrine:schema:update --force --dump-sql
```

Di chuyển

```
bin/console doctrine:migrations:migrate
```

### 8. Cập nhật tệp mẫu giao diện

Đối với từng phiên bản, cần cập nhật tệp mẫu giao diện (twig).

Từ "Quản lý nội dung" hoặc "Cài đặt cửa hàng > Cài đặt email" trong giao diện quản lý, hãy chỉnh sửa trang/khối/mẫu email tương ứng.

Bạn có thể kiểm tra sự khác biệt của các thay đổi từ [sự khác biệt giữa các phiên bản](#sự khác biệt giữa các phiên bản).

#### 4.1.0 → 4.1.1

<a href="https://github.com/EC-CUBE/ec-cube/pulls?q=is%3Apr+label%3Aaffected%3Atemplate+is%3Aclosed+milestone%3A4.1.1" target = "_blank">Sự khác biệt của tệp mẫu giao diện</a>

#### 4.1.1 → 4.1.2

<a href="https://github.com/EC-CUBE/ec-cube/pulls?q=is%3Apr+label%3Aaffected%3Atemplate+is%3Aclosed+milestone%3A4.1.2" target = "_blank">Sự khác biệt của tệp mẫu giao diện</a>

### 9. Vô hiệu hóa chế độ bảo trì

Truy cập giao diện quản lý của EC-CUBE, từ "Quản lý nội dung" chọn "Quản lý bảo trì" và vô hiệu hóa chế độ bảo trì.

Hoặc, bạn có thể vô hiệu hóa chế độ bảo trì bằng cách xóa tệp ".maintenance" trong thư mục gốc của EC-CUBE.

---

Quy trình nâng cấp phiên bản của EC-CUBE đã hoàn tất.

## Sự khác biệt giữa các phiên bản

Bạn có thể kiểm tra sự khác biệt chi tiết giữa các phiên bản từ các liên kết dưới đây.

| Phiên bản      | Trang sự khác biệt                                                                                                             |
|-----------------|------------------------------------------------------------------------------------------------------------------------|
| 4.1.0 → 4.1.1   | [https://github.com/EC-CUBE/ec-cube/compare/4.1.0...4.1.1](https://github.com/EC-CUBE/ec-cube/compare/4.1.0...4.1.1?w=1#files_bucket){:target="_blank"}   |
| 4.1.1 → 4.1.2   | [https://github.com/EC-CUBE/ec-cube/compare/4.1.1...4.1.2](https://github.com/EC-CUBE/ec-cube/compare/4.1.1...4.1.2?w=1#files_bucket){:target="_blank"}   |
| 4.1.2 → 4.1.2-p1   | [https://github.com/EC-CUBE/ec-cube/compare/4.1.2...4.1.2-p1](https://github.com/EC-CUBE/ec-cube/compare/4.1.2...4.1.2-p1?w=1#files_bucket){:target="_blank"}   |

