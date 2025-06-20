---
title: Thay đổi bố cục form
keywords: thiết kế 
tags: [thiết kế]
permalink: design_form
summary: Hướng dẫn cách thay đổi bố cục form.
---

## Cấu trúc màn hình form
Khi tạo màn hình form, bạn không nên viết trực tiếp thẻ `<input type="text" name="hoge">` mà nên sử dụng các hàm Twig để tạo form.  

Để hiểu rõ hơn về form, hãy tham khảo trang của Symfony:  
[https://symfony.com/doc/current/forms.html](https://symfony.com/doc/current/forms.html){:target="_blank"}  
[https://symfony.com/doc/current/best_practices/forms.html](https://symfony.com/doc/current/best_practices/forms.html){:target="_blank"}

## Cách xuất nội dung form
Khi tạo màn hình form với Twig, bạn sử dụng các hàm và biến chuyên dụng.

```twig
{% raw %}{{ form(form) }}{% endraw %}
→ 'form' ở đây là tên key được truyền từ Controller
```
Khi viết như trên, các trường của form sẽ được hiển thị.
Nếu muốn xuất riêng từng trường:

```twig
{% raw %}{{ form_row(form.name) }}{% endraw %}
hoặc
{% raw %}{{ form_widget(form.name) }}{% endraw %}
```

## Thay đổi bố cục form
Khi sử dụng hàm form, các thẻ sẽ tự động được thêm vào để tạo màn hình form, nhưng đôi khi bạn muốn thay đổi thiết kế form cho phù hợp.

EC-CUBE cung cấp sẵn template để xuất nội dung form, bạn có thể chỉnh sửa file này để thay đổi thiết kế khi xuất form.

Vị trí các file bố cục form cho frontend và admin:

- Bố cục form cho frontend  
ECCUBEROOT/src/Eccube/Resource/template/default/Form/form_div_layout.twig

- Bố cục form cho admin  
ECCUBEROOT/src/Eccube/Resource/template/admin/Form/bootstrap_4_layout.html.twig
ECCUBEROOT/src/Eccube/Resource/template/admin/Form/bootstrap_4_horizontal_layout.html.twig

## Nội dung file form_div_layout.twig sử dụng ở frontend

Nội dung bố cục form được định nghĩa bằng các block (ví dụ: form_errors, form_label) và có thể ghi đè lại theo ý muốn.
Các block như `form_errors` hay `form_label` tương ứng với các hàm Twig.

### Nội dung file form_div_layout.twig

{% highlight twig  %}
{% raw %}
{#
 - form_div_layout.html.twig
 - https://github.com/symfony/symfony/blob/master/src/Symfony/Bridge/Twig/Resources/views/Form/form_div_layout.html.twig
#}
{%- extends 'form_div_layout.html.twig' -%}

{%- block form_errors -%}
    {%- if errors|length > 0 -%}
        {%- for error in errors -%}
            <p class="ec-errorMessage">{{ error.message|trans({}, translation_domain) }}</p>
        {%- endfor -%}
    {%- endif -%}
{%- endblock form_errors -%}

{%- block form_label -%}
    {{ parent() }}
    {%- if required -%}
        <span class="ec-required">{{'common.text.message.required'|trans}}</span>
    {%- endif -%}
{%- endblock form_label -%}

{% block choice_widget %}
    {% if type is defined and type == 'hidden' %}
        {{ block('form_widget_simple') }}
    {% else %}
        {{ parent() }}
    {% endif %}
{% endblock %}

{%- block textarea_widget -%}
    {% if type is defined and type == 'hidden' %}
        {{ block('form_widget_simple') }}
    {% else %}
        {{ parent() }}
    {% endif %}
{%- endblock textarea_widget -%}
{% endraw %}
{% endhighlight %}

Ví dụ, nếu muốn thay đổi thiết kế hiển thị lỗi bằng form_errors:

```twig
{% raw %}{%- block form_errors -%}
    {%- if errors|length > 0 -%}
        <ul>
        {%- for error in errors -%}
            <li>{{ error.message|trans({}, translation_domain) }}</li>
        {%- endfor -%}
        </ul>
    {%- endif -%}
{%- endblock form_errors -%}{% endraw %}
```

Chỉ cần đổi thẻ p thành ul là có thể thay đổi cách hiển thị lỗi.

Các hàm Twig khác cũng có thể thay đổi thiết kế bằng cách ghi đè nội dung block tương ứng.

## Cách sử dụng thiết kế form ở frontend

Khi sử dụng form ở frontend, bạn cần khai báo rõ theme cho form bằng dòng sau: `{% raw %}{% form_theme form 'Form/form_div_layout.twig' %}{% endraw %}`
Dòng này dùng để chỉ định theme cho form.

### Cách sử dụng

```twig
{% raw %}{% extends 'default_frame.twig' %}

{% form_theme form 'Form/form_div_layout.twig' %}

{% block main %}
・
・
・
{{ form_widget(form.name.name01, {'attr': {'placeholder': 'signup.label.family_name'}}) }}
・
・
・
{% endblock %}{% endraw %}
```

Trong đó,

```twig
{% raw %}{% form_theme form 'Form/form_div_layout.twig' %}{% endraw %}
```

và

```twig
{% raw %}{{ form_widget(form.name.name01, {'attr': {'placeholder': 'signup.label.family_name'}}) }}{% endraw %}
```

biến `form` là tên biến được truyền từ Controller.
Nếu Controller truyền sang là `form1`, bạn cần viết:

```twig
{% raw %}{% form_theme form1 'Form/form_div_layout.twig' %}{% endraw %}
```

hoặc

```twig
{% raw %}{{ form_widget(form1.name.name01, {'attr': {'placeholder': 'signup.label.family_name'}}) }}{% endraw %}
```

Để tìm hiểu chi tiết hơn về tuỳ biến form, hãy tham khảo trang Symfony:  
[http://symfony.com/doc/current/form/form_customization.html](http://symfony.com/doc/current/form/form_customization.html){:target="_blank"}
