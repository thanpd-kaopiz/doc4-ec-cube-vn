---
title: Cài đặt từ dòng lệnh
keywords: cài đặt Docker
tags: [quickstart, install, command]
permalink: quickstart/command_install
folder: quickstart
---

---

**Đây là phương pháp khuyến nghị cho môi trường phát triển.**  
Phương pháp này sẽ cài đặt EC-CUBE4 mới nhất từ GitHub.  
※ Khác với bản đóng gói trên trang chủ chính thức, vui lòng lưu ý.

1. Di chuyển đến thư mục bạn muốn cài đặt EC-CUBE

```shell
cd Địa chỉ thư mục (hoặc kéo & thả thư mục)
```

※ Thư mục ec-cube sẽ được tạo trong thư mục trên.

2. Sau khi di chuyển, tạo file composer.phar  
Thực hiện lệnh trong phần [Cài đặt Composer](https://getcomposer.org/download/){:target="_blank"} để tạo file composer.phar.

Cập nhật composer.phar về phiên bản 1.x tương thích với EC-CUBE 4.0.

```shell
php composer.phar selfupdate --1
```

3. Đảm bảo bạn đang ở đúng thư mục chứa composer.phar, sau đó chạy lệnh sau:

```shell
php composer.phar create-project ec-cube/ec-cube ec-cube "4.1.x-dev" --keep-vcs
```

※ Mặc định sử dụng SQLite3.   
※ Một số phiên bản MacOS có thể thiếu php-intl, hãy cài đặt PHP mới qua homebrew nếu gặp lỗi.

4. Thư mục ec-cube sẽ được tạo, di chuyển vào đó và chạy web server tích hợp:

```shell
cd ec-cube
php bin/console server:run --env=dev
```

5. Truy cập [http://127.0.0.1:8000/admin](http://127.0.0.1:8000/admin){:target='_blank'} để kiểm tra màn hình đăng nhập quản trị EC-CUBE.  
Đăng nhập với:

`ID: admin PW: password`

*Để dừng web server, nhấn `Ctrl+C`*

#### Nếu muốn thay đổi loại database

Sau khi cài đặt, chạy lệnh sau và thiết lập `Database Url`:

```shell
## for MySQL
mysql://<user>:<password>@<host>/<database name>

## for PostgreSQl
postgres://<user>:<password>@<host>/<database name>
```

#### Nếu sử dụng môi trường Windows

Không thể sử dụng lệnh `php bin/console eccube:install`.
Thay vào đó, sử dụng các lệnh sau:

```shell
# (tùy chọn) Xóa database
php bin/console doctrine:database:drop --force
# Tạo database
php bin/console doctrine:database:create
# (tùy chọn) Xóa schema
php bin/console doctrine:schema:drop --force
# Tạo schema
php bin/console doctrine:schema:create
# Nạp dữ liệu khởi tạo
php bin/console eccube:fixtures:load
```

- *Lệnh `php bin/console eccube:install` thực hiện các lệnh trên bên trong.*
- Do Symfony không tương thích tốt với Windows, tốc độ có thể rất chậm. Khuyến nghị [Cài đặt bằng Docker Compose](/quickstart/docker_compose_install).
