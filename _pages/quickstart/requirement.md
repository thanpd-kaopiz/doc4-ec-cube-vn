---
layout: single
author_profile: false
title: Yêu cầu hệ thống
keywords:
tags: [quickstart, getting_started]
permalink: quickstart/requirement

---

## 4.3

| Phân loại | Phần mềm|Phiên bản|
|---|-------|---|
|Máy chủ Web|Apache |2.4.x <br> (mod_rewrite / mod_ssl bắt buộc) |
|PHP |PHP |8.1 〜 8.3 |
|Cơ sở dữ liệu|PostgreSQL|12.x 〜 16.x <br> (quyền tham chiếu bảng pg_settings bắt buộc) |
|Cơ sở dữ liệu|MySQL| 8.0<br> (InnoDB engine bắt buộc) |
|Cơ sở dữ liệu|SQLite(dành cho phát triển) |3.x |

## 4.2

| Phân loại | Phần mềm|Phiên bản|
|---|-------|---|
|Máy chủ Web|Apache |2.4.x <br> (mod_rewrite / mod_ssl bắt buộc) |
|PHP | PHP | 7.4 〜 8.1|
|Cơ sở dữ liệu|PostgreSQL| 10.x 〜 14.x <br> (quyền tham chiếu bảng pg_settings bắt buộc) |
|Cơ sở dữ liệu|MySQL|5.7 hoặc 8.0<br> (InnoDB engine bắt buộc) |
|Cơ sở dữ liệu|SQLite(dành cho phát triển) |3.x |

## 4.0/4.1

| Phân loại | Phần mềm|Phiên bản|
|---|-------|---|
|Máy chủ Web|Apache |2.4.x <br> (mod_rewrite / mod_ssl bắt buộc) |
|PHP | PHP | 7.3 〜 7.4 <small>(※1)</small>|
|Cơ sở dữ liệu|PostgreSQL| 9.6.x 〜 14.x <small>(※2)</small><br> (quyền tham chiếu bảng pg_settings bắt buộc) |
|Cơ sở dữ liệu|MySQL|5.7.x <small>(※3)</small><br> (InnoDB engine bắt buộc) |
|Cơ sở dữ liệu|SQLite(dành cho phát triển) |3.x |

※1 EC-CUBE 4.0.0〜4.0.1 hỗ trợ PHP 7.1〜7.2, 4.0.2〜4.0.3 hỗ trợ PHP 7.1〜7.3, 4.0.4〜4.0.x hỗ trợ PHP 7.1〜7.4  
※2 EC-CUBE 4.0 hỗ trợ PostgreSQL 9.2.x〜13.x  
※3 EC-CUBE 4.0 hỗ trợ MySQL 5.5.x〜5.7.x

# Thư viện PHP

| Phân loại | Thư viện|
|---|---|
|Thư viện bắt buộc|pgsql / mysqli (phù hợp với cơ sở dữ liệu sử dụng) <br> pdo_pgsql / pdo_mysql / pdo_sqlite (phù hợp với cơ sở dữ liệu sử dụng) <br> pdo <br> phar <br> mbstring <br> zlib <br> ctype <br> session <br> JSON <br> xml <br> libxml <br> OpenSSL <br> zip <br> cURL <br> fileinfo <br> intl <br> GD <br> Sodium(※4) |
|Thư viện khuyến nghị|hash <br> APCu / WinCache (phù hợp với môi trường sử dụng) <br> Zend OPcache |

※4 EC-CUBE 4.2 yêu cầu mở rộng Sodium khi sử dụng plugin Web API.  
Nếu không thể cài đặt plugin, hãy tham khảo [mục này](/quickstart/trouble-shooting-for-plugin-install)

# Trình duyệt kiểm tra hoạt động

Giao diện quản lý và mẫu giao diện chuẩn

| Hệ điều hành | Trình duyệt|
|---|-------|
|Windows | Edge mới nhất |
||FireFox mới nhất |
||Google Chrome mới nhất |
|Mac|Safari mới nhất|
|iOS|Safari mới nhất|
|Android| Trình duyệt chuẩn mới nhất|
