---
title: Cài đặt bằng Docker Compose
keywords: cài đặt Docker docker-composer
tags: [quickstart, install, docker, docker-compose]
permalink: quickstart/docker_compose_install
folder: quickstart
---

---

[Nếu bạn sử dụng EC-CUBE4.0.5 trở xuống, hãy xem tại đây.](/quickstart/install_docker-compose_405orlower)

**Khuyến nghị cho môi trường phát triển khi muốn xây dựng nhanh chóng kèm các dịch vụ liên quan (DB, môi trường debug mail, ...)**

+ Yêu cầu cài đặt trước [Docker Desktop](https://hub.docker.com){:target="_blank"}.
  + Với Windows, nên sử dụng [Docker Desktop WSL 2 Backend](https://docs.docker.jp/docker-for-windows/wsl.html#docker-desktop-wsl-2){:target="_blank"} và tạo workspace trên hệ thống file Linux để đạt hiệu năng tốt.
+ Mặc định sử dụng SQLite3.

```shell
cd path/to/ec-cube

# Khởi động container (lần đầu sẽ build)
docker-compose up -d

# Lần đầu cần chạy script cài đặt (LƯU Ý: chạy bằng user `www-data` và chế độ không tương tác!)
docker-compose exec -u www-data ec-cube bin/console eccube:install -n
```

Các lần khởi động sau cũng dùng lệnh tương tự.

```shell
# Khởi động container
docker-compose up -d

# Dừng container
docker-compose down
```

Khi cài đặt bằng docker-compose, các thiết lập cơ bản sẽ nằm trong mục `environment` của file `docker-compose.yml` (xem thêm ở phần [Sử dụng .env](#env-の使用について)).
**Lưu ý: phải dùng chế độ không tương tác (`-n`) khi chạy lệnh `eccube:install`.**

Có thể chỉ định các file `docker-compose.*.yml` để mount thư mục local hoặc thay đổi database.

#### Sử dụng PostgreSQL

Chỉ định file `docker-compose.pgsql.yml`.

``` shell
docker-compose -f docker-compose.yml -f docker-compose.pgsql.yml up -d
```

Nếu chưa khởi tạo schema database, chạy thêm:

```
# Tạo schema + nạp dữ liệu mẫu
docker-compose -f docker-compose.yml -f docker-compose.pgsql.yml exec ec-cube composer run-script compile
```

#### Sử dụng MySQL

Chỉ định file `docker-compose.mysql.yml`.

``` shell
docker-compose -f docker-compose.yml -f docker-compose.mysql.yml up -d
```

Nếu chưa khởi tạo schema database, chạy thêm:

```
# Tạo schema + nạp dữ liệu mẫu
docker-compose -f docker-compose.yml -f docker-compose.mysql.yml exec ec-cube composer run-script compile
```

#### Mount thư mục local

Chỉ định file `docker-compose.dev.yml`.

```
## Ví dụ dùng MySQL
docker-compose -f docker-compose.yml -f docker-compose.mysql.yml -f docker-compose.dev.yml up -d
```

#### Sử dụng .env

Khi cài đặt bằng docker-compose, các biến môi trường như `DATABASE_URL` nên được thiết lập trong mục `environment` của file `docker-compose.*.yml`.

Nếu muốn sử dụng `.env`, hãy làm như sau:

1. Trong `docker-compose*.yml`, đặt `APP_ENV: ~`
2. Trong file `.env` local, comment dòng `APP_ENV`

Thứ tự ưu tiên của các biến môi trường:

1. `environment` trong `docker-compose*.yml`
2. `.env` local (thiết lập qua docker-compose, không phải php dotenv)
3. `.env` trong container ec-cube (thiết lập qua php dotenv)

#### Đồng bộ file

Khi cài đặt bằng docker-compose, thư mục local và file trong container sẽ được đồng bộ. Các file cấu hình như `.env` cũng chỉnh sửa trực tiếp trên host.

Lưu ý: một số thư mục sẽ bị loại khỏi đồng bộ để tránh giảm hiệu năng nghiêm trọng:
 - /var
 - /vendor
 - /node_modules

Các thư mục này sẽ được lưu trữ riêng bằng Docker Volume.
