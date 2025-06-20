---
title: Cách xử lý sự cố plugin
keywords: plugin lỗi sự cố lỗi plugin sự cố plugin
tags: [quickstart, getting_started]
permalink: plugin_error
---

---

## Khi nào xảy ra lỗi?

- Ngay sau khi cài plugin thì xuất hiện lỗi, không thể truy cập front hoặc quản trị
- Khi kích hoạt plugin thì xuất hiện lỗi, không thể truy cập front hoặc quản trị
- Cài đặt/cập nhật/kích hoạt plugin thành công nhưng hiển thị bị lỗi

Trang này sẽ hướng dẫn cách giải quyết các sự cố trên.

### Cài đặt khi ở chế độ bảo trì

Khi cài plugin, nên chuyển sang chế độ bảo trì để tránh lỗi cache.
Vào quản trị EC-CUBE → Quản lý nội dung → Quản lý bảo trì để bật chế độ bảo trì trước khi cài plugin.

## Nếu gặp lỗi khi cài/kích hoạt plugin, không thể truy cập site
  
Hãy kiểm tra các mục sau.

- Nếu là môi trường ec-cube.co -> Liên hệ [bộ phận hỗ trợ EC-CUBE](https://www.ec-cube.net/product/co/support.php){:target="_blank"}
- Nếu không thể thao tác trên server (ssh, v.v.) -> Xem [FAQ - Lỗi sau khi cài module/plugin](https://support.ec-cube.net/hc/ja/articles/360038542232){:target="_blank"}
- Nếu không thuộc các trường hợp trên, hãy đọc tiếp các hướng dẫn bên dưới.

### Cache bị lỗi do quá trình cài đặt bị gián đoạn

Nguyên nhân phổ biến nhất là cache bị lỗi do quá trình cài đặt bị dừng giữa chừng.
Hãy xóa cache theo hướng dẫn bên dưới rồi thử cài lại.

[Xóa cache bằng lệnh](#Xóa-cache-bằng-lệnh)  
[Xóa cache bằng cách xóa thư mục](#Xóa-cache-bằng-cách-xóa-thư-mục)

### Khi thêm menu quản trị, chỉ file Nav được kích hoạt
 
Nếu plugin thêm menu quản trị, đôi khi chỉ file Nav `/ec-cube/app/config/eccube/packages/eccube_nav.yaml` được kích hoạt mà routing không được kích hoạt.
  
Hãy thử các bước sau:

1. Backup file Nav về local.
1. Xóa file Nav trên server.
1. Đăng nhập lại quản trị sẽ được.
1. Vào quản trị, tạm thời vô hiệu hóa plugin.
1. Đưa lại file Nav đã backup vào đúng thư mục trên server.
1. Nếu kích hoạt lại plugin từ quản trị có thể lại bị lỗi, nên nếu có thể hãy [kích hoạt plugin bằng lệnh](/plugin_install#%E3%81%9D%E3%81%AE%E4%BB%96%E3%81%AE%E6%93%8D%E4%BD%9C){:target="_blank"}.

### Plugin bị xung đột

Nếu cài nhiều plugin và bị xung đột, hãy liên hệ tác giả plugin.
Khi liên hệ, nên chuẩn bị log lỗi, cách tái hiện để trao đổi dễ dàng hơn.

[Xem FAQ - Lấy log](https://support.ec-cube.net/hc/ja/search?utf8=%E2%9C%93&query=%E3%83%AD%E3%82%B0){:target="_blank"}

### Nếu các cách trên không giải quyết được

Tham khảo thêm các bài viết chi tiết của evangelist EC-CUBE ông Okouchi:

- [Cách xử lý lỗi khi cài plugin trên EC-CUBE4](https://qiita.com/nanasess/items/583683eb94947aebea44){:target="_blank"}
- [Nguyên nhân và cách phòng tránh lỗi plugin trên EC-CUBE4](https://qiita.com/nanasess/items/791c9ec98f69ada93ea0){:target="_blank"}

## Kích hoạt nhưng hiển thị bị lỗi

Có thể gặp các trường hợp sau.  
Ngoài ra, lỗi hiển thị có thể xảy ra cả khi cập nhật plugin.

- Kích hoạt thành công nhưng menu hoặc icon plugin không hiển thị ở quản trị
- Kích hoạt thành công nhưng hiển thị bị lỗi, tiếng Anh hoặc lỗi font

### Kích hoạt nhưng menu hoặc icon plugin không hiển thị

Hãy thử vô hiệu hóa rồi kích hoạt lại plugin.

### Kích hoạt nhưng hiển thị bị lỗi, tiếng Anh hoặc lỗi font

Hãy thử xóa cache từ quản trị.

[Xóa cache từ quản trị](#Xóa-cache-từ-quản-trị)

### Nếu vẫn không giải quyết được

Hãy liên hệ tác giả plugin.

---
---

## Phụ lục: Cách xóa cache

### Xóa cache từ quản trị

Nếu đăng nhập được quản trị, vào [Quản lý nội dung] > [Quản lý cache] để xóa cache.

### Xóa cache bằng lệnh

Nếu không vào được quản trị, hãy xóa cache bằng lệnh qua SSH.  
Cần SSH vào server EC-CUBE.

Sau khi SSH, chuyển vào thư mục EC-CUBE.
```shell
## Ghi đúng đường dẫn EC-CUBE vào path/to/eccube_root
cd path/to/eccube_root/
```

Chạy lệnh xóa và tạo lại cache
```shell
## Xóa và tạo lại cache bằng lệnh Symfony
bin/console cache:clear --no-warmup
bin/console cache:warmup
```

Nếu lệnh xóa cache không thành công, hãy xóa mạnh tay:
```shell
## Ghi đúng đường dẫn EC-CUBE vào path/to/eccube_root
rm -rf path/to/eccube_root/var/cache/*
```

### Xóa cache bằng cách xóa thư mục

Nếu xóa cache bằng lệnh không được, hãy xóa trực tiếp thư mục cache qua FTP.

1. Kết nối FTP
1. Xóa thư mục dưới `var/cache/` trong thư mục EC-CUBE
