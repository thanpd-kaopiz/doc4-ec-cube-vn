---
title: Thiết lập môi trường
keywords: debug
tags: [debug, env]
permalink: environmental_setting
folder: i18n

---

## Tổng quan

Mở file .env ở thư mục gốc dự án ec-cube, bạn sẽ thấy biến APP_ENV.

Thay đổi giá trị APP_ENV để thiết lập các cấu hình khác nhau cho từng môi trường.

Khi bật chế độ phát triển bằng biến môi trường, bạn sẽ có nhiều chức năng hỗ trợ phát triển, nhưng thông tin nội bộ sẽ hiển thị khi truy cập từ trình duyệt. Chỉ nên sử dụng chế độ phát triển khi làm local, khi public lên internet phải chuyển sang chế độ production.

## Ví dụ thiết lập


### Môi trường production

Thiết lập như sau cho môi trường production:

```
APP_ENV=prod
```


### Môi trường phát triển

Thiết lập như sau cho môi trường phát triển:

```
APP_ENV=dev
```


### Môi trường test

Thiết lập như sau cho môi trường test:

```
APP_ENV=test
```


## Vị trí file cấu hình

Các file cấu hình cho từng môi trường nằm trong thư mục app/config/eccube/packages/.


## Hiển thị profiler

Khi `APP_ENV=dev`,

bạn có thể hiển thị thanh công cụ profiler của symfony.

![Vị trí thanh debug toolbar](/doc4-ec-cube-vn/images/environmental_setting/debug_toolbar1.png)

Nhấn vào icon symfony,

sẽ hiển thị thanh công cụ ở dưới cùng màn hình như sau:

![Mở thanh debug toolbar](/doc4-ec-cube-vn/images/environmental_setting/debug_toolbar2.png)

Bạn có thể kiểm tra SQL đã thực thi, nội dung request, tốc độ hiển thị và nhiều thông tin khác ngay trên trình duyệt.
