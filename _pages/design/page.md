---
title: Tạo trang mới
keywords: thiết kế trang
tags: [thiết kế]
permalink: design_page
summary: Giải thích về việc thay đổi thiết kế sử dụng quản lý trang.

---

## Về quản lý trang
EC-CUBE 4.0, chức năng "Quản lý trang" chỉ dùng để thêm mới và chỉnh sửa trang, việc bố trí block cho từng trang sẽ thực hiện ở [Quản lý layout](design_layout).  
Quản lý trang vẫn cho phép chỉnh sửa trang như các phiên bản 2.x, 3.x.


### Tạo mới trang trong quản lý trang

Sau khi đăng nhập vào trang quản trị,  
Từ [Quản lý nội dung] -> [Quản lý trang], nhấn nút "Nhập mới" để tạo trang mới.

![Quản lý block](./images/design/design-block-01.png)

Nhập tên trang, URL, tên file (phải là duy nhất), nhập mã html muốn hiển thị vào phần chỉnh sửa mã, sau đó nhấn nút "Đăng ký" để tạo trang.  
Lưu ý: Nếu đặt tên file trùng với file đã có, trang mới sẽ ghi đè lên trang cũ.

Khi tạo trang mới, hãy viết như sau:

{% highlight twig  %}
{% raw %}
{% extends 'default_frame.twig' %}

{% block main %}
    Viết mã html tại đây
{% endblock %}{% endraw %}
{% endhighlight %}

Nếu không viết `{% raw %}{% extends 'default_frame.twig' %}{% endraw %}`, `{% raw %}{% block main %}{% endraw %}`, `{% raw %}{% endblock %}{% endraw %}` thì header sẽ không hiển thị, vì vậy cần phải có các dòng này.


### Xoá trang

Các trang mặc định không thể xoá, chỉ có thể xoá các trang do bạn tự tạo mới.
