---
title: ec-cube.co Về các biện pháp bảo mật
keywords: co ec-cube.co Cloud version Biện pháp bảo mật
tags: [co, ec-cube.co]
permalink: co/co_security
folder: co
---

---

Về các biện pháp bảo mật của ec-cube.co, dựa trên [Chính sách bảo mật thông tin](https://www.ec-cube.net/policy/securitypolicy.php){:target="_blank"}, chúng tôi thực hiện các biện pháp sau. Về điều khoản sử dụng, vui lòng tham khảo [Điều khoản sử dụng ec-cube.co](https://www.ec-cube.co/pdf/term.pdf){:target="_blank"}.

## Biện pháp bảo mật ứng dụng

### Giám sát & Monitoring

Chúng tôi thực hiện các biện pháp giám sát sau:
- Giám sát hoạt động (kiểm tra site có hoạt động không)
- Giám sát lỗi (kiểm tra ứng dụng hoạt động bình thường không)
- Giám sát tài nguyên (bộ nhớ, CPU, ...)

### Khi phát sinh sự cố

Khi phát hiện sự cố nghiêm trọng như không thể truy cập site, quản trị viên hệ thống sẽ được thông báo và tiến hành xử lý.

### Backup

Thực hiện backup định kỳ file ứng dụng và DB dump.

### Bảo trì định kỳ

- Bảo trì hàng tuần: cập nhật mã nguồn EC-CUBE mà không dừng dịch vụ.
- Bảo trì hàng tháng: có thể dừng dịch vụ để cập nhật hạ tầng, middleware, ...
- Bảo trì khẩn cấp: thực hiện khi có sự cố hoặc khi EC-CUBE đánh giá cần thiết.

## Biện pháp bảo mật mạng

### Chống truy cập trái phép, tấn công, phá hoại

Sử dụng WAF để phát hiện tấn công vào ứng dụng web, chặn truy cập từ kẻ tấn công và bảo vệ site.

## Biện pháp cho phát triển

### Xử lý thông tin cá nhân
Tham khảo [Chính sách bảo vệ thông tin cá nhân](https://www.ec-cube.net/policy/privacy.php){:target="_blank"} và [Về xử lý thông tin cá nhân](https://www.ec-cube.net/policy/){:target="_blank"}.

### Thiết bị phát triển/vận hành

Áp dụng phần mềm bảo mật cho thiết bị phát triển/vận hành, luôn cập nhật mới nhất và thực hiện quét virus định kỳ.

## Biện pháp để sử dụng an toàn

### Mã hoá truyền dữ liệu

Sử dụng SSL để mã hoá truyền dữ liệu, ngăn chặn nghe lén và sửa đổi dữ liệu.

### Kiểm soát truy cập

Có thể giới hạn IP truy cập vào màn hình quản trị.

### Thông tin thanh toán

Các plugin thanh toán cung cấp trên [Owner's Store](https://www.ec-cube.net/owners/){:target="_blank"} đều hỗ trợ không lưu trữ thông tin thẻ tín dụng.
