---
title: Tips
keywords: Tips tips vướng mắc khó khăn
tags: [tips]
permalink: reverse-lookup/tips
folder: reverse-lookup
---

---

Tại đây tổng hợp các tips hữu ích khi gặp khó khăn trong quá trình phát triển.

## Thủ thuật phát triển

### Muốn debug khi phát triển

Bật chế độ debug sẽ rất tiện lợi.

[Chế độ debug](/debug_mode)

### Muốn kiểm tra nội dung object khi phát triển

Bật debug mode và chèn hàm dump vào source, có thể kiểm tra từ thanh công cụ Symfony.

```
// Chèn vào source
 dump([instance object muốn kiểm tra]);
```

![Debug mode với dump](/doc4-ec-cube-vn/images/reverse-lookup/dump.png)

### Gặp lỗi trắng trang!

Có thể do nhiều nguyên nhân (core, server, ...), trước tiên hãy kiểm tra log của core.

```
[Thư mục gốc EC-CUBE]/var/log
```

### Muốn kiểm tra nội dung email gửi đi khi phát triển

Dùng MailCatcher rất tiện.

[MailCatcher](/development-tools/mail-catcher)

## Liên quan DB

### Muốn thêm cột vào bảng

Sau khi sửa Entity, hãy chạy lệnh update schema sau.

```
$ cd {đường dẫn EC-CUBE}
$ bin/console doctrine:schema:update --force --dump-sql
```

### Đã chạy lệnh update schema nhưng bảng chưa thay đổi

Có thể cache của Doctrine còn sót lại. Hãy xoá cache bằng lệnh sau.

```
$ cd {đường dẫn EC-CUBE}
$ rm -rf var/cache
```

### Dữ liệu ngày giờ trong bảng bị lệch?

Hãy đọc tài liệu về cấu hình timezone của core và DB.

[Timezone](/i18n_timezone)

### Muốn thêm dữ liệu vào bảng khi cài mới hoặc nâng cấp core?

#### Khi nâng cấp core

Cần thêm file migration.  
File migration cũng sẽ chạy khi cài mới, nên cần tránh trùng dữ liệu.

![Bảng migration_versions](/doc4-ec-cube-vn/images/reverse-lookup/migration_versions.png)

File migration được quản lý trong bảng migration_versions.  
Cột version sẽ lưu tên file migration (phần ngày giờ).

[Ví dụ file migration](https://github.com/EC-CUBE/ec-cube/blob/4.0/app/DoctrineMigrations/Version20201218044542.php){:target="_blank"}

#### Khi cài mới core

Cần thêm record vào file csv.

[Import CSV](https://github.com/EC-CUBE/ec-cube/tree/4.0/src/Eccube/Resource/doctrine/import_csv){:target="_blank"}
