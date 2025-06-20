---
title: Chế độ debug
keywords: debug
tags: [debug, env]
permalink: debug_mode
folder: i18n

---

## Tổng quan

Khi bật chế độ debug, bạn có thể xem thông tin chi tiết như stack trace trên trang lỗi.

Ngoài ra, file cache sẽ được tạo lại mỗi lần request.

Việc bật chế độ debug bằng biến môi trường sẽ giúp phát triển thuận tiện hơn, nhưng khi truy cập từ trình duyệt, thông tin debug sẽ hiển thị công khai. Chỉ nên sử dụng chế độ debug khi phát triển local, khi public lên internet phải tắt chế độ debug.

## Thiết lập chế độ debug

Mở file .env ở thư mục gốc dự án ec-cube, tìm biến `APP_DEBUG`.

Thay đổi giá trị của `APP_DEBUG` để bật/tắt chế độ debug.

Nếu `APP_DEBUG=0`, khi có lỗi chỉ hiển thị thông báo tối giản.

Nếu `APP_DEBUG=1`, chế độ debug sẽ được bật.

Khi có lỗi ở chế độ debug, màn hình sau sẽ hiển thị:

![Màn hình lỗi](/images/debug_mode/debug_error.png)

Thông thường, nên đặt `APP_DEBUG=1` khi `APP_ENV=dev` hoặc `APP_ENV=test`, và đặt `APP_DEBUG=0` khi `APP_ENV=prod`.


