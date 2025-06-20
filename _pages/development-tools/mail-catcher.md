---
title: MailCatcher
keywords: mailcatcher
tags: [development-tools, mail-catcher]
permalink: /development-tools/mail-catcher
folder: development-tools
---

## Tổng quan

Khi xây dựng môi trường phát triển EC-CUBE trên máy tính, ngoài Web server bạn còn cần một mail server.

Bài viết này hướng dẫn cách xây dựng mail server sử dụng image công khai trên DockerHub.

## Điều kiện tiên quyết

Yêu cầu đã cài đặt Docker for Mac hoặc Docker for Windows trên máy tính.

## Sử dụng MailCatcher

Bằng cách sử dụng <a href="https://mailcatcher.me/" target="_blank">MailCatcher</a>, bạn có thể thêm mail server SMTP vào môi trường phát triển.

Bạn có thể dễ dàng cài đặt mail server bằng cách lấy image MailCatcher từ <a href="https://hub.docker.com/r/schickling/mailcatcher/" target="_blank">DockerHub</a>.

## Cấu hình EC-CUBE

Thêm cấu hình sau vào file `.env` của EC-CUBE:

```
MAILER_URL=smtp://127.0.0.1:1025
```

## Khởi động container Docker
Có 2 cách sau:

### Sử dụng lệnh Docker
Chạy lệnh sau để sử dụng SMTP server:

```bash
$ docker run -d -p 1080:1080 -p 1025:1025 --name mailcatcher schickling/mailcatcher

$ docker ps
CONTAINER ID        IMAGE                    COMMAND                  CREATED              STATUS              PORTS                                            NAMES
41290748f3ab        schickling/mailcatcher   "mailcatcher --no-qu…"   About a minute ago   Up 58 seconds       0.0.0.0:1025->1025/tcp, 0.0.0.0:1080->1080/tcp   mailcatcher
```

Dừng hoặc khởi động lại container:

```bash
# Dừng container
$ docker stop mailcatcher

# Khởi động lại container
$ docker start mailcatcher

```

### Sử dụng Docker Compose

Nếu dùng docker-compose, hãy tạo file `docker-compose.yml` như sau:

```yml
version: '3'

services:
  mailcatcher:
          image: schickling/mailcatcher
          ports:
              - "1080:1080"
              - "1025:1025"
```

```bash
$ docker-compose up -d
```
Chạy lệnh trên để tạo container MailCatcher.

Để dừng, dùng lệnh sau:

```bash
$ docker-compose down
```

## Mail client

Truy cập http://127.0.0.1:1080/ bằng trình duyệt (ví dụ Google Chrome) sẽ thấy giao diện như sau:

![mailcatcher-image](/doc4-ec-cube-vn/images/development-tools/mailcatcher-client.png)

Bạn có thể kiểm tra kết quả gửi mail ngay trên trình duyệt.

## Tham khảo

- <a href="https://mailcatcher.me/" target="_blank">https://mailcatcher.me/</a>
- <a href="https://hub.docker.com/r/schickling/mailcatcher/" target="_blank">https://hub.docker.com/r/schickling/mailcatcher/</a>
