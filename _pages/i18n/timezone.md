---
title: Múi giờ
keywords: timezone
tags: [i18n, currency]
permalink: i18n_timezone
folder: i18n

---

## Tổng quan

Trang này giải thích về thiết lập múi giờ trong EC-CUBE.

Cách xử lý dữ liệu ngày giờ và cách thay đổi thiết lập múi giờ.

## Giá trị mặc định

Múi giờ mặc định của EC-CUBE là `Asia/Tokyo`.

## Lưu ý (về lưu và hiển thị dữ liệu ngày giờ)

※ Dữ liệu ngày giờ sẽ luôn được lưu trong database dưới dạng UTC.
{: .notice--danger}

Dữ liệu nhập từ form sẽ được chuyển sang UTC (trừ 9 tiếng so với giờ Nhật) trước khi lưu vào database.

Khi lấy dữ liệu từ database, hệ thống sẽ chuyển đổi sang múi giờ được thiết lập trong `ECCUBE_TIMEZONE`.


### Tham khảo

- [Hỗ trợ kiểu dữ liệu ngày giờ - github](https://github.com/EC-CUBE/ec-cube/pull/2308){:target="_blank"}

## Cách thay đổi thiết lập múi giờ

Múi giờ mặc định là `Asia/Tokyo`,

bạn có thể chuyển đổi múi giờ trong ứng dụng bằng cách chỉ định biến môi trường.

Sao chép file `.env.dist` ở thư mục gốc EC-CUBE thành file mới tên `.env`.

Bỏ comment dòng `ECCUBE_TIMEZONE` trong file `.env` và ghi múi giờ mong muốn.

```bash
//.env

ECCUBE_TIMEZONE=Pacific/Honolulu
```

Sau khi thiết lập biến môi trường, chỉ cần reload trang là múi giờ sẽ được chuyển đổi.
Không cần xoá cache.