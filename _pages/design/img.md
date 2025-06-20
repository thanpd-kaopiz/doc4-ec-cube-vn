---
title: Quản lý hình ảnh
keywords: thiết kế hình ảnh tùy chỉnh
tags: [thiết kế]
permalink: design_img
summary: Giải thích về quản lý hình ảnh và cách gọi hình ảnh.
---

## Về hình ảnh
Khi muốn thêm hình ảnh khi tùy chỉnh thiết kế<br>
Có hai cách: thêm trực tiếp vào thư mục hoặc upload từ trang quản trị.

## Cách thêm trực tiếp vào thư mục hình ảnh

### Đường dẫn thư mục hình ảnh

- Thư mục mặc định<br>
    `ECCUBEROOT/html/template/default/assets/img/`<br>
    ※ ECCUBEROOT là thư mục cài đặt EC-CUBE.

- Thư mục mặc định khi sử dụng template thiết kế riêng<br>
    `ECCUBEROOT/html/template/[template_code]/assets/img/`<br>
    → [template_code] là mã nhận diện template.<br>
    Mặc định với frontend là "default"


## Cách liên kết tới hình ảnh
Khi muốn gọi hình ảnh, hãy viết theo cú pháp twig như sau:
```twig
{% raw %}{{ asset('assets/img/tên_thư_mục/tên_hình_ảnh') }}{% endraw %}
```

Ví dụ: muốn hiển thị hình hoge.jpg trong thư mục top
```twig
{% raw %}<img src="{{ asset('assets/img/top/hoge.jpg') }}" alt="hoge">{% endraw %}
```

Cũng có thể viết như sau, nhưng khi đổi template có thể không hiển thị:
```html
<img src="html/template/defult/assets/img/top/hoge.jpg" alt="hoge">
```

## Cách thêm hình ảnh từ trang quản trị
Ngay cả khi không thể upload lên ec-cube.co hoặc server, bạn vẫn có thể thêm file hình ảnh từ trang quản trị.

### Upload hình ảnh
Từ [Quản lý nội dung] -> [Quản lý file] có thể upload hình ảnh.

Ngoài hình ảnh, bạn cũng có thể upload các file khác.<br>
Khi upload, nên tạo thư mục img trong assets để quản lý dễ dàng hơn.

![Thêm thư mục và hiển thị thư mục img](./images/design/design-img-01.png)

Chọn file từ "Thêm file", sau đó nhấn nút upload để thêm file.<br>
※ Có thể chọn nhiều file cùng lúc bằng Shift hoặc Ctrl khi chọn file.

![Đã thêm file](./images/design/design-img-02.png)


### Đường dẫn thư mục chứa hình ảnh upload từ trang quản trị
Hình ảnh upload sẽ được lưu trong thư mục user_data.

- Đường dẫn tới hình ảnh upload<br>
    `ECCUBEROOT/html/user_data/assets/tên_thư_mục/tên_hình_ảnh`<br>
    ※ ECCUBEROOT là thư mục cài đặt EC-CUBE.

### Cách liên kết tới hình ảnh upload từ trang quản trị
Hình ảnh upload sẽ xuất hiện trong danh sách file.<br>
Nhấn vào icon copy để lấy link hình ảnh và tự động copy vào clipboard.

![Đã thêm file](./images/design/design-img-04.png)

Ví dụ: muốn hiển thị hình hoge.png trong thư mục img
```html
<img src="/html/user_data/assets/img/hoge.png" alt="hoge">
```

Cũng có thể viết như sau:
```twig
{% raw %}<img src="{{ asset('assets/img/hoge.png','user_data') }}" alt="hoge">{% endraw %}
```


## 【Bổ sung】Về hình ảnh upload từ Quản lý sản phẩm > Đăng ký sản phẩm
Hình ảnh upload khi đăng ký sản phẩm sẽ được lưu ở thư mục khác.<br>
Không nên thêm trực tiếp vào thư mục này.

 - Đường dẫn tới hình ảnh upload từ đăng ký sản phẩm<br>
    `ECCUBEROOT/html/upload/save_image/`<br>
    ※ ECCUBEROOT là thư mục cài đặt EC-CUBE.

### Cách liên kết tới hình ảnh upload từ đăng ký sản phẩm
Khi muốn gọi hình ảnh, hãy viết theo cú pháp twig như sau:
```twig
{% raw %}{{ asset('tên_hình_ảnh', 'save_image') }}{% endraw %}
```
Tên hình ảnh sẽ bị đổi khi upload, hãy kiểm tra tên hình ảnh hiển thị trên trang chi tiết sản phẩm.

Ví dụ: muốn hiển thị hình hoge-1.jpg
```twig
{% raw %}<img src="{{ asset('hoge-1.jpg', 'save_image') }}" alt="hoge">{% endraw %}
```
