---
layout: single
title: Sử dụng file .env trong môi trường production
keywords: cài đặt
tags: [quickstart, install, dotenv]
permalink: quickstart/dotenv
folder: quickstart
description: Hướng dẫn sử dụng file .env trong môi trường production.
---

## Về việc sử dụng file .env trong môi trường production

Sau khi cài đặt xong, một file **.env** sẽ được tạo ra trong thư mục cài đặt, chứa thông tin kết nối database và các biến môi trường khác.
**File .env** chủ yếu dùng cho mục đích phát triển, không khuyến khích sử dụng trong môi trường production.
Trong môi trường production, nên thiết lập biến môi trường trong file cấu hình của server để đảm bảo an toàn, tránh lộ thông tin ra ngoài.

### Ví dụ thiết lập với Apache

Thiết lập trong httpd.conf hoặc file .htaccess:

```
SetEnv APP_ENV prod
SetEnv APP_DEBUG 0
SetEnv DATABASE_URL pgsql://dbuser:password@127.0.0.1/cube4_dev
SetEnv DATABASE_SERVER_VERSION 10.5
SetEnv ECCUBE_AUTH_MAGIC 8PPlCHZVdH5vbMkIUKeuTeDHycQQMuaB
SetEnv ECCUBE_ADMIN_ALLOW_HOSTS []
SetEnv ECCUBE_FORCE_SSL false
SetEnv ECCUBE_ADMIN_ROUTE admin
SetEnv ECCUBE_COOKIE_PATH /
```

[Tham khảo: Apache HTTP Server 2.4 - SetEnv directive](https://httpd.apache.org/docs/2.4/ja/mod/mod_env.html#setenv){:target="_blank"}

### Lưu ý khi thiết lập biến môi trường trong file cấu hình server

Khi thiết lập biến môi trường trong file cấu hình server, bạn sẽ không thể thay đổi các chức năng sau từ trang quản trị:

**Cần thay đổi biến môi trường trong file cấu hình server và xóa cache sau khi thay đổi.**

- Quản lý template tại: Quản trị → Owners Store → Template
- Quản lý bảo mật tại: Quản trị → Cài đặt → Cài đặt hệ thống → Quản lý bảo mật

### Về việc sử dụng lệnh bin/console

Khi sử dụng lệnh `bin/console`, mặc định sẽ lấy biến môi trường từ file .env.
Nếu không dùng .env, hãy thiết lập biến môi trường trong shell.
Nên đặt quyền file cấu hình shell như `.bashrc` là 600 để đảm bảo an toàn.

```
## Ví dụ thiết lập trong .bashrc
export APP_ENV="prod"
export APP_DEBUG="0"
export DATABASE_URL="pgsql://dbuser:password@127.0.0.1/cube4_dev"
export DATABASE_SERVER_VERSION="10.5"
export ECCUBE_AUTH_MAGIC="8PPlCHZVdH5vbMkIUKeuTeDHycQQMuaB"
export ECCUBE_ADMIN_ALLOW_HOSTS="[]"
export ECCUBE_FORCE_SSL="false"
export ECCUBE_ADMIN_ROUTE="admin"
export ECCUBE_COOKIE_PATH="/"
```

