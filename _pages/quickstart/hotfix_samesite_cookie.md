---
layout: single
title: Hỗ trợ SameSite Cookie
keywords: samesite
tags: [quickstart, getting_started]
permalink: hotfix_samesite_cookie
summary : Hướng dẫn xử lý tạm thời SameSite Cookie trên EC-CUBE4
---

Ngày 17/06/2020, EC-CUBE 4.0.4 đã hỗ trợ tiêu chuẩn mới về SameSite Cookie, do đó trang này đã được cập nhật.

## Tổng quan

Từ ngày 14/07/2020, trên Chrome 80 trở lên, khi chuyển từ website khác sang site EC-CUBE, trong một số trường hợp cookie sẽ không được gửi đi, dẫn đến lỗi không hoàn tất thanh toán, v.v.
EC-CUBE 4.0.4 đã hỗ trợ tiêu chuẩn này, vì vậy nếu bạn đang sử dụng EC-CUBE 4.0.3 trở xuống, hãy cập nhật lên phiên bản mới.
Nếu đã áp dụng hot-fix, bạn cũng nên cập nhật lên EC-CUBE 4.0.4 để đảm bảo an toàn, đồng thời chú ý không để lại file không cần thiết khi update.

### Thông tin liên quan
- [Google Developers Japan: Chuẩn bị cho thiết lập Cookie mới SameSite=None; Secure](https://developers-jp.googleblog.com/2019/11/cookie-samesitenone-secure.html)
- [SameSite Updates - The Chromium Projects](https://www.chromium.org/updates/same-site)
- [Chrome80 ảnh hưởng SameSite gây lỗi thanh toán khi dùng 3D Secure, v.v. #4457](https://github.com/EC-CUBE/ec-cube/issues/4457)

## Cách hoàn tác hot-fix thủ công

1.  Hoàn tác thay đổi sau trong `app/config/eccube/packages/framework.yaml`
    - [Xem diff commit](https://github.com/EC-CUBE/ec-cube/commit/93c120dbd4dc34f6d9883b6336fb3c31f013ae54)
1. Xóa 2 file sau:
    - [src/Eccube/EventListener/SameSiteCookieHotfixListener.php](https://raw.githubusercontent.com/kiy0taka/ec-cube/2ef44a5e5e0741abfd2f04a259a05b315bd07808/src/Eccube/EventListener/SameSiteCookieHotfixListener.php)
    - [src/Eccube/Resource/template/default/error_samesite.twig](https://raw.githubusercontent.com/kiy0taka/ec-cube/2ef44a5e5e0741abfd2f04a259a05b315bd07808/src/Eccube/Resource/template/default/error_samesite.twig)
1. Xóa cache bằng một trong các cách sau:
    - Xóa cache bằng lệnh:
        ```
        $ bin/console cache:clear --no-warmup
        ```
    - Hoặc vào trang quản trị → Quản lý nội dung → Quản lý cache và nhấn "Xóa cache"
