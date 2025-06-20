---
title: Sử dụng CSS
keywords: thiết kế 
tags: [thiết kế]
permalink: design_css

summary: Cách chỉnh sửa CSS
---

## Về việc sử dụng CSS

Trong EC-CUBE, có hai cách để chỉnh sửa CSS:

1. [Chỉnh sửa từ Quản lý CSS trong trang quản trị](#chỉnh-sửa-từ-quản-lý-css-trong-trang-quản-trị)
2. [Chỉnh sửa trực tiếp file style.css](#chỉnh-sửa-trực-tiếp-file-style.css)

Một số CSS như slide của hình ảnh chính trên trang chủ được viết trực tiếp trong file twig.<br>
Bạn có thể chỉnh sửa tại [Quản lý nội dung] -> [Quản lý trang] -> Trang TOP trong trang quản trị EC-CUBE.


## Chỉnh sửa từ Quản lý CSS trong trang quản trị

Từ [Quản lý nội dung] -> [Quản lý CSS] trong trang quản trị EC-CUBE, bạn có thể viết mã CSS.

- Mã bạn viết trong [Quản lý CSS] sẽ được phản ánh vào file customize.css trong thư mục sau:<br>

```
[html]
 └─ [user_data]
     └─ [assets]
         └─ [css]
             └─ customize.css
```
  
  CSS chỉnh sửa từ trang quản trị (customize.css) sẽ được ưu tiên hơn style.css.


## Chỉnh sửa trực tiếp file style.css

CSS của EC-CUBE được tập trung trong file style.css ở thư mục sau:<br>
Về mặt bảo trì CSS, bạn cũng nên cân nhắc sử dụng Sass như sẽ giới thiệu bên dưới.

- style.css được lưu tại thư mục sau:

```
[html]
 └─ [template]
     └─ [default]
            └─[assets]
                 ├─ [css]
                 │    ├─ style.css     # CSS được sử dụng
                 │    └─ style.min.css # CSS phiên bản rút gọn
                 └─ [sass]
                      ├─...
```


## Về Style Guide

EC-CUBE cung cấp 'Style Guide' để bạn có thể kiểm tra các nguyên tắc thiết kế và quy tắc code cho CSS và HTML.
Tham khảo thêm tại các link sau:

- [Style Guide cho giao diện người dùng](https://github.com/EC-CUBE/Eccube-Styleguide){:target="_blank"}
- [Style Guide cho trang quản trị](https://github.com/EC-CUBE/Eccube-Styleguide-Admin){:target="_blank"}
