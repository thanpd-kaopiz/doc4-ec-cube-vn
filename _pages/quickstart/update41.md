---
layout: single
title: Nâng cấp từ 4.0 lên 4.1
keywords: howto update
tags: [quickstart, getting_started]
permalink: update41
summary : Hướng dẫn nâng cấp từ EC-CUBE 4.0 lên 4.1.
---

Trước khi thực hiện nâng cấp trên môi trường sản xuất, hãy đảm bảo kiểm tra trước trên môi trường thử nghiệm.
{: .notice--danger}
Hướng dẫn này giả định rằng bạn đang sử dụng gói EC-CUBE tải về từ ec-cube.net.
{: .notice--danger}
Hướng dẫn này giả định rằng bạn đang nâng cấp từ EC-CUBE 4.0.6-p1 lên 4.1.0.
{: .notice--danger}
Nếu bạn đã tùy chỉnh mã nguồn của EC-CUBE (các thư mục app/config/eccube, app/DoctrineMigrations, bin, src, html), các tệp sẽ bị ghi đè và bạn không thể nâng cấp theo hướng dẫn này. Hãy kiểm tra [sự khác biệt giữa các phiên bản](#sự khác biệt giữa các phiên bản) và tích hợp các thay đổi cần thiết.
{: .notice--danger}

## Chuẩn bị trước

### Kiểm tra phiên bản của plugin

- Nếu bạn đã cài đặt plugin, hãy kiểm tra xem chúng có tương thích với EC-CUBE 4.1 hay không.
- Trước khi thực hiện nâng cấp lên 4.1, hãy cập nhật các plugin đang sử dụng lên phiên bản tương thích với 4.1.

### Di chuyển khi sử dụng tùy chỉnh hoặc plugin riêng

- Nếu bạn đã sử dụng tùy chỉnh trong vùng Customize hoặc plugin riêng, hãy tham khảo [Di chuyển từ EC-CUBE 4.0 lên 4.1](/update-40-41) để thực hiện tương thích với 4.1.

### Vô hiệu hóa plugin đã được tích hợp vào mã nguồn

- Từ phiên bản 4.1.0, các plugin sau đã được tích hợp vào mã nguồn của EC-CUBE.
  - [taba secure 2段階認証プラグイン for EC-CUBE 4](https://www.ec-cube.net/products/detail.php?product_id=1750)
- Nếu bạn đang sử dụng các plugin này, hãy xóa chúng.

## Phương pháp nâng cấp sử dụng plugin cập nhật

- Đối với việc nâng cấp phiên bản 4.x của EC-CUBE, bạn có thể sử dụng plugin cập nhật.
- Plugin cập nhật có thể được tìm kiếm và sử dụng từ "Cửa hàng chủ sở hữu/ Tìm kiếm plugin" trong giao diện quản lý của EC-CUBE.

Nếu bạn đã thực hiện nâng cấp bằng plugin cập nhật, các bước dưới đây không cần thiết.
{: .notice--info}

## Quy trình công việc

1. Sao lưu trang web
1. Kích hoạt chế độ bảo trì
1. Thay thế các tệp nguồn của EC-CUBE bằng phiên bản đã nâng cấp
1. Thay thế tệp riêng lẻ
1. Cập nhật composer.json/composer.lock
1. Cập nhật schema/di chuyển
1. Tái tạo cache và các tệp khác
1. Cập nhật tệp mẫu giao diện
1. Vô hiệu hóa chế độ bảo trì

## Chi tiết các bước

### 1. Sao lưu trang web

Hãy sao lưu toàn bộ thư mục cài đặt của EC-CUBE.

Cũng hãy sao lưu toàn bộ cơ sở dữ liệu của bạn.

### 2. Kích hoạt chế độ bảo trì (phiên bản 4.0.1 trở lên)

Truy cập giao diện quản lý của EC-CUBE, từ "Quản lý nội dung" chọn "Quản lý bảo trì" và kích hoạt chế độ bảo trì.

Hoặc, bạn có thể kích hoạt chế độ bảo trì bằng cách tạo tệp ".maintenance" trong thư mục gốc của EC-CUBE.

```
[root]
  ├──.maintenance
  │
```

※ Khi sử dụng chế độ bảo trì, nếu truy cập vào các trang ngoài giao diện quản lý, màn hình bảo trì sẽ được hiển thị.

### 3. Thay thế các tệp nguồn của EC-CUBE bằng phiên bản đã nâng cấp

Về các tệp nguồn của EC-CUBE, hãy thay thế từng thư mục bằng các tệp nguồn đã nâng cấp. Các thư mục cần thay thế là những thư mục đã thay đổi trong lần nâng cấp này.
（`app/config/eccube` `app/DoctrineMigrations` `bin` `src` `html` `vendor` v.v...）

#### Thay thế ngoài thư mục `vendor`

Hãy xóa các thư mục cần thay thế và thay thế bằng các thư mục của phiên bản EC-CUBE đã nâng cấp.

（Không chỉ ghi đè lên các thư mục mục tiêu mà cần thay thế toàn bộ các tệp trong thư mục. Nếu các tệp cũ còn sót lại, có thể dẫn đến hoạt động không mong muốn, vì vậy hãy chắc chắn thay thế toàn bộ các tệp trong từng thư mục mục tiêu.）

```
[root]
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
  ├──[vendor]
  │
```

### 4. Thay thế tệp riêng lẻ

Hãy kiểm tra các tệp cần thay thế từ dưới đây và ghi đè bằng các tệp mới nhất.

- composer.json
- composer.lock
- .htaccess
- symfony.lock
- index.php

### 5. Cập nhật composer.json/composer.lock

Nếu bạn đã tự cài đặt các thư viện bên ngoài như packagist, hãy yêu cầu lại.

Ví dụ, nếu bạn đã cài đặt psr/http-message, hãy thực hiện lệnh dưới đây.

```
composer require psr/http-message --no-plugins --no-scripts
```

Nếu bạn sử dụng plugin với Symfony Bundle, hãy kiểm tra composer.json của plugin và cài đặt các thư viện phụ thuộc.

Ví dụ, đối với plugin API, hãy kiểm tra composer.json và cài đặt các thư viện phụ thuộc như dưới đây.

```
$ cat app/Plugin/Api/composer.json
...
  "require": {
    "ec-cube/plugin-installer": "~0.0.6 || ^2.0",
    "trikoder/oauth2-bundle": "^2.1",
    "nyholm/psr7": "^1.2",
    "webonyx/graphql-php": "^14.0"

$ composer require trikoder/oauth2-bundle:^2.1 --no-plugins --no-scripts
$ composer require nyholm/psr7:^1.2 --no-plugins --no-scripts
$ composer require webonyx/graphql-php:^14.0 --no-plugins --no-scripts
```

Hãy xóa bộ nhớ đệm bằng lệnh dưới đây.

```
bin/console cache:clear --no-warmup
```

Hãy thực hiện lệnh dưới đây.

```
bin/console eccube:composer:require-already-installed
```

### 6. Cập nhật schema/di chuyển

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

### 7. Tái tạo cache và các tệp khác

Tái tạo tệp autoload
```
composer dump-autoload
```

Tái tạo tệp proxy
```
bin/console eccube:generate:proxies
```

Tái tạo tệp bộ nhớ đệm
```
bin/console cache:warmup --env=prod
```

Xóa phiên làm việc
```
rm -rf var/sessions
```

### 8. Cập nhật tệp mẫu giao diện

Đối với từng phiên bản, cần cập nhật tệp mẫu giao diện (twig).

Từ "Quản lý nội dung" hoặc "Cài đặt cửa hàng > Cài đặt email" trong giao diện quản lý, hãy chỉnh sửa trang/khối/mẫu email tương ứng.

Danh sách các tệp thay đổi từ 4.0.6-p1 lên 4.1.0 như sau.
Bạn có thể kiểm tra sự khác biệt của các thay đổi từ [sự khác biệt](#sự khác biệt).

- src/Eccube/Resource/template/admin/default_frame.twig
- src/Eccube/Resource/template/default/Contact/confirm.twig
- src/Eccube/Resource/template/default/Contact/index.twig
- src/Eccube/Resource/template/default/Entry/confirm.twig
- src/Eccube/Resource/template/default/Entry/index.twig
- src/Eccube/Resource/template/default/Mail/contact_mail.twig
- src/Eccube/Resource/template/default/Mail/customer_withdraw_mail.twig
- src/Eccube/Resource/template/default/Mail/entry_complete.twig
- src/Eccube/Resource/template/default/Mail/entry_confirm.twig
- src/Eccube/Resource/template/default/Mail/forgot_mail.twig
- src/Eccube/Resource/template/default/Mail/order.html.twig
- src/Eccube/Resource/template/default/Mail/order.twig
- src/Eccube/Resource/template/default/Mail/reset_complete_mail.twig
- src/Eccube/Resource/template/default/Mail/shipping_notify.twig
- src/Eccube/Resource/template/default/Mypage/change.twig
- src/Eccube/Resource/template/default/Mypage/delivery_edit.twig
- src/Eccube/Resource/template/default/Mypage/index.twig
- src/Eccube/Resource/template/default/Product/detail.twig
- src/Eccube/Resource/template/default/Product/list.twig
- src/Eccube/Resource/template/default/Shopping/shipping_edit.twig
- src/Eccube/Resource/template/default/Shopping/shipping_multiple_edit.twig
- src/Eccube/Resource/template/default/default_frame.twig
- src/Eccube/Resource/template/default/meta.twig
- src/Eccube/Resource/template/default/sitemap.xml.twig
- src/Eccube/Resource/template/default/sitemap_index.xml.twig

### 9. Vô hiệu hóa chế độ bảo trì

Truy cập giao diện quản lý của EC-CUBE, từ "Quản lý nội dung" chọn "Quản lý bảo trì" và vô hiệu hóa chế độ bảo trì.

Hoặc, bạn có thể vô hiệu hóa chế độ bảo trì bằng cách xóa tệp ".maintenance" trong thư mục gốc của EC-CUBE.

## Sự khác biệt

Bạn có thể kiểm tra sự khác biệt chi tiết từ 4.0.6-p1 lên 4.1.0 từ liên kết dưới đây.

[https://github.com/EC-CUBE/ec-cube/compare/4.0.6-p1...4.1.0](https://github.com/EC-CUBE/ec-cube/compare/4.0.6-p1...4.1.0?w=1#files_bucket){:target="_blank"}
