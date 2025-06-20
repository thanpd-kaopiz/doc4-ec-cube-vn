---
title: Cài đặt bằng Web Installer từ Composer
keywords: cài đặt Composer Web Installer
tags: [quickstart, install, composer]
permalink: quickstart/composer_web_installer
folder: quickstart
---

---

Phương pháp này gần giống với [Cài đặt từ dòng lệnh](/quickstart/command_install).   
Khác biệt là sau khi thực hiện, màn hình cài đặt EC-CUBE sẽ xuất hiện. Phù hợp cho ai muốn cài đặt qua giao diện web.

Ở bước 3 trong [Cài đặt từ dòng lệnh](/quickstart/command_install), thay bằng lệnh sau:

```shell
php composer.phar create-project --no-scripts ec-cube/ec-cube ec-cube "4.1.x-dev" --keep-vcs
```

Thư mục ec-cube sẽ được tạo, di chuyển vào đó và chạy web server tích hợp:

```shell
cd ec-cube
php bin/console server:run
```

Truy cập [http://127.0.0.1:8000/](http://127.0.0.1:8000/){:target="_blank"} để bắt đầu cài đặt EC-CUBE qua giao diện web.

*Để dừng web server, nhấn `Ctrl+C`*
