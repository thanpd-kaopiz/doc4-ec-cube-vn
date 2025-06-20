---
title: Cơ bản về template thiết kế
keywords: thiết kế template tìm kiếm
tags: [thiết kế]
permalink: design_template
summary: Giải thích về các quy tắc cơ bản của template thiết kế.
---

## Vị trí lưu file template mặc định

Giả sử thư mục cài đặt EC-CUBE là `ECCUBEROOT`.  
Các file Twig mặc định của hệ thống được lưu tại các thư mục sau:

- Thư mục mặc định cho giao diện người dùng (frontend)  
`ECCUBEROOT/src/Eccube/Resource/template/default`

- Thư mục mặc định cho trang quản trị  
`ECCUBEROOT/src/Eccube/Resource/template/admin`

- Thư mục mặc định cho trang cài đặt  
`ECCUBEROOT/src/Eccube/Resource/template/install`

## Vị trí lưu file khi tuỳ chỉnh thiết kế

Trong EC-CUBE, ngoài thư mục mặc định, bạn có thể lưu template thiết kế riêng của mình.  

Khi tạo thiết kế mới, không nên chỉnh sửa trực tiếp template mặc định vì có thể bị ghi đè khi nâng cấp phiên bản.  

- Thư mục mặc định khi lưu template thiết kế riêng  
`ECCUBEROOT/app/template/[template_code]`  
→ [template_code] là mã nhận diện template.  
Mặc định với frontend là "default", với admin là "admin".

Thư mục này sẽ được sử dụng khi áp dụng template thiết kế.  
Các file template thiết kế sẽ được lưu dưới thư mục này.  

Các file resource sẽ được lưu tại `ECCUBEROOT/html/template/[template_code]`.

## Thứ tự ưu tiên khi gọi template

Thứ tự gọi file template như sau:

- Frontend

```
1. ECCUBEROOT/app/template/[template_code]
2. ECCUBEROOT/src/Eccube/Resource/template/[template_code]
3. ECCUBEROOT/app/Plugin
```

- Admin

```
1. ECCUBEROOT/app/template/admin
2. ECCUBEROOT/src/Eccube/Resource/template/admin
3. ECCUBEROOT/app/Plugin
```

Sẽ kiểm tra xem có template tuỳ chỉnh không, nếu không có sẽ gọi template mặc định.


### Ví dụ gọi template

* Ví dụ frontend  
Nếu sử dụng template_code là "MyDesign" và trong Controller có định nghĩa `@Template("TemplateDir/template_name.twig")`

```
 1. app/template/MyDesign/TemplateDir/template_name.twig
 2. src/Eccube/Resource/template/default/TemplateDir/template_name.twig
 3. app/Plugin/[plugin_code]/Resource/template/TemplateDir/template_name.twig
```
Sẽ hiển thị theo thứ tự trên.

* Ví dụ admin  
Nếu sử dụng `@Template("@admin/Product/index.twig")` và đã lưu file template vào app/template/admin, thứ tự gọi sẽ là:

```
 1. app/template/admin/Product/index.twig
 2. src/Eccube/Resource/template/admin/Product/index.twig
 3. app/Plugin/[plugin_code]/Resource/template/admin/Product/index.twig
```

## Hành vi của file template khi chỉnh sửa từ trang quản trị (chỉnh sửa trang, block)

* Chi tiết trang  
Mặc định sẽ hiển thị file tương ứng trong `ECCUBEROOT/src/Eccube/Resource/template/default`.  
Khi chỉnh sửa từ chi tiết trang, file sẽ được lưu mới vào `ECCUBEROOT/app/template/default/` và từ đó về sau sẽ chỉnh sửa file trong thư mục này.

* Chỉnh sửa block  
Mặc định sẽ hiển thị file tương ứng trong `ECCUBEROOT/src/Eccube/Resource/template/default/Block`.  
Khi tạo mới hoặc chỉnh sửa block, file sẽ được lưu vào `ECCUBEROOT/app/template/default/Block` và từ đó về sau sẽ chỉnh sửa file trong thư mục này.
