---
title: Tiền tệ
keywords: currency
tags: [i18n, currency]
permalink: i18n_currency
folder: i18n

---

## Tổng quan

Mặc định, tiền tệ sẽ hiển thị là Yên Nhật.
Bạn có thể chỉ định ký hiệu/định dạng tiền tệ tuỳ ý bằng cách thiết lập biến môi trường.

## Cách chuyển đổi hiển thị tiền tệ

Bạn có thể chuyển đổi hiển thị tiền tệ bằng cách chỉ định locale/mã tiền tệ trong biến môi trường.

Tạo file `.env` ở thư mục gốc của EC-CUBE, thiết lập `ECCUBE_LOCALE` và `ECCUBE_CURRENCY` như sau:

```bash
//.env

ECCUBE_LOCALE=en
ECCUBE_CURRENCY=USD
```

Sau khi thiết lập biến môi trường, chỉ cần reload trang là tiền tệ sẽ được chuyển đổi.
Không cần xoá cache.

※ Chức năng này chỉ chuyển đổi ký hiệu/định dạng tiền tệ, không thực hiện quy đổi tỷ giá.

## PriceType

Đối với các trường nhập số tiền, EC-CUBE cung cấp `PriceType` mở rộng từ `MoneyType`.
`PriceType` sẽ tự động xác định scale dựa trên giá trị của `ECCUBE_CURRENCY`.

Ví dụ, nếu chọn JPY thì scale là 0.
Nếu chọn USD thì scale là 2, cho phép nhập đến 2 chữ số thập phân.
※ Nếu nhập quá scale, giá trị sẽ được làm tròn.

Dưới đây là ví dụ hiển thị khi thiết lập `ECCUBE_LOCALE: en`, `ECCUBE_CURRENCY: USD`:


![Form nhập tiền tệ](/images/i18n_currency/sample_scale.png)


## price filter

Khi hiển thị số tiền trên twig, bạn có thể sử dụng filter price.
Filter này sẽ tự động điều chỉnh ký hiệu và vị trí hiển thị tiền tệ.

Cách sử dụng như sau:

```
{{ 123|price }}
```

![Hiển thị tiền tệ](https://user-images.githubusercontent.com/8196725/28563890-5e370800-7162-11e7-9015-b2eab14ab726.png)


## Tham khảo

[Thêm chức năng chuyển đổi tiền tệ](https://github.com/EC-CUBE/ec-cube/pull/2431){:target="_blank"}