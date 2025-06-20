---
title: Đối tượng kiểm thử
permalink: /penetration-testing/planning/target
---
Kiểm thử này tập trung vào phạm vi phụ thuộc vào ứng dụng (EC-CUBE).

## Đối tượng kiểm thử

- Phạm vi phụ thuộc vào ứng dụng (EC-CUBE)
- Trong các mục kiểm tra của bản phát hành OWASP ZAP, các mục sau là đối tượng:
  - CSRF
  - XSS
  - Tham số/Parameter Tampering
  - OS Command Injection
  - Server Side Code Injection
  - SQL Injection
  - Format String Error
  - External Redirect
  - Path Traversal
  - Remote File Inclusion

## Ngoài phạm vi kiểm thử

**Lưu ý:** Một số kiểm thử không áp dụng cho đợt phát hành EC-CUBE, nhưng nên thực hiện khi vận hành thực tế. Hãy cân nhắc tuỳ theo chính sách của từng dự án.
{: .notice--info}

- Lộ thông tin thư mục
- Server Side Include
- Buffer Overflow
- Tấn công lỗ hổng của Web server, middleware, PHP
- Cấu hình sai của Web server, middleware, PHP
- DoS
- Tấn công tổng hợp như password

## Những gì không thể kiểm thử bằng OWASP ZAP

- Kiểm thử về quyền xác thực
- Kiểm thử về cấu hình sai của EC-CUBE


