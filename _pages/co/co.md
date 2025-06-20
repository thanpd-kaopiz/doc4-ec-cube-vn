---
layout: single
title: ec-cube.co
keywords: co ec-cube.co Cloud version
tags: [co, ec-cube.co]
permalink: co
folder: co
---

---

![ec-cube.co](./images/co/co.png)

## ec-cube.co là gì?

ec-cube.co là dịch vụ EC-CUBE phiên bản cloud được vận hành bởi Công ty Cổ phần EC-CUBE.

Việc bảo trì, vận hành hạ tầng và quản lý EC-CUBE sẽ do Công ty Cổ phần EC-CUBE đảm nhận.

ec-cube.co giúp các chủ shop và nhà phát triển tập trung vào vận hành cửa hàng và xây dựng website mà không phải lo lắng về bảo trì, vận hành server hay ứng dụng.

## Thông tin hệ thống

### Kiến trúc của ec-cube.co

[Google Cloud Anthos Day: Track 2 - 5『Nền tảng xây dựng EC site tự do với GKE』](https://www.youtube.com/watch?v=woK-Zzi-eUQ){:target="_blank"}

### EC-CUBE

Mã nguồn EC-CUBE sử dụng trên ec-cube.co (4.0/4.1/4.2) được công khai tại các branch [co/master](https://github.com/EC-CUBE/ec-cube/tree/co/master){:target="_blank"}, [co/4.1](https://github.com/EC-CUBE/ec-cube/tree/co/4.1){:target="_blank"}, [co/4.2](https://github.com/EC-CUBE/ec-cube/tree/co/4.2){:target="_blank"}.
Branch [4.2](https://github.com/EC-CUBE/ec-cube/tree/4.2){:target="_blank"} sẽ được merge định kỳ vào branch [co/4.2](https://github.com/EC-CUBE/ec-cube/tree/co/4.2){:target="_blank"} trong các đợt bảo trì hàng tuần.

Mã nguồn EC-CUBE đang áp dụng cho ec-cube.co (bản 4.2) có thể kiểm tra tại [co/4.2-YYYYMMDD](https://github.com/EC-CUBE/ec-cube/tags){:target="_blank"}.
Mã nguồn EC-CUBE đang áp dụng cho ec-cube.co (bản 4.1) có thể kiểm tra tại [co/4.1-YYYYMMDD](https://github.com/EC-CUBE/ec-cube/tags){:target="_blank"}.
Mã nguồn EC-CUBE đang áp dụng cho ec-cube.co (bản 4.0) có thể kiểm tra tại [co/YYYYMMDD](https://github.com/EC-CUBE/ec-cube/tags){:target="_blank"}.

### Middleware

- Apache 2.4.x
- PostgreSQL 10.x
- PHP 7.4.x (EC-CUBE 4.0/4.1) / PHP 8.1.x (EC-CUBE 4.2)
- Danh sách extension PHP:
  - Core, date, libxml, openssl, pcre, sqlite3, zlib, ctype, curl, dom, fileinfo, filter, ftp, hash, iconv, json, mbstring, SPL, PDO, session, posix, Reflection, standard, SimpleXML, pdo_sqlite, Phar, tokenizer, xml, xmlreader, xmlwriter, mysqlnd, apache2handler, exif, gd, intl, pdo_pgsql, sodium, zip, Zend OPcache

## CookBook

- Hướng dẫn chuyển đổi từ bản download EC-CUBE sang ec-cube.co (đang cập nhật)
