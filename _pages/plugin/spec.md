---
title: Đặc tả plugin
keywords: plugin đặc tả plugin spec
tags: [quickstart, getting_started]
permalink: plugin_spec

---

## Tổng quan

Mô tả tổng quan về đặc tả plugin.

## Cấu trúc thư mục

Cấu trúc thư mục phổ biến của plugin như sau:

```
app/Plugin/SamplePlugin/
├── Command
├── Common
│   └── Nav.php
├── Controller
├── Doctrine
│   └── Query
├── Entity
├── EventListener
│   └── EventListener.php
├── Form
│   ├── Extension
│   └── Type
├── PluginManager.php
├── Repository
├── Resource
│   ├── assets
│   ├── config
│   │   └── services.yaml
│   ├── locale
│   └── template
└── composer.json
```

Không bắt buộc phải có tất cả các thư mục/file trên.
Chỉ bắt buộc phải có `composer.json`.

## File cấu hình

Có 2 file cấu hình chính: `composer.json` (mô tả thông tin plugin) và `services.yaml` (định nghĩa container).

### composer.json

Mô tả thông tin plugin.
Đặt tại `[thư mục plugin]/composer.json`.

Các mục cấu hình:

- name: Tên package
    - Ghi dạng "ec-cube/[mã plugin]"
- version: Phiên bản
    - Số version của plugin, theo format version của PHP.
- description: Tên plugin
- type: Loại package
    - Ghi là "eccube-plugin"
- require: Package phụ thuộc
    - Nếu plugin dùng package ngoài, thêm vào đây.
    - Luôn ghi "ec-cube/plugin-installer": "~0.0.6"
- extra: Thông tin bổ sung
    - Ghi "code": "[mã plugin]"

Ví dụ:

```yaml
{
    "name": "ec-cube/ProductReview",
    "version": "1.0.0",
    "description": "Plugin đánh giá sản phẩm",
    "type": "eccube-plugin",
    "require": {
        "ec-cube/plugin-installer": "~0.0.6"
    },
    "extra": {
        "code": "ProductReview"
    }
}
```

### services.yaml

Định nghĩa container.
Đặt tại `[thư mục plugin]/Resouce/config/services.yaml`.
Có thể viết bằng yaml, php hoặc xml.

Tham khảo thêm về định nghĩa container tại tài liệu chính thức của Symfony:
https://symfony.com/doc/current/service_container.html

### Các file cấu hình khác
Có thể thêm file cấu hình riêng cho plugin, nhưng các file sinh ra hoặc thay đổi sau khi cài đặt plugin nên đặt dưới `app/PluginData`.
Nếu đặt trong thư mục plugin, các file này sẽ bị mất khi update hoặc cài lại plugin.
Khi dùng `app/PluginData`, nên tạo thư mục `app/PluginData/[mã plugin]` để tránh xung đột với plugin khác.

## Nội dung tĩnh

Các file tĩnh (html, css, js, ảnh, ...) dùng trong plugin nên đặt dưới `Resource/assets`. Khi cài/upgrade plugin, thư mục này sẽ được copy sang `[EC-CUBE_HOME]/html/plugin/[mã plugin]/assets`. [#3821](https://github.com/EC-CUBE/ec-cube/pull/3821)

Ví dụ, nếu đặt file `sample.jpg` như sau, sẽ được copy sang `[EC-CUBE_HOME]/html/plugin/SamplePlugin/assets/sample.jpg`:

```
SamplePlugin
 └── Resource
      └── assets
         └── sample.jpg
```

Từ file twig, có thể lấy đường dẫn như sau:

```twig
{% raw %}{{ asset('SamplePlugin/assets/sample.jpg', 'plugin') }}{% endraw %}
```

Đường dẫn thực tế sẽ là:

```
/html/plugin/SamplePlugin/assets/sample.jpg
```

## Đóng gói plugin

Khi muốn phân phối hoặc đăng ký plugin lên Owners Store, cần đóng gói plugin thành file tar.gz.
Lưu ý:
- Không nén cả thư mục cha
- Không đưa các file .git, .DS_Store vào gói

```bash
$ cd app/Plugin/[PluginDir]
$ COPYFILE_DISABLE=1 tar --exclude  ".git" --exclude ".DS_Store" -cvzf ../[PluginDir].tar.gz *
```

## Thay đổi so với 3.0.x

Các thay đổi chính so với 3.0.x:

- Bỏ ServiceProvider
    - Định nghĩa container chuyển sang dùng cơ chế của Symfony.
- Thay đổi cơ chế migration
    - Migration dùng doctrine:schema:update.
    - PluginManager không thực hiện migration, chỉ thêm/sửa/xóa dữ liệu khởi tạo.
- Không khuyến khích dùng hook point
    - Các hook như `eccube.event.admin.request` không khuyến khích dùng nữa.
    - Nếu muốn chèn phần vào twig, hãy chuẩn bị snippet để người dùng tự dán vào.
    - https://github.com/EC-CUBE/ec-cube/issues/2440
- Plugin chỉ copy file sẽ không được load
    - Cần có record trong dtb_plugin.

## Plugin mẫu

- [Plugin mẫu thanh toán](https://github.com/EC-CUBE/sample-payment-plugin){:target="_blank"}
