---
title: Hướng dẫn cấu hình môi trường
permalink: /penetration-testing/testing/settings
---
## Yêu cầu hệ thống

- Docker 1.13.0 trở lên
- docker-compose 1.10.0 trở lên

- Chrome (phiên bản mới nhất) - Dùng để thao tác giao diện quản lý OWASP ZAP
- Firefox (phiên bản mới nhất) - Dùng để thăm dò thủ công qua Local Proxes

## Cài đặt

Tham khảo [Quick Start](/penetration-testing/quick_start)

**Lưu ý:** Sẽ bổ sung chi tiết sau
{: .notice}

### Nội dung được tự động thiết lập bởi docker-compose.owaspzap.yml

#### Thư mục mount VOLUME

```shell
<ec-cube-thư-mục-cài-đặt>/ec-cube/zap:/zap/wrk
```

Nếu thiết lập lưu session, report, ... vào `/zap/wrk` thì có thể dễ dàng lấy ra từ môi trường local.

#### Addon được cài đặt

- [help_ja_JP](https://www.zaproxy.org/addons/#addon-help_ja_JP) - Trợ giúp tiếng Nhật
- [wappalyzer](https://www.zaproxy.org/docs/desktop/addons/technology-detection/) - Phát hiện công nghệ sử dụng
- [sequence](https://www.zaproxy.org/docs/desktop/addons/sequence-scanner/) - Addon cho kiểm thử chuyển trang nhiều màn hình

#### Addon bị gỡ bỏ

- [hud](https://www.zaproxy.org/docs/desktop/addons/hud/) - Head Up Display. Không sử dụng vì gây xung đột với các công cụ thao tác trình duyệt như Selenium

#### Các tuỳ chọn được thiết lập tự động

- Ngôn ngữ tiếng Nhật
- Vô hiệu hoá API key
  - Để tăng tiện lợi trong môi trường đóng
- Token Anti-CSRF (thử nghiệm)
- Token HttpSession
- Global Alert Filter (thử nghiệm)
  - Đăng ký các cảnh báo luôn bị false positive

#### Khác

- Tự động xuất chứng chỉ gốc SSL cho Local Proxes
  - Được xuất ra `<ec-cube-thư-mục-cài-đặt>/zap/owasp_zap_root_ca.cer` trên môi trường local
  - Đọc vào Firefox qua Certificate Manager để sử dụng
