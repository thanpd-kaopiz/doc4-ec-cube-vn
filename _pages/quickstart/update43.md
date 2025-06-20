---
layout: single
title: Nâng cấp từ 4.2 lên 4.3
keywords: howto update
tags: [quickstart, getting_started]
permalink: update43
summary : Hướng dẫn nâng cấp từ EC-CUBE 4.2 lên 4.3.
---

Trước khi thực hiện nâng cấp trên môi trường sản xuất, hãy đảm bảo kiểm tra trước trên môi trường thử nghiệm.
{: .notice--danger}
Hướng dẫn này giả định rằng bạn đang sử dụng gói EC-CUBE tải về từ ec-cube.net.
{: .notice--danger}
Hướng dẫn này giả định rằng bạn đang nâng cấp từ EC-CUBE 4.2.3 lên 4.3.0.
{: .notice--danger}
Nếu bạn đã tùy chỉnh mã nguồn của EC-CUBE (các thư mục app/config/eccube, app/DoctrineMigrations, bin, src, html), các tệp sẽ bị ghi đè và bạn không thể nâng cấp theo hướng dẫn này. Hãy kiểm tra [sự khác biệt giữa các phiên bản](#sự khác biệt) và tích hợp các thay đổi cần thiết.
{: .notice--danger}

## Chuẩn bị trước

### Kiểm tra phiên bản của plugin

- Nếu bạn đã cài đặt plugin, hãy kiểm tra xem chúng có tương thích với EC-CUBE 4.3 hay không.
- Trước khi thực hiện nâng cấp lên 4.3, hãy cập nhật các plugin đang sử dụng lên phiên bản tương thích với 4.3.

### Di chuyển khi sử dụng tùy chỉnh hoặc plugin riêng

- Nếu bạn đã sử dụng tùy chỉnh trong vùng Customize hoặc plugin riêng, hãy tham khảo [Di chuyển từ EC-CUBE 4.2 lên 4.3](/update-42-43) để thực hiện tương thích với 4.3.

## Quy trình công việc

1. Sao lưu trang web
1. Kích hoạt chế độ bảo trì
1. Cập nhật plugin
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

Hãy kiểm tra các tệp cần thay thế từ dưới đây và ghi đè bằng các tệp mới nhất.

- composer.json
- composer.lock
- package.json
- package-lock.json
- index.php

### 6. Cập nhật composer.json/composer.lock

Nếu bạn đã tự cài đặt các thư viện bên ngoài như packagist, hãy yêu cầu lại.

Ví dụ, nếu bạn đã cài đặt psr/http-message, hãy thực hiện lệnh dưới đây.

```
composer require psr/http-message --no-plugins --no-scripts
```

Nếu bạn sử dụng plugin với Symfony Bundle, hãy kiểm tra composer.json của plugin và cài đặt các thư viện phụ thuộc.

Ví dụ, đối với plugin API, hãy kiểm tra composer.json và cài đặt các thư viện phụ thuộc như dưới đây.

```
$ cat app/Plugin/Api42/composer.json
...
  "require": {
    "ec-cube/plugin-installer": "^2.0",
    "league/oauth2-server-bundle": "^0.5",
    "nyholm/psr7": "^1.2",
    "php-http/message-factory": "*",
    "webonyx/graphql-php": "^14.0"

$ composer require league/oauth2-server-bundle:^0.5 --no-plugins --no-scripts
$ composer require nyholm/psr7:^1.2 --no-plugins --no-scripts
$ composer require php-http/message-factory --no-plugins --no-scripts
$ composer require webonyx/graphql-php:^14.0 --no-plugins --no-scripts
```

Hãy xóa bộ nhớ đệm bằng lệnh dưới đây.

```
rm -rf var
bin/console cache:clear --no-warmup
```

Hãy thực hiện lệnh dưới đây.

```
bin/console eccube:composer:require-already-installed
```

### 6. Cập nhật schema/di chuyển

Sử dụng chức năng cập nhật schema và di chuyển để nâng cấp cơ sở dữ liệu.

Hãy thực hiện lệnh dưới đây.

<span style="color:#ff0000;">
※ Có thể xảy ra lỗi sau khi thực hiện lệnh cập nhật schema.
</span>

`In Eccube_KernelProdContainer.php line 1936:
Attempted to call an undefined method named "registerUniqueLoader" of class
"Doctrine\\Common\\Annotations\\AnnotationRegistry".`


Lỗi này xảy ra do cấu hình cache của Symfony vẫn còn cũ mặc dù dữ liệu của Symfony đã thay đổi.
Để giải quyết vấn đề này, cần xóa thư mục var chứa cache và các tệp log.
Hãy xóa thư mục var bằng lệnh dưới đây và thực hiện lại cập nhật schema.

Xóa thư mục var

```
rm -rf var
```


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

Danh sách các tệp thay đổi từ 4.2.3 lên 4.3.0 như sau.
Bạn có thể kiểm tra sự khác biệt của các thay đổi từ [sự khác biệt](#sự khác biệt).

- src/Eccube/Resource/template/admin/Content/news_edit.twig
- src/Eccube/Resource/template/admin/Order/index.twig
- src/Eccube/Resource/template/admin/Order/shipping.twig
- src/Eccube/Resource/template/admin/Product/category.twig
- src/Eccube/Resource/template/admin/Product/class_category.twig
- src/Eccube/Resource/template/admin/Product/class_name.twig
- src/Eccube/Resource/template/admin/Product/csv_class_category.twig
- src/Eccube/Resource/template/admin/Product/csv_class_name.twig
- src/Eccube/Resource/template/admin/Product/product_class.twig
- src/Eccube/Resource/template/admin/Setting/Shop/mail.twig
- src/Eccube/Resource/template/admin/Setting/Shop/payment_edit.twig
- src/Eccube/Resource/template/admin/Setting/Shop/shop_master.twig
- src/Eccube/Resource/template/admin/Setting/System/system.twig
- src/Eccube/Resource/template/admin/Store/plugin_table.twig
- src/Eccube/Resource/template/admin/change_password.twig
- src/Eccube/Resource/template/admin/default_frame.twig
- src/Eccube/Resource/template/admin/error.twig
- src/Eccube/Resource/template/admin/info.twig
- src/Eccube/Resource/template/admin/notice_debug_mode.twig
- src/Eccube/Resource/template/default/Block/auto_new_item.twig
- src/Eccube/Resource/template/default/Block/google_analytics.twig
- src/Eccube/Resource/template/default/Block/new_item.twig
- src/Eccube/Resource/template/default/Cart/index.twig
- src/Eccube/Resource/template/default/Shopping/alert.twig
- src/Eccube/Resource/template/default/Shopping/shipping.twig
- src/Eccube/Resource/template/default/default_frame.twig

### 9. Vô hiệu hóa chế độ bảo trì

Truy cập giao diện quản lý của EC-CUBE, từ "Quản lý nội dung" chọn "Quản lý bảo trì" và vô hiệu hóa chế độ bảo trì.

Hoặc, bạn có thể vô hiệu hóa chế độ bảo trì bằng cách xóa tệp ".maintenance" trong thư mục gốc của EC-CUBE.

## Sự khác biệt

Bạn có thể kiểm tra sự khác biệt chi tiết từ 4.2.3 lên 4.3.0 từ liên kết dưới đây.

[https://github.com/EC-CUBE/ec-cube/compare/4.2.3...4.3.0](https://github.com/EC-CUBE/ec-cube/compare/4.2.3...4.3.0?w=1#files_bucket){:target="_blank"}
