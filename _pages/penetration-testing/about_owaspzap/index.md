---
title: Giới thiệu về OWASP ZAP
permalink: /penetration-testing/about_owaspzap
---
**OWASP Zed Attack Proxy (ZAP)** là một công cụ kiểm tra bảo mật Web mã nguồn mở do dự án **O**pen **W**eb **A**pplication **S**ecurity **P**roject (OWASP) phát triển.
Công cụ này được phát triển sôi nổi bởi một nhóm tình nguyện viên quốc tế.

Official: [https://www.zaproxy.org](https://www.zaproxy.org){:target="_blank"}

## Quy trình kiểm thử với OWASP ZAP

Kiểm thử cơ bản được thực hiện theo các bước sau:

1. Dò quét - Sử dụng Local Proxies để duyệt qua tất cả các chức năng.
1. Spider - Sử dụng **Spider** để phát hiện các URL ẩn.
1. Forced Browse - Phát hiện các file hoặc thư mục không được tham chiếu.
1. Quét động - Phát hiện các lỗ hổng tiềm ẩn mà không thực hiện tấn công thực tế.
1. Kiểm thử thủ công - Để phát hiện nhiều lỗ hổng hơn, hãy sử dụng các chức năng khác nhau của OWASP ZAP để kiểm thử thủ công.

**Lưu ý:** Để biết chi tiết, vui lòng tham khảo hướng dẫn sử dụng trên trang trợ giúp của OWASP ZAP.
{: .notice--info}
