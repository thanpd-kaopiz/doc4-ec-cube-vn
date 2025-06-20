---
title: Phân loại Context
permalink: /penetration-testing/testing/context
---
OWASP ZAP có chức năng đăng nhập tự động để kiểm thử các trang cần đăng nhập, cho phép thiết lập pattern xác thực cho từng context.
Vì vậy, context được chia thành 3 loại tùy theo cách sử dụng HTTP Session:

- Màn hình quản trị
- Front (khách vãng lai)
- Front (đã đăng nhập)

**Lưu ý:** *Nếu sử dụng đồng thời nhiều context này, session có thể bị xung đột và không thể đăng nhập, hãy chú ý!*
{: .notice--warning}

Với từng context, có thể thiết lập các mục sau:

- Thiết lập URL kiểm thử
- Thiết lập URL loại trừ khỏi kiểm thử
- Thiết lập ký tự nối query string, POST (&, =, ...)
- Thiết lập OS, middleware đang sử dụng
- Thiết lập pattern xác thực
- Thiết lập user xác thực
- Thiết lập cách quản lý HTTP Session
- Thiết lập alert filter

Tùy theo loại context, đã chuẩn bị sẵn file cấu hình, hãy import và sử dụng phù hợp.

```shell
## Dành cho màn hình quản trị
docker-compose -f docker-compose.yml -f docker-compose.owaspzap.yml exec zap zap-cli -p 8090 context import /zap/wrk/admin.context
## Dành cho front (đã đăng nhập)
docker-compose -f docker-compose.yml -f docker-compose.owaspzap.yml exec zap zap-cli -p 8090 context import /zap/wrk/front_login.context
## Dành cho front (khách vãng lai)
docker-compose -f docker-compose.yml -f docker-compose.owaspzap.yml exec zap zap-cli -p 8090 context import /zap/wrk/front_guest.context
```

Hãy thực hiện kiểm thử cho từng context và đánh giá báo cáo kết quả kiểm thử tương ứng.

**Lưu ý:** Nếu lưu session của OWASP ZAP riêng cho từng context sẽ rất tiện lợi.
{: .notice--info}
