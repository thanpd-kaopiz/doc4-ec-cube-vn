---
title: Tuỳ biến FormType
keywords: core tuỳ biến FormType
tags: [core, formtype]
permalink: customize_formtype
folder: customize
---

## Mở rộng bằng FormExtension

Bằng cách sử dụng cơ chế FormExtension, bạn có thể tuỳ biến các form hiện có.

### Cách mở rộng

Tạo file class kế thừa `AbstractTypeExtension` trong thư mục `./app/Customize/Form/Extension/`, hệ thống sẽ tự động nhận diện là FormExtension.

#### Chỉ định loại form cần mở rộng

Với EC-CUBE 4.0, bạn cần cài đặt hàm getExtendedType và chỉ định loại form muốn mở rộng.

```php
public function getExtendedType()
{
    return EntryType::class;
}
```

Từ EC-CUBE 4.1 trở đi, bạn cần cài đặt hàm getExtendedTypes và chỉ định loại form muốn mở rộng.

```php
public static function getExtendedTypes(): iterable
{
    yield EntryType::class;
}
```

#### Các hàm có thể override để mở rộng

Bạn có thể override các hàm sau và thay đổi tham số truyền vào để tuỳ biến form:

- buildForm()
- buildView()
- configureOptions()
- finishView()

EC-CUBE 4 sử dụng cơ chế FormExtension của Symfony. 
Tham khảo chi tiết cách mở rộng tại tài liệu Symfony:
https://symfony.com/doc/current/form/create_form_type_extension.html

### Ví dụ

Ví dụ mở rộng form đăng ký hội viên, chuyển trường "Tên công ty" thành bắt buộc nhập.

./app/Customize/Form/Extension/CompanyNameRequiredExtension.php

```php
<?php

namespace Customize\Form\Extension;

use Eccube\Form\Type\Front\EntryType;
use Symfony\Component\Form\AbstractTypeExtension;
use Symfony\Component\Form\Extension\Core\Type\TextType;
use Symfony\Component\Form\FormBuilderInterface;
use Symfony\Component\Validator\Constraints\NotBlank;

class CompanyNameRequiredExtension extends AbstractTypeExtension
{
    /**
     * {@inheritdoc}
     */
    public function buildForm(FormBuilderInterface $builder, array $options)
    {
        $options = $builder->get('company_name')->getOptions();

        $options['required'] = true;
        $options['constraints'] = [ new NotBlank() ];
        $options['attr']['placeholder'] = 'Tên công ty';

        $builder->add('company_name', TextType::class, $options);
    }

    /**
     * {@inheritdoc}
     */
    public function getExtendedType()
    {
        return EntryType::class;
    }
    
    /**
     * {@inheritdoc}
     */
    public static function getExtendedTypes(): iterable
    {
        yield EntryType::class;
    }
}

```

## Mở rộng tạo form từ Entity

Tham khảo [Tuỳ biến Entity](/customize_entity).

