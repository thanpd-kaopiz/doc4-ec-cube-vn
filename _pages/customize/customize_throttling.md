---
layout: single
title: Tuỳ biến chức năng throttling
keywords: core tuỳ biến throttling
tags: [core, throttling]
permalink: customize_throttling
folder: customize
---

---

## Chức năng throttling

※Chức năng này có từ EC-CUBE 4.2.1.

- [EC-CUBE/ec-cube#5881](https://github.com/EC-CUBE/ec-cube/pull/5881)
- [EC-CUBE/ec-cube#5942](https://github.com/EC-CUBE/ec-cube/pull/5942)
 
Chức năng throttling được thêm vào để hạn chế truy cập, ví dụ như chống brute force vào credit master.

Có thể throttling theo IP hoặc theo hội viên.

Các chức năng, số lần thử... được áp dụng mặc định như sau:

| Màn hình | Routing | Theo IP | Theo hội viên | Ghi chú |
|---|---|---|---|---|
| Đăng ký hội viên | entry | 25 lần/30 phút | - | Khi chuyển từ màn hình nhập sang xác nhận |
| Đăng ký hội viên (hoàn tất) | entry | 5 lần/30 phút | - | Khi hoàn tất đăng ký hội viên |
| Quên mật khẩu | forgot | 5 lần/30 phút | - |  |
| Liên hệ | contact | 5 lần/30 phút | - |  |
| Xác nhận đơn hàng | shopping_confirm | 25 lần/30 phút | 10 lần/30 phút | Thực hiện trước khi chuyển sang xử lý thanh toán |
| Hoàn tất đơn hàng | shopping_checkout | 25 lần/30 phút | 10 lần/30 phút | Thực hiện trước khi chuyển sang xử lý thanh toán |
| Sửa thông tin hội viên | mypage_change | - | 10 lần/30 phút | Chỉ áp dụng cho hội viên đã đăng nhập |
| Thêm địa chỉ giao hàng | mypage_delivery_new | - | 10 lần/30 phút | Chỉ áp dụng cho hội viên đã đăng nhập |
| Sửa địa chỉ giao hàng | mypage_delivery_edit | - | 10 lần/30 phút | Chỉ áp dụng cho hội viên đã đăng nhập |
| Xoá địa chỉ giao hàng | mypage_delivery_delete | - | 10 lần/30 phút | Chỉ áp dụng cho hội viên đã đăng nhập |
| Sửa nhiều địa chỉ giao hàng | shopping_shipping_multiple_edit | - | 10 lần/30 phút | Chỉ áp dụng cho hội viên đã đăng nhập |
| Sửa địa chỉ giao hàng trong giỏ | shopping_shipping_edit | - | 10 lần/30 phút | Chỉ áp dụng cho hội viên đã đăng nhập |
| Đăng nhập quản trị (2FA) | admin_two_factor_auth | - | 5 lần/30 phút | Chỉ áp dụng cho quản trị viên đã đăng nhập |

Bạn cũng có thể sử dụng chức năng này trong Plugin hoặc Customize.

## Ví dụ mở rộng

### Cấu hình bằng yaml

Cấu hình như sau để tự động throttling theo routing.

Có thể chỉ định kiểm soát theo IP hoặc hội viên (hoặc quản trị viên).

File yaml:

- Customize: app/Customize/Resource/config/services.yaml
- Plugin: app/Plugin/[Plugin Code]/Resource/config/services.yaml
  
```yaml
eccube:
    rate_limiter:
        forgot:
            route: forgot # Routing cần throttling
            method: ['POST'] # Phương thức cần throttling, mặc định là POST
            type: ip # Kiểm soát theo ip, user. Có thể chỉ định nhiều (từ 4.2.3 dùng user thay cho customer)
            limit: 5
            interval: '30 minutes'
        entry:
            route: entry
            method: ['POST']
            params:
                mode: complete # Nếu có bước xác nhận, chỉ định param
            type: [ 'ip', 'user' ]
            limit: 5
            interval: '30 minutes'
        shopping_confirm_ip:
            route: ~ # Nếu route là null thì không tự động thực thi
            limit: 25
            interval: '30 minutes'
```

### Tự triển khai throttling riêng

Chỉ định route là null để chỉ tạo RateLimiter, không tự động thực thi.

```yaml
eccube:
    rate_limiter:
        hoge:
            route: ~ 
            limit: 25
            interval: '30 minutes'
```

Inject RateLimiterFactory vào controller để sử dụng:

```php
class HogeController {

  public function index(RateLimiterFactory $hogeLimiter, Request $request) {
    $limiter = $hogeLimiter->create($request->getClientIp());
    if (!$limiter->consume()->isAccepted()) {
        throw new TooManyRequestsHttpException();
    }
  }

```

### Ghi đè cấu hình mặc định

Có thể ghi đè cấu hình mặc định của core hoặc plugin bằng Customize.

Ví dụ, core có cấu hình:

```yaml
eccube:
 rate_limiter:
  forgot:
   route: forgot
   method: ['POST']
   type: ip
   limit: 5
   interval: '30 minutes'
```

Customize ghi đè như sau:

```yaml
eccube:
 rate_limiter:
  forgot:
   limit: 10
   interval: '60 minutes'
```

### Xoá cache throttling

Xoá cache bằng lệnh:

```
bin/console cache:pool:clear rate_limiter.cache --env=<APP_ENV> 
```

### Thay đổi nơi lưu thông tin throttling

Mặc định lưu bằng file system.

Có thể thay đổi tại app/config/eccube/packages/rate_limiter.yml.

```
# config/packages/rate_limiter.yaml
framework:
    cache:
        pools:
            rate_limiter.cache:
                adapter: cache.adapter.filesystem
```

Tham khảo: [https://symfony.com/doc/5.4/cache.html](https://symfony.com/doc/5.4/cache.html)

{: .notice--danger}
Hiện tại, [EC-CUBE/ec-cube#5957](https://github.com/EC-CUBE/ec-cube/issues/5957) có bug, không thể dùng cache.adapter.doctrine_dbal. Nếu cần HA, hãy dùng redis hoặc memcached.
{: .notice--danger}

### Throttling đăng nhập

Tham khảo thêm:

- [EC-CUBE/ec-cube#4249](https://github.com/EC-CUBE/ec-cube/issues/4249)
- [EC-CUBE/ec-cube#5473](https://github.com/EC-CUBE/ec-cube/pull/5473)
- [EC-CUBE/ec-cube#6035](https://github.com/EC-CUBE/ec-cube/pull/6035)
- [EC-CUBE/ec-cube#6038](https://github.com/EC-CUBE/ec-cube/pull/6038)

## Tham khảo

Chức năng throttling sử dụng symfony/rate-limiter. Tham khảo thêm tại tài liệu Symfony:

[Rate Limiter](https://symfony.com/doc/5.4/rate_limiter.html){:target="_blank"}
