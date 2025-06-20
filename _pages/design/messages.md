---
title: Tuỳ chỉnh thông điệp (message)
keywords: thiết kế
tags: [thiết kế]
permalink: design_messages
description: Giải thích về việc tuỳ chỉnh thông điệp (message).
---

## Vị trí lưu file thông điệp

- Thư mục mặc định chứa file thông điệp  
`src/Eccube/Resource/locale/`

Tên trường và thông điệp lỗi được tập trung trong các file sau:

- Tiếng Nhật  
  `src/Eccube/Resource/locale/messages.ja.yaml`  
  `src/Eccube/Resource/locale/validators.ja.yaml` 

- Tiếng Anh  
  `src/Eccube/Resource/locale/messages.en.yaml`  
  `src/Eccube/Resource/locale/validators.en.yaml`  

## Vị trí lưu file khi tuỳ chỉnh thông điệp

- Thư mục lưu file thông điệp tuỳ chỉnh  
`app/Customize/Resource/locale/` 

Khi sử dụng tuỳ chỉnh thông điệp, các file sẽ được lưu tại thư mục này.  
Bạn thêm hoặc sửa thông điệp tuỳ ý vào các file sau:

- Tiếng Nhật  
  `app/Customize/Resource/locale/messages.ja.yaml`  
  `app/Customize/Resource/locale/validators.ja.yaml`   

- Tiếng Anh  
  `app/Customize/Resource/locale/messages.en.yaml`    
  `app/Customize/Resource/locale/validators.en.yaml`  


## Thay đổi/Thêm thông điệp

File thông điệp là file yaml dạng hash. Key là ID của thông điệp, value là chuỗi đã dịch.  
Ví dụ một phần của `src/Eccube/Resource/locale/messages.ja.yaml`:

```
#====================================================================================
# Chung
#====================================================================================

common.select: Vui lòng chọn
common.select__pref: Chọn tỉnh/thành phố
common.select__unspecified: Không chỉ định
common.select__all_products: Tất cả sản phẩm

```  

Khi muốn thay đổi/thêm thông điệp, hãy ghi vào `app/Customize/Resource/locale/messages.ja.yaml` như sau:

```
#====================================================================================
# Thay đổi
#====================================================================================
common.select: [Chuỗi muốn ghi đè]

#====================================================================================
# Thêm mới
#====================================================================================
[ID thông điệp mới]: [Chuỗi muốn định nghĩa]

```


### Về phiên bản trước 4.0.3

Với phiên bản trước 4.0.3, đường dẫn `app/Customize/Resource/locale/` chưa được thêm vào,
nên cần thêm dòng sau vào file `app/config/eccube/packages/translation.yaml`:

```
framework:
    default_locale: '%locale%'
    translator:
        paths:
            - '%kernel.project_dir%/src/Eccube/Resource/locale/'
            - '%kernel.project_dir%/app/Customize/Resource/locale/'
        fallbacks:
            - '%locale%'
```


