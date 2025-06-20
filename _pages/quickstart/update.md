---
layout: single
title: Nâng cấp phiên bản 4.0
keywords: howto update
tags: [quickstart, getting_started]
permalink: update
summary : Hướng dẫn nâng cấp phiên bản 4.0.x.
---

Trước khi thực hiện nâng cấp trên môi trường sản xuất, hãy đảm bảo kiểm tra trước trên môi trường thử nghiệm.
{: .notice--danger}
Hướng dẫn này giả định rằng bạn đang sử dụng gói EC-CUBE tải về từ ec-cube.net.
{: .notice--danger}
Nếu bạn đã tùy chỉnh mã nguồn của EC-CUBE (các thư mục app/config/eccube, app/DoctrineMigrations, bin, src, html), các tệp sẽ bị ghi đè và bạn không thể nâng cấp theo hướng dẫn này. Hãy kiểm tra [sự khác biệt giữa các phiên bản](#sự khác biệt giữa các phiên bản) và tích hợp các thay đổi cần thiết.
{: .notice--danger}
EC-CUBE 4.0.6 trở về trước có chứa [lỗ hổng bảo mật mức độ "cao"](https://www.ec-cube.net/info/weakness/index.php?level=0&version=4.0). Hãy nâng cấp lên phiên bản EC-CUBE 4.0.6-p2 hoặc cao hơn.
{: .notice--danger}

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
1. Tái tạo proxy
1. Cập nhật tệp mẫu giao diện
1. Vô hiệu hóa chế độ bảo trì
1. Khác

## Chi tiết các bước

### 1. Sao lưu trang web

Hãy sao lưu toàn bộ thư mục cài đặt của EC-CUBE.

Cũng hãy sao lưu toàn bộ cơ sở dữ liệu của bạn.

### 2. Kích hoạt chế độ bảo trì (phiên bản 4.0.1 trở lên)

Truy cập giao diện quản lý của EC-CUBE, từ "Quản lý nội dung" chọn "Quản lý bảo trì" và kích hoạt chế độ bảo trì.

Hoặc, bạn có thể kích hoạt chế độ bảo trì bằng cách tạo tệp ".maintenance" trong thư mục gốc của EC-CUBE.

```
[root]
  │
  ├──.maintenance
  │
```

※ Khi sử dụng chế độ bảo trì, nếu truy cập vào các trang ngoài giao diện quản lý, màn hình bảo trì sẽ được hiển thị.

※ Tính năng này chỉ có thể sử dụng nếu phiên bản EC-CUBE là "4.0.1" trở lên.

### 3. Thay thế các tệp nguồn của EC-CUBE bằng phiên bản đã nâng cấp

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

### 4. Thay thế tệp riêng lẻ

Đối với từng phiên bản, cần thay thế các tệp riêng lẻ.

Hãy kiểm tra các tệp cần thay thế từ dưới đây và ghi đè bằng các tệp mới nhất.

| Phiên bản nâng cấp | Tệp cần thay thế                                                                              |
|----------------------|---------------------------------------------------------------------------------------------------|
| 4.0.0 → 4.0.1        | composer.json<br>composer.lock<br>.htaccess<br>index.php<br>maintenance.php|
| 4.0.1 → 4.0.2        | composer.json<br>composer.lock|
| 4.0.2 → 4.0.3        | composer.json<br>composer.lock<br>.htaccess<br>index.php|
| 4.0.3 → 4.0.4        | composer.json<br>composer.lock<br>.htaccess<br>app/Customize/Resource<br>var/.htaccess|
| 4.0.4 → 4.0.5-p1        | composer.json<br>composer.lock<br>.htaccess<br>robots.txt<br>app/template/plugin|
| 4.0.5 → 4.0.6        | composer.lock<br>symfony.lock<br>.htaccess|
| 4.0.6 → 4.0.6-p1     | .htaccess|
| 4.0.6-p1 → 4.0.6-p2     | -|
- ※ Nếu tệp cần thay thế bao gồm composer.json/composer.lock, sau khi ghi đè, hãy thực hiện bước `cập nhật composer.json/composer.lock`.
- ※ Nếu thực hiện nâng cấp qua nhiều phiên bản như `4.0.0 → 4.0.2`, hãy nâng cấp từng bước như `4.0.0 → 4.0.1`→`4.0.1 → 4.0.2`.
- ※ Khi tải lên tệp qua FTP, có thể quyền truy cập sẽ bị thay đổi. Hãy tham khảo [cài đặt quyền truy cập](/quickstart/permission) để kiểm tra quyền truy cập.
- ※ Hãy kiểm tra [danh sách lỗ hổng bảo mật trên trang chính thức](https://www.ec-cube.net/info/weakness/) và tìm kiếm theo phiên bản tương ứng để áp dụng các bản vá cần thiết.

Sau khi ghi đè, hãy xóa bộ nhớ đệm bằng lệnh dưới đây.

```
bin/console cache:clear --no-warmup
```

### 5. Cập nhật composer.json/composer.lock

Bước này chỉ cần thiết nếu bạn đáp ứng tất cả các điều kiện dưới đây. Nếu không, hãy bỏ qua.

- Tệp cần thay thế trong bước `thay thế tệp riêng lẻ` bao gồm composer.json/composer.lock
- Đã cài đặt plugin

Hãy thực hiện lệnh dưới đây.

```
bin/console eccube:composer:require-already-installed
```

Nếu bạn đã tự cài đặt các thư viện bên ngoài như packagist, hãy yêu cầu lại.

Ví dụ, nếu bạn đã cài đặt psr/http-message, hãy thực hiện lệnh dưới đây.

```
composer require psr/http-message
```

### 6. Cập nhật schema/di chuyển

Sử dụng chức năng cập nhật schema và di chuyển để nâng cấp cơ sở dữ liệu.

Hãy thực hiện lệnh dưới đây.

**※ Không cần cập nhật schema khi nâng cấp lên các phiên bản 4.0.0 → 4.0.1, 4.0.1 → 4.0.2, 4.0.4 → 4.0.5-p1, 4.0.5 → 4.0.6, 4.0.6 → 4.0.6-p1, 4.0.6-p1 → 4.0.6-p2.**

Tham khảo: [Khi plugin bị vô hiệu hóa, Doctrine SchemaTool không nhận diện được mở rộng entity](https://github.com/EC-CUBE/ec-cube/issues/4056){:target="_blank"}


Cập nhật schema

```
bin/console doctrine:schema:update --force --dump-sql
```

Di chuyển

```
bin/console doctrine:migrations:migrate
```

### 7. Tái tạo proxy

Chỉ cần tái tạo proxy khi nâng cấp lên phiên bản 4.0.3. Nếu không, hãy bỏ qua.

Xóa tệp proxy
```
rm -rf app/proxy/entity/*
```

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

### 8. Cập nhật tệp mẫu giao diện

Đối với từng phiên bản, cần cập nhật tệp mẫu giao diện (twig).

Từ "Quản lý nội dung" hoặc "Cài đặt cửa hàng > Cài đặt email" trong giao diện quản lý, hãy chỉnh sửa trang/khối/mẫu email tương ứng.

Bạn có thể kiểm tra sự khác biệt của các thay đổi từ [sự khác biệt giữa các phiên bản](#sự khác biệt giữa các phiên bản).

#### 4.0.0 → 4.0.1

|Tên trang                               |Tên tệp|
|--------------------------------------|---------------|
|Đăng ký thành viên (trang nhập)                     |<a href="../documents/updatedoc/4.0.1/Contact_index_twig.htm" target = "_blank">Contact/index.twig</a>|
|Đăng ký thành viên (trang nhập)                     |<a href="../documents/updatedoc/4.0.1/Entry_index_twig.htm" target = "_blank">Entry/index.twig</a>|
|Trang của tôi/Thay đổi thông tin đăng ký thành viên (trang nhập)     |<a href="../documents/updatedoc/4.0.1/Mypage_change_twig.htm" target = "_blank">Mypage/change.twig</a>|
|Trang của tôi/Thêm địa chỉ giao hàng                   |<a href="../documents/updatedoc/4.0.1/Mypage_delivery_edit_twig.htm" target = "_blank">Mypage/delivery_edit.twig</a>|
|Mua hàng                               |<a href="../documents/updatedoc/4.0.1/Shopping_index_twig.htm" target = "_blank">Shopping/index.twig</a>|
|Mua hàng không đăng ký                      |<a href="../documents/updatedoc/4.0.1/Shopping_nonmember_twig.htm" target = "_blank">Shopping/nonmember.twig</a>|
|Mua hàng/Thêm địa chỉ giao hàng                  |<a href="../documents/updatedoc/4.0.1/Shopping_shipping_edit_twig.htm" target = "_blank">Shopping/shipping_edit.twig</a>|
|Mua hàng/Chỉ định nhiều địa chỉ giao hàng (Thêm địa chỉ giao hàng)|<a href="../documents/updatedoc/4.0.1/Shopping_shipping_multiple_edit_twig.htm" target = "_blank">Shopping/shipping_multiple_edit.twig</a>|

#### 4.0.1 → 4.0.2

|Tên trang                               |Tên tệp|
|--------------------------------------|---------------|
|Trang của tôi/Chi tiết lịch sử mua hàng                    |<a href="https://github.com/EC-CUBE/ec-cube/pull/4008/files" target = "_blank">Mypage/history.twig</a>|
|Email xác nhận đơn hàng                          |<a href="https://github.com/EC-CUBE/ec-cube/pull/4060/files" target = "_blank">Mail/order.twig</a>|
|Email xác nhận đơn hàng (HTML)                    |<a href="https://github.com/EC-CUBE/ec-cube/pull/4060/files" target = "_blank">Mail/order.html.twig</a>|

#### 4.0.2 → 4.0.3

<a href="https://github.com/EC-CUBE/ec-cube/pulls?q=is%3Apr+label%3Aaffected%3Atemplate+is%3Aclosed+milestone%3A4.0.3" target = "_blank">Sự khác biệt của tệp mẫu giao diện</a>

#### 4.0.3 → 4.0.4

<a href="https://github.com/EC-CUBE/ec-cube/pulls?q=is%3Apr+label%3Aaffected%3Atemplate+is%3Aclosed+milestone%3A4.0.4" target = "_blank">Sự khác biệt của tệp mẫu giao diện</a>

#### 4.0.4 → 4.0.5-p1

<a href="https://github.com/EC-CUBE/ec-cube/pulls?q=is%3Apr+label%3Aaffected%3Atemplate+is%3Aclosed+milestone%3A4.0.5" target = "_blank">Sự khác biệt của tệp mẫu giao diện</a>

#### 4.0.5-p1 → 4.0.6、4.0.6 → 4.0.6-p1, 4.0.6-p1 → 4.0.6-p2

Không có cập nhật tệp mẫu giao diện.

### 9. Vô hiệu hóa chế độ bảo trì (phiên bản 4.0.1 trở lên)

Truy cập giao diện quản lý của EC-CUBE, từ "Quản lý nội dung" chọn "Quản lý bảo trì" và vô hiệu hóa chế độ bảo trì.

Hoặc, bạn có thể vô hiệu hóa chế độ bảo trì bằng cách xóa tệp ".maintenance" trong thư mục gốc của EC-CUBE.

※ Tính năng này chỉ có thể sử dụng nếu phiên bản EC-CUBE là "4.0.1" trở lên.

### 10. Khác

#### 4.0.0 -> 4.0.1

Nếu bạn muốn sử dụng [tính năng bảo trì](https://github.com/EC-CUBE/ec-cube/pull/3998){:target="_blank"} được triển khai trong phiên bản 4.0.1, cần ghi vào .env hoặc định nghĩa các giá trị dưới đây như biến môi trường.

```
ECCUBE_LOCALE=ja
ECCUBE_ADMIN_ROUTE=admin
ECCUBE_TEMPLATE_CODE=default

※ Giá trị cài đặt là ví dụ. Hãy thay đổi theo môi trường của bạn.
```

#### 4.0.1 -> 4.0.2

- Nếu bạn muốn sử dụng [thay đổi đường dẫn favicon](https://github.com/EC-CUBE/ec-cube/pull/4075){:target="_blank"}, sau khi áp dụng [sự khác biệt](https://github.com/EC-CUBE/ec-cube/commit/50fcbdea4c66e5eabc03ba1e38ce7952a53ca97d#diff-7cefac9fd3759d999afb711a36b6dad9){:target="_blank"}, hãy tải lên tệp favicon từ quản lý tệp để thay đổi favicon.
- Nếu bạn muốn sử dụng [quản lý CSS](https://github.com/EC-CUBE/ec-cube/pull/4083){:target="_blank"}, cần áp dụng [sự khác biệt](https://github.com/EC-CUBE/ec-cube/commit/7994bd00de19399d7c6a8e22dd280791478b9435#diff-7cefac9fd3759d999afb711a36b6dad9){:target="_blank"}.
- Nếu bạn muốn sử dụng [quản lý Javascript](https://github.com/EC-CUBE/ec-cube/pull/4084){:target="_blank"}, cần áp dụng [sự khác biệt](https://github.com/EC-CUBE/ec-cube/commit/008236d28633d803d18e15abecf5a04224d0a4f4#diff-7cefac9fd3759d999afb711a36b6dad9R50){:target="_blank"}.

#### 4.0.2 -> 4.0.3

- Nếu bạn muốn sử dụng [hỗ trợ cho hệ thống thuế suất giảm](https://github.com/EC-CUBE/ec-cube/issues/4183){:target="_blank"}, cần áp dụng [sự khác biệt](https://github.com/EC-CUBE/ec-cube/pulls?q=is%3Apr+is%3Aclosed+label%3A%E8%BB%BD%E6%B8%9B%E7%A8%8E%E7%8E%87%E5%AF%BE%E5%BF%9C){:target="_blank"}.
  ※ Hãy kiểm tra [lưu ý](/update/4_0_3) kèm theo.
- Nếu bạn muốn sử dụng [thay đổi hình ảnh logo PDF](https://github.com/EC-CUBE/ec-cube/pull/4216){:target="_blank"}, cần áp dụng [sự khác biệt](https://github.com/EC-CUBE/ec-cube/commit/e8f2952925dda75db5b02ab52bf357f59343ecef){:target="_blank"}.
- Nếu bạn muốn sử dụng [tải lên nhiều tệp](https://github.com/EC-CUBE/ec-cube/pull/4235){:target="_blank"}, cần áp dụng [sự khác biệt](https://github.com/EC-CUBE/ec-cube/commit/fe5cae800fa4e7f09cbb905e1ef3632b34e41489){:target="_blank"}.

Quy trình nâng cấp phiên bản của EC-CUBE đã hoàn tất.

## Sự khác biệt giữa các phiên bản

Bạn có thể kiểm tra sự khác biệt chi tiết giữa các phiên bản từ các liên kết dưới đây.

| Phiên bản      | Trang sự khác biệt                                                                                                             |
|-----------------|------------------------------------------------------------------------------------------------------------------------|
| 4.0.0 → 4.0.1   | [https://github.com/EC-CUBE/ec-cube/compare/4.0.0...4.0.1](https://github.com/EC-CUBE/ec-cube/compare/4.0.0...4.0.1?w=1#files_bucket){:target="_blank"}   |
| 4.0.1 → 4.0.2   | [https://github.com/EC-CUBE/ec-cube/compare/4.0.1...4.0.2](https://github.com/EC-CUBE/ec-cube/compare/4.0.1...4.0.2?w=1#files_bucket){:target="_blank"}   |
| 4.0.2 → 4.0.3   | [https://github.com/EC-CUBE/ec-cube/compare/4.0.2...4.0.3](https://github.com/EC-CUBE/ec-cube/compare/4.0.2...4.0.3?w=1#files_bucket){:target="_blank"}   |
| 4.0.3 → 4.0.4   | [https://github.com/EC-CUBE/ec-cube/compare/4.0.3...4.0.4](https://github.com/EC-CUBE/ec-cube/compare/4.0.3...4.0.4?w=1#files_bucket){:target="_blank"}   |
| 4.0.4 → 4.0.5-p1   | [https://github.com/EC-CUBE/ec-cube/compare/4.0.4...4.0.5-p1](https://github.com/EC-CUBE/ec-cube/compare/4.0.4...4.0.5-p1?w=1#files_bucket){:target="_blank"}   |
| 4.0.5-p1 → 4.0.6   | [https://github.com/EC-CUBE/ec-cube/compare/4.0.5-p1...4.0.6](https://github.com/EC-CUBE/ec-cube/compare/4.0.5-p1...4.0.6?w=1#files_bucket){:target="_blank"}   |
| 4.0.6 → 4.0.6-p1   | [https://github.com/EC-CUBE/ec-cube/compare/4.0.6...4.0.6-p1](https://github.com/EC-CUBE/ec-cube/compare/4.0.6...4.0.6-p1?w=1#files_bucket){:target="_blank"}   |
| 4.0.6-p1 → 4.0.6-p2   | [https://github.com/EC-CUBE/ec-cube/compare/4.0.6-p1...4.0.6-p2](https://github.com/EC-CUBE/ec-cube/compare/4.0.6-p1...4.0.6-p2?w=1#files_bucket){:target="_blank"}   |

