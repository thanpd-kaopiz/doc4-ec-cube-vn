---
layout: single
title: Cài đặt quyền
keywords: quyền
permalink: quickstart/permission
folder: quickstart
description: Về cài đặt quyền
---

## Về cài đặt quyền (Điểm chung)

Một số tính năng tiện lợi của EC-CUBE dựa trên việc máy chủ web có thể ghi vào tệp. Tuy nhiên, việc ứng dụng có quyền ghi vào tệp là nguy hiểm. Từ góc độ bảo mật, tốt nhất là hạn chế quyền càng nhiều càng tốt và chỉ cấp quyền ghi cho các thư mục/tệp cụ thể. Các cài đặt quyền dưới đây là chung cho mọi phương pháp cài đặt.

### Quyền ghi của máy chủ web

Để sử dụng tất cả các tính năng của EC-CUBE, cần có quyền ghi từ máy chủ web cho các thư mục/tệp sau.

```
[eccube_root/]
  │
  ├──[app/]
  │   ├──[Plugin/]
  │   ├──[PluginData/]
  │   ├──[proxy/]
  │   └──[template/]
  ├──[html/]
  ├──[var/]
  ├──[vendor/]
  ├──[composer.json]
  └──[composer.lock]
```

Các thư mục/tệp khác cần có quyền đọc.

#### eccube_root/

Cần có quyền ghi từ máy chủ web cho thư mục gốc của EC-CUBE. Dưới thư mục gốc có các tệp như `.env` và `.maintenance`. **Có các quyền khuyến nghị khác cho thư mục gốc, vì vậy hãy cẩn thận không thay đổi quyền một cách toàn diện.**

#### app/

Cần có quyền ghi từ máy chủ web cho thư mục này. Vì cần có quyền ghi từ máy chủ web cho các thư mục con.

#### app/Plugin/

Cần có quyền ghi từ máy chủ web cho thư mục này. Mã nguồn của plugin được đặt ở đây.

#### app/PluginData/

Cần có quyền ghi từ máy chủ web cho thư mục này. Dữ liệu của plugin được đặt ở đây.

#### app/proxy/

Cần có quyền ghi từ máy chủ web cho thư mục này. Các tệp proxy được tạo ra khi mở rộng Entity được đặt ở đây.

#### app/template/

Cần có quyền ghi từ máy chủ web cho thư mục này. Các tệp mẫu được đặt ở đây.

#### html/

Cần có quyền ghi từ máy chủ web cho thư mục này. Các tệp css và js được đặt ở đây.

#### var/

Cần có quyền ghi từ máy chủ web cho thư mục này. Các tệp tạm thời như cache và log được đặt ở đây.

#### vendor/

Cần có quyền ghi từ máy chủ web cho thư mục này. Các thư viện được cài đặt khi cài đặt plugin và bản đồ lớp được cập nhật.

#### composer.json / composer.lock

Cần có quyền ghi từ máy chủ web cho các tệp này. Được cập nhật khi cài đặt plugin.

#### Ví dụ cài đặt quyền

Quyền cần thiết cho các vai trò khác nhau tùy thuộc vào thông số kỹ thuật của máy chủ. Ví dụ, trong trường hợp máy chủ chia sẻ, người dùng FTP đặt tệp và người dùng thực thi máy chủ web có thể khác nhau. Trong trường hợp này, máy chủ web sẽ truy cập với quyền Other, vì vậy cần thiết lập quyền ghi cho Other để sử dụng các tính năng của EC-CUBE.

| Thư mục/Tệp | Quyền cần thiết cho máy chủ web | Ví dụ cài đặt |
|--------------------|----------|-------|
| eccube_root/ <br> app/ <br>  app/Plugin/ <br>  app/PluginData/ <br>  app/proxy/ <br>  app/template/ <br>  html/ <br>  var/ <br> vendor/ | Đọc, ghi | 707( `rwx---rwx` ) |
| Các thư mục khác | Đọc | 705( `rwx---r-x` ) |
| composer.json <br> composer.lock | Đọc, ghi | 606( `rw----rw-` ) |
| Các tệp khác | Đọc | 604( `rw----r--` ) |

#### Về việc nâng cấp phiên bản chính

Khi nâng cấp phiên bản chính của EC-CUBE bằng plugin cập nhật, cần có quyền ghi từ máy chủ web cho tất cả các tệp. Khi nâng cấp, hãy tạm thời cấp quyền ghi từ máy chủ web, sau khi cập nhật hãy trở lại cài đặt quyền khuyến nghị.

#### Về bin/console

Khi sử dụng lệnh của EC-CUBE, hãy cấp quyền thực thi cho `bin/console`.

### Cài đặt quyền trong môi trường sản xuất

Phần trước đã đề cập đến quyền ghi từ máy chủ web để sử dụng tất cả các tính năng của EC-CUBE. Trong môi trường sản xuất, có thể giảm rủi ro bảo mật bằng cách hạn chế quyền hơn nữa. Tuy nhiên, việc hạn chế quyền quá mức có thể làm giảm tính tiện lợi và hạn chế một số tính năng. Hãy hiểu rõ vai trò và nội dung hạn chế của từng tệp/thư mục trước khi cài đặt quyền.

Không nên cấp quyền ghi từ máy chủ web cho các thư mục/tệp sau từ góc độ bảo mật.

```
[eccube_root/]
  │
  ├──[app/]
  │   ├──[Plugin/]
  │   ├──[proxy/]
  │   └──[template/]
  ├──[vendor/]
  ├──[.env]
  ├──[.htaccess]
  ├──[composer.json]
  └──[composer.lock]
```

Khi hạn chế quyền ghi từ máy chủ web cho các thư mục/tệp trên, các tính năng sau sẽ bị hạn chế.

- Quản lý nội dung
  - Quản lý trang
  - Quản lý khối
  - Quản lý bảo trì
- Cài đặt
  - Cài đặt cửa hàng
    - Cài đặt luật thương mại cụ thể
    - Cài đặt điều khoản sử dụng
    - Cài đặt email
  - Cài đặt hệ thống
    - Quản lý bảo mật
- Cửa hàng chủ sở hữu
  - Plugin
    - Danh sách plugin
  - Mẫu
    - Danh sách mẫu
    - Tải lên
  - Cài đặt

#### .env và .htaccess

`.env` được tạo khi cài đặt EC-CUBE và chứa các cài đặt quan trọng của EC-CUBE. Ngoài ra, `.htaccess` chứa các cài đặt quan trọng như cài đặt máy chủ web và biến môi trường. Vì cả hai đều chứa các cài đặt quan trọng, nên hạn chế chỉ cho phép quyền đọc và ghi từ máy chủ web. Hãy đặt chủ sở hữu tệp là người dùng máy chủ web và thiết lập quyền `400(rw-------)`. Về việc sử dụng tệp `.env` trong môi trường sản xuất, hãy xem thêm [Về việc sử dụng tệp .env trong môi trường sản xuất](/quickstart/dotenv).

#### var/

Các tệp cần thiết cho hoạt động của EC-CUBE như cache và log được đặt ở đây. Để EC-CUBE hoạt động, cần có quyền ghi từ máy chủ web.

#### app/PluginData/

Thư mục này dùng để đặt dữ liệu của plugin. Việc sử dụng `app/PluginData/` phụ thuộc vào plugin. Nếu có plugin sử dụng `app/PluginData/` được cài đặt, cần có quyền ghi từ máy chủ web.

#### html/

Khi tải lên các hình ảnh sản phẩm, chúng được đặt trong `html/`. Khi hạn chế quyền ghi từ máy chủ web, các tính năng sau sẽ bị hạn chế.

- Quản lý sản phẩm
  - Đăng ký sản phẩm
    - Hình ảnh sản phẩm
- Quản lý nội dung
  - Quản lý tệp
- Cài đặt
  - Cài đặt cửa hàng
    - Cài đặt phương thức thanh toán
      - Hình ảnh logo