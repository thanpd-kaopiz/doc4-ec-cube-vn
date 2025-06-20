---
title: Đa ngôn ngữ
keywords: multilingualization
tags: [i18n, multilingualization]
permalink: i18n_multilingualization
folder: i18n

---

## Tổng quan

Mặc định sẽ hiển thị bằng tiếng Nhật, nhưng EC-CUBE đã tích hợp sẵn cơ chế hiển thị bằng tiếng Anh hoặc ngôn ngữ khác. Bạn có thể chuyển đổi ngôn ngữ hiển thị bằng cách chỉ định locale trong biến môi trường, hiện tại hỗ trợ tiếng Nhật và tiếng Anh.

## Cách chuyển đổi ngôn ngữ

Chỉ định locale trong biến môi trường để chuyển đổi ngôn ngữ hiển thị.

Thiết lập `ECCUBE_LOCALE` trong file `.env` ở thư mục gốc EC-CUBE. Mặc định biến này sẽ bị comment. Nếu không thiết lập gì, hệ thống sẽ dùng tiếng Nhật.

```bash
//.env

#ECCUBE_LOCALE=ja
ECCUBE_LOCALE=en

```

Sau khi thiết lập biến môi trường, chỉ cần reload trang là ngôn ngữ sẽ được chuyển đổi.
Không cần xoá cache.

## Chỉ định ngôn ngữ khi cài đặt

Để chỉ định ngôn ngữ khi cài đặt, thiết lập `ECCUBE_LOCALE` trong file `.env.install` ở thư mục gốc EC-CUBE. Nếu không chỉ định, hệ thống sẽ cài đặt bằng tiếng Nhật. Nếu có dữ liệu khởi tạo cho ngôn ngữ đó trong `/src/Eccube/Resource/doctrine/import_csv`, dữ liệu master sẽ được cài đặt theo ngôn ngữ đã chọn.

```bash
//.env.install

ECCUBE_LOCALE=en

```

Sau khi cài đặt, mặc định hệ thống sẽ dùng tiếng Nhật. Nếu muốn sử dụng ngôn ngữ khác, hãy chỉnh lại giá trị `ECCUBE_LOCALE` trong `.env.install`.

※ Hiện tại, dữ liệu lưu trong database sẽ không được dịch tự động.
※ Cả trang shop và trang quản trị đều sẽ chuyển đổi ngôn ngữ hiển thị.

## File message (file dịch)

Các file message được lưu trong `src/Eccube/Resouce/locale`.
Tùy theo giá trị `ECCUBE_LOCALE`, hệ thống sẽ đọc các file:

- messages.xxx.yaml
- validators.xxx.yaml

Các file message là file yaml dạng hash.
Key là ID message, value là chuỗi đã dịch.

```yaml
#====================================================================================
# Chung
#====================================================================================

common.select: Vui lòng chọn
common.select__pref: Chọn tỉnh/thành phố
common.select__unspecified: Không chỉ định
common.select__all_products: Tất cả sản phẩm
    ...
```

## Hàm trans và filter trans

Bạn có thể sử dụng hàm trans hoặc filter trans để hiển thị chuỗi đã dịch.
Dùng hàm trans trong PHP, dùng filter trans trong twig.

## Hàm trans

Chỉ định ID message cho hàm trans để lấy chuỗi đã dịch.
Cách sử dụng cơ bản như sau:

```php
<?php

// 'common.label.add' => 'Tạo mới',

$message = trans('common.label.edit');
var_dump($message);

// Sửa
```

Nếu message có tham số, sử dụng như sau:

```php
<?php

// 'admin.order.index.paginator_total_count' => 'Kết quả tìm kiếm: %count% bản ghi',

$message = trans('admin.order.index.paginator_total_count', ['%count%' => 10]);
var_dump($message);

// Kết quả tìm kiếm: 10 bản ghi

```

※ Label và message lỗi trong FormType sẽ tự động được dịch, không cần gọi trans trong FormType.

```php
class TemplateType extends AbstractType
{
    /**
     * {@inheritdoc}
     */
    public function buildForm(FormBuilderInterface $builder, array $options)
    {
        $builder

            ...

            ->add('file', FileType::class, array(
                'mapped' => false,
                'required' => true,
                'constraints' => array(
                    // Chỉ cần chỉ định ID message
                    new Assert\NotBlank(array('message' => 'template.text.message.select_file')),
                    new Assert\File(array(
                        'mimeTypes' => array('application/zip', 'application/x-tar', 'application/x-gzip'),
                        'mimeTypesMessage' => 'template.text.message.upload_files',
                    )),
                ),
            ));
    }

```

## Filter trans

Khi dịch trong twig, sử dụng filter trans.
Cách sử dụng cơ bản như sau:

```twig
{% raw %}
{{ 'common.label.add'|trans }}

{# Sửa #}
{% endraw %}
```

Nếu message có tham số, sử dụng như sau:

```twig
{% raw %}
{{ 'admin.order.index.paginator_total_count'|trans({
    '%count%' : 10
}) }}

{# Kết quả tìm kiếm: 10 bản ghi #}
{% endraw %}
```

# Tham khảo

Cơ chế dịch của EC-CUBE sử dụng component Translation của Symfony.
Tham khảo thêm tại tài liệu chính thức của Symfony:

[Translations](http://symfony.com/doc/current/translation.html){:target="_blank"}
