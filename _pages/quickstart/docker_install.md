---
title: Cài đặt bằng Docker
keywords: cài đặt Docker
tags: [quickstart, install, docker]
permalink: quickstart/docker_install
folder: quickstart
---

---

+ Trước tiên, bạn cần [cài đặt Docker Desktop](https://hub.docker.com){:target="_blank"}.
  + Đối với Windows, nên sử dụng [Docker Desktop WSL 2 Backend](https://docs.docker.jp/docker-for-windows/wsl.html#docker-desktop-wsl-2){:target="_blank"} và tạo workspace trên hệ thống file Linux để đạt hiệu năng tốt.
+ Mặc định sử dụng SQLite3.
+ Có thể sử dụng file trên container hoặc mount VOLUME để sử dụng file local.

```shell
cd path/to/ec-cube
docker build -t eccube4-php-apache .

## Sử dụng file trên container
Docker run --name ec-cube -p "8080:80" -p "4430:443" eccube4-php-apache

## Mount thư mục local
# Nếu mount thư mục var sẽ rất chậm, chỉ nên mount src, html, app
Docker run --name ec-cube -p "8080:80" -p "4430:443"  -v "$PWD/html:/var/www/html/html:cached" -v "$PWD/src:/var/www/html/src:cached" -v "$PWD/app:/var/www/html/app:cached" eccube4-php-apache
```

**Từ lần khởi động thứ 2 trở đi, sử dụng lệnh sau:**

```shell
docker start --attach ec-cube
```

#### Chỉnh sửa file cấu hình

Nếu muốn chỉnh sửa file như .env trong thư mục cài đặt, hãy chỉnh sửa trực tiếp trên container hoặc mount riêng file đó.

```shell
docker exec -it ec-cube /bin/bash
root@de5372ce7139:/var/www/html# vi .env
```

#### Sử dụng gửi mail

Sử dụng mailcatcher

```shell
## Trong file .env, đặt MAILER_URL=smtp://mailcatcher:1025
docker run -d -p 1080:1080 -p 1025:1025 --name mailcatcher schickling/mailcatcher
docker run --name ec-cube -p "8080:80" -p "4430:443"  --link mailcatcher:mailcatcher eccube4-php-apache
```

[Xem chi tiết về mailcatcher](/development-tools/mail-catcher)

#### Sử dụng PostgreSQL

```shell
## Trong file .env, đặt DATABASE_URL=pgsql://postgres:password@db/cube4_dev
docker run --name container_postgres -e POSTGRES_PASSWORD=password  -p 5432:5432 -d postgres
docker run --name ec-cube -p "8080:80" -p "4430:443" --link container_postgres:db eccube4-php-apache
```

#### Sử dụng MySQL

```shell
## Trong file .env, đặt DATABASE_URL=mysql://root:password@db/cube4_dev
docker run --name container_mysql -e MYSQL_ROOT_PASSWORD=password  -d -p 3306:3306 mysql:5.7
docker run --name ec-cube -p "8080:80" -p "4430:443" --link container_mysql:db eccube4-php-apache
```
