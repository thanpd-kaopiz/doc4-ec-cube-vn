---
layout: single
title: Cài đặt bằng Docker Compose (dành cho EC-CUBE4.0.5 trở xuống)
keywords: cài đặt
tags: [quickstart, install, docker, docker-compose]
permalink: quickstart/install_docker-compose_405orlower
folder: quickstart
description: Hướng dẫn cài đặt EC-CUBE 4.0.5 trở xuống bằng Docker Compose.
---

---

**Đây là phương pháp khuyến nghị nếu bạn muốn xây dựng nhanh môi trường phát triển kèm các dịch vụ liên quan (DB, môi trường debug mail, v.v.)**

Yêu cầu đã cài đặt [Docker Desktop](https://hub.docker.com){:target="_blank"}.

+ Mặc định sử dụng SQLite3
+ Mount thư mục local

```shell
cd path/to/ec-cube

# Khởi động container (lần đầu sẽ build)
docker-compose up -d

# Lần đầu cần chạy script cài đặt (LƯU Ý: chạy bằng user `www-data`!)
docker-compose exec -u www-data ec-cube bin/console eccube:install
```

Từ lần khởi động thứ 2 trở đi cũng dùng các lệnh sau.
```shell
# Khởi động container
docker-compose up -d

# Dừng container
docker-compose down
```

#### Sử dụng các container
Bao gồm web server chạy EC-CUBE 4 và các container sau có thể khởi động dễ dàng:

| Tên container  | Mô tả                             | Truy cập trình duyệt |
| -------------- | --------------------------------- | -------------------- |
| ec-cube        | Web server PHP cho EC-CUBE        | [http://localhost:8080](http://localhost:8080){:target="_blank"} |
| postgres       | PostgreSQL database server        |                      |
| mysql          | MySQL database server             |                      |
| mailcatcher    | SMTP server debug MailCatcher     | [http://localhost:1080](http://localhost:1080){:target="_blank"} |

Khi khởi động, liệt kê tên container để chỉ khởi động các dịch vụ cần thiết.
```shell
# Ví dụ: Khởi động EC-CUBE, MySQL, phpMyAdmin và MailCatcher
docker-compose up -d ec-cube mysql mailcatcher

# Nếu không chỉ định, tất cả dịch vụ sẽ được khởi động
docker-compose up -d
```
Khi kết hợp với các container khác, cần thiết lập như sau.
##### Sử dụng gửi mail
Trong `.env` đặt `MAILER_URL=smtp://mailcatcher:1025`.

##### Sử dụng PostgreSQL
Trong `.env` đặt `DATABASE_URL=postgres://dbuser:secret@postgres/eccubedb`.

Nếu chưa khởi tạo schema database, cần chạy lệnh sau.
```
# Tạo schema + nạp dữ liệu mẫu
docker-compose exec ec-cube composer run-script compile
```

##### Sử dụng MySQL
Trong `.env`

