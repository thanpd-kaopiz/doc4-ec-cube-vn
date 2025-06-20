---
title: Thêm & Viết tài liệu
description: Hướng dẫn cách thêm trang và viết markdown cho tài liệu phát triển EC-CUBE4.
tags: [howto]
permalink: documents/writing-and-formatting
---

## Cách thêm trang mới

Trang được tự động sinh bằng [Jekyll](http://jekyllrb-ja.github.io/){:target="_blank"}.
Chỉ cần đặt file markdown (.md) vào thư mục `_pages` trong [source code tài liệu phát triển](https://github.com/EC-CUBE/doc4.ec-cube.net/){:target="_blank"}, trang sẽ tự động được thêm mới.

### Cách viết phần header của markdown

Đây là thông tin header dùng khi sinh trang. Bắt buộc phải có ở mỗi trang.

```yaml
---
title: Trang thử nghiệm
description: Tổng hợp các lưu ý khi cài đặt công cụ và triển khai xxxx.
permalink: test
tags: [quickstart, install]
---
```

`title`: Sẽ là nội dung thẻ h1.
`description`: Sẽ là `og:description` khi share.
`permalink`: Đường dẫn URL của trang. Có thể viết dạng hoge/test.
`tags`: Gắn tag cho trang.

### Thêm vào menu bên trái

Thêm vào `_data/navigation.yml`. Có thể tạo menu con đến 2 cấp.

```yaml
docs:
  - title: Danh mục lớn
    output: web, pdf
    children:
      - title: Nội dung
        url: /quickstart_requirement
        output: web, pdf
      - title: Danh mục nhỏ
        output: web, pdf
        sub_items:
        - title: Nội dung
          url: /update
          output: web, pdf
```

## Cách viết nội dung trang

- Viết bằng markdown.
- Để xuống dòng (br tag) cần 2 dấu xuống dòng liên tiếp.
- Khi link ra ngoài, thêm `{:target="_blank"}`.
- Có thể highlight code bằng cách viết "```php".
- Có thể sử dụng các Utility/Helpers template đã cung cấp:
    - [Utility](https://mmistakes.github.io/minimal-mistakes/docs/utility-classes/){:target="_blank"}
    - [Helpers](https://mmistakes.github.io/minimal-mistakes/docs/helpers/){:target="_blank"}

### Ví dụ Utility

{: .notice--info}
Bạn có thể đóng khung thông tin bổ sung để dễ đọc hơn.

[Bạn cũng có thể tạo nút link](#link){: .btn .btn--primary}
