---
title: Phát triển Plugin
keywords: plugin phát triển
tags: [plugin, development]
permalink: plugin_development

---

Giải thích các bước cơ bản để phát triển plugin.

## Điều kiện tiên quyết

- Đã [cài đặt EC-CUBE ở môi trường local](/quickstart/install#cui%E3%81%A7%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E3%81%99%E3%82%8B)
- Có thể chạy PHP trên dòng lệnh

## Tạo khung plugin

Có thể tạo khung plugin bằng lệnh `bin/console eccube:plugin:generate`.

```shell
bin/console eccube:plugin:generate


EC-CUBE Plugin Generator Interactive Wizard
===========================================

 name [EC-CUBE Sample Plugin]:
 > <Nhập tên plugin rồi Enter>

 code [Sample]:
 > <Nhập mã plugin rồi Enter>

 ver [1.0.0]:
 > <Nhập số phiên bản rồi Enter>

 [OK] Plugin đã được tạo thành công: EC-CUBE Sample Plugin Sample 1.0.0
```

Sau đó sẽ tạo ra khung plugin tại `app/Plugin/Sample`.

## Cài đặt plugin

Có thể cài đặt bằng lệnh `bin/console eccube:plugin:install --code=<mã plugin>`.

```shell
bin/console eccube:plugin:install --code Sample

 Chạy bin/console cache:clear --no-warmup...

 // Đang xóa cache cho môi trường dev với debug
 // true

 [OK] Đã xóa cache cho môi trường "dev" (debug=true).



 [OK] Đã cài đặt.
```

Sau khi cài đặt, có thể xác nhận tại EC-CUBE quản trị → Owners Store → Plugin → Danh sách plugin.

Các lệnh khác có thể sử dụng khi phát triển, vui lòng xem [tại đây](/quickstart/cli#ec-cube%E3%81%8C%E6%8F%90%E4%BE%9B%E3%81%97%E3%81%A6%E3%81%84%E3%82%8B%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89)。

## Phát triển plugin

Hãy sửa file trong `app/Plugin/<mã plugin>` để phát triển.

Khi xóa plugin, toàn bộ file dưới `app/Plugin/<mã plugin>` cũng sẽ bị xóa vật lý, hãy chú ý!
{: .notice--danger}

## Khác

Nếu muốn quản lý mã nguồn plugin bằng Git, hãy tham khảo bài viết sau:

[Sử dụng Composer để tăng hiệu suất phát triển plugin EC-CUBE4](https://zenn.dev/nanasess/articles/ec-cube4-plugin-development){:target="_blank"}

Nếu muốn viết test E2E cho plugin, hãy tham khảo bài viết sau:

[Viết test E2E cho plugin EC-CUBE trong 10 phút](https://zenn.dev/nanasess/articles/ec-cube-plugin-e2etesting-in-10mins){:target="_blank"}

Nếu muốn test plugin trước khi đăng ký lên Owners Store, hãy xem [trang sau](/plugin_mock_package_api)。
