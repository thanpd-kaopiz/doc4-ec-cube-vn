---
title: Cấu trúc thư mục và tệp tin
keywords: spec directory structure
tags: [spec, getting_started]
permalink: spec_directory-structure

layout: single
---

## Đặc điểm

1. Dựa trên [Cấu trúc thư mục của Symfony3](https://symfony.com/doc/3.4/quick_tour/the_architecture.html){:target="_blank"}, EC-CUBE 4 có cấu trúc riêng biệt.

## Các thư mục chính và vai trò

### app/

- Chứa các tệp cấu hình, plugin, mã PHP tuỳ biến EC-CUBE, v.v... Đây là nơi chứa các tệp thay đổi theo từng ứng dụng.

```
app
├── Customize   Chứa mã PHP tuỳ biến
├── Plugin      Chứa các plugin đã cài đặt
├── PluginData  Chứa các tệp do plugin sử dụng
├── config      Chứa các tệp cấu hình
├── proxy       Chứa các class Proxy được sinh ra bởi chức năng mở rộng Entity
└── template    Chứa các tệp template bị ghi đè
```

### bin/

- Chứa các tệp thực thi phục vụ phát triển như `bin/console`.

### html/

- Chứa các tệp tài nguyên (js, css, hình ảnh, ...)

### src/

- Chứa mã nguồn chính của EC-CUBE, bao gồm các tệp php và Twig

### tests/

- Chứa mã kiểm thử

### var/

- Chứa các tệp sinh ra khi chạy hệ thống như cache, log

### vendor/

- Chứa các thư viện bên thứ ba phụ thuộc
