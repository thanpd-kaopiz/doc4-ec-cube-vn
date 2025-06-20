---
layout: single
title: Kiểm soát danh sách cho phép với Twig Sandbox
keywords: core tuỳ biến twig danh sách cho phép sandbox
tags: [core, twig, sandbox]
permalink: customize_twig_sandbox
folder: customize
---

---

## Kiểm soát danh sách cho phép với Twig Sandbox

※Chức năng này có từ EC-CUBE 4.2.3.

Để tăng cường bảo mật, EC-CUBE bổ sung chức năng kiểm soát bằng danh sách cho phép nhằm ngăn chặn việc thực thi các chức năng twig không mong muốn.
Với chức năng này, bạn có thể lựa chọn các chức năng (tag, filter, function) được phép sử dụng trong twig.

### Tips: Về chức năng của twig

EC-CUBE sử dụng twig làm template engine.
Twig cho phép sử dụng các hàm, biến, giúp xây dựng View linh hoạt. Tuy nhiên, nếu lạm dụng, có thể gây rò rỉ thông tin ngoài ý muốn.

Mặc định, output từ template twig của EC-CUBE sẽ được escape HTML. Tuy nhiên, nếu dùng filter như `raw`, bạn có thể bỏ escape một cách chủ động. Nếu dữ liệu đầu vào là từ bên ngoài, điều này có thể bị lợi dụng để tấn công.

```
{{ "{{ variable|raw " }}}}
```

## Kiểm soát chức năng bằng Sandbox

Để loại bỏ rủi ro trên, EC-CUBE áp dụng Sandbox cho các khu vực sau:

* Free area trên trang chi tiết sản phẩm
* Meta tag (Quản trị > Quản lý nội dung > Quản lý trang > Meta tag)

Trong Sandbox, chỉ các chức năng twig có trong danh sách cho phép mới được sử dụng.
(Các chuỗi ký tự thông thường vẫn ghi bình thường)

![Vị trí sử dụng Sandbox]({{site.baseurl}}/images/customize/sandbox.png)

## Danh sách cho phép mặc định

**※Chỉ các chức năng twig liệt kê dưới đây mới dùng được trong Sandbox.**
Nếu cần thêm chức năng khác, hãy bổ sung vào danh sách cho phép.

[Xem cấu hình danh sách cho phép mặc định](https://github.com/EC-CUBE/ec-cube/blob/4.2/app/config/eccube/packages/twig_extensions.yaml){:target="_blank"}

## Chỉnh sửa danh sách cho phép

Cấu hình bằng file yaml.
Chỉnh sửa các file sau:

* Danh sách cho phép mặc định: `app/config/eccube/packages/twig_extensions.yaml`
* Nếu Customize: `app/Customize/Resource/config/services.yaml`

Chuẩn bị list dưới đây để thêm/bớt chức năng.

### Đối với tag

```yaml
parameters:
    eccube.twig_sandbox.allowed_tags:
        - 'apply'
        - 'block'
        - 'deprecated'
        - 'embed'
        - 'extends'
        - 'flush'
# ...
```

### Đối với filter

```yaml
    eccube.twig_sandbox.allowed_filters:
        - 'abs'
        - 'batch'
        - 'capitalize'
        - 'column'
        - 'convert_encoding'
        - 'country_name'
# ...
```

### Đối với function

```yaml
    eccube.twig_sandbox.allowed_functions:
        - 'cycle'
        - 'date'
        - 'max'
        - 'min'
        - 'random'
        - 'range'
# ...
```

### Khác

Nếu muốn kiểm soát method/property, chỉnh các mục sau:

```yaml
    eccube.twig_sandbox.allowed_methods:
        'Symfony\Bridge\Twig\AppVariable': [ 'getrequest' ]
        'Symfony\Component\HttpFoundation\Request': [ 'geturi' ]
    eccube.twig_sandbox.allowed_properties: []
```

## Hành vi của Sandbox

Hiện tại, nếu có code không nằm trong danh sách cho phép trong Sandbox:

* Ở chế độ phát triển (`APP_ENV=dev`): "Hiển thị lỗi"
* Ở chế độ production (`APP_ENV=prod`): "Ghi log lỗi và xoá nội dung không hợp lệ trong sandbox"

### Trường hợp chế độ phát triển

Sẽ hiển thị màn hình lỗi như sau:

![Màn hình lỗi]({{site.baseurl}}/images/customize/error_screen.png)

### Trường hợp production

Log sẽ ghi lại nội dung như sau:

```
Filter "abs" is not allowed in "__string_template__cceb5b1ce6c6124b4a33368da2e5f5c5" at line 3
```

![Màn hình log]({{site.baseurl}}/images/customize/log_screen.png)

### Nếu thông tin chi tiết sản phẩm từng hiển thị nay không còn

Có thể do sử dụng keyword không có trong danh sách cho phép của Sandbox. Hãy kiểm tra log xem có bị hạn chế keyword không.
Nếu có, hãy kiểm tra [danh sách cho phép](#danh-sach-cho-phep-mac-dinh) và bổ sung nếu cần.

## Tham khảo

Chức năng kiểm soát danh sách cho phép này sử dụng Sandbox của twig. Tham khảo thêm tại:

[Sandbox Extension](https://twig.symfony.com/doc/3.x/api.html#sandbox-extension){:target="_blank"}