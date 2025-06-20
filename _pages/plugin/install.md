---
title: Cài đặt Plugin
keywords: plugin cài đặt plugin
tags: [quickstart, getting_started]
permalink: plugin_install

---

### Tổng quan về thao tác plugin

- Sau khi cài đặt plugin, cần kích hoạt để sử dụng chức năng.  
- Nếu muốn tạm thời không sử dụng, có thể chuyển đổi giữa bật/tắt plugin.
- Nếu không cần nữa, có thể xóa plugin.

### Cài đặt từ màn hình quản trị

Có thể cài plugin từ quản trị bằng các cách sau:

- Cài plugin đã mua từ Owners Store
- Cài plugin tự phát triển (tar.gz/zip) bằng cách upload

### Cài đặt bằng dòng lệnh

Sau khi giải nén plugin mẫu (ProductReview) vào `./app/Plugin/ProductReview`, hãy chạy lệnh sau.

1. Cài đặt  
`bin/console eccube:plugin:install --code=ProductReview`
1. Kích hoạt  
`bin/console eccube:plugin:enable --code=ProductReview`

#### Các thao tác khác

Có thể thao tác plugin bằng các lệnh sau trên dòng lệnh.  
Nhờ đó có thể quản lý plugin bằng command.

```
bin/console eccube:plugin:install            // Cài đặt
bin/console eccube:plugin:uninstall          // Xóa
bin/console eccube:plugin:enable             // Kích hoạt
bin/console eccube:plugin:disable            // Vô hiệu hóa
```

##### Ví dụ sử dụng

1. Cài đặt  
`bin/console eccube:plugin:install --code=<mã plugin>`
1. Kích hoạt  
`bin/console eccube:plugin:enable --code=<mã plugin>`
1. Vô hiệu hóa  
`bin/console eccube:plugin:disable --code=<mã plugin>`
1. Xóa  
`bin/console eccube:plugin:uninstall --code=<mã plugin>`
1. Xóa cả file plugin  
`bin/console eccube:plugin:uninstall --code=<mã plugin> --uninstall-force=true`
