---
title: Tuỳ biến Entity
keywords: core tuỳ biến Entity
tags: [core, entity]
permalink: customize_entity
folder: customize
---

## Mở rộng Entity [#2267](https://github.com/EC-CUBE/ec-cube/pull/2267){:target="_blank"}

### Cách mở rộng cơ bản

Bạn có thể mở rộng field của Entity bằng cách sử dụng trait và annotation `@EntityExtension`.
Không cần kế thừa, EC-CUBE sẽ tự động sinh Proxy class, cho phép nhiều plugin hoặc tuỳ biến cùng mở rộng một entity.

```php
<?php

namespace Customize\Entity;

use Doctrine\ORM\Mapping as ORM;
use Eccube\Annotation\EntityExtension;

/**
  * @EntityExtension("Eccube\\Entity\\Product")
 */
trait ProductTrait
{
    /**
     * @ORM\Column(type="string", nullable=true)
     */
    public $maker_name;
}
```

Tham số của annotation `@EntityExtension` là tên class bạn muốn áp dụng trait.
Trong trait, bạn khai báo các field muốn thêm, sử dụng annotation của Doctrine ORM như `@ORM\Column` để định nghĩa DB.

Sau khi tạo trait, chạy lệnh sau để sinh Proxy class:

```
bin/console eccube:generate:proxies
```

Sau đó, chạy lệnh sau để cập nhật DB:

```
## Xoá cache để nhận Proxy mới
bin/console cache:clear --no-warmup

## Xem SQL sẽ thực thi
bin/console doctrine:schema:update --dump-sql

## Thực thi SQL
bin/console doctrine:schema:update --dump-sql --force
```

#### Sử dụng trong Controller hoặc Twig

Bạn có thể sử dụng field mở rộng như bình thường trong controller hoặc twig.

```php
// Ví dụ trong controller
public function index()
{
    $Product = $this->productRepository->find(1);
    dump($Product->maker_name);

    $Product->maker_name = 'abc';
    $this->entityManger->persist($Product);
    $this->entityManger->flush();
    ...
```

```twig
{# Ví dụ trong twig #}
{{ Product.maker_name }}
```

### Tự động sinh form từ Entity

Nếu muốn tự động sinh form cho field mở rộng, thêm annotation `@FormAppend` vào field trong trait.

```php
<?php

namespace Customize\Entity;

use Doctrine\ORM\Mapping as ORM;
use Eccube\Annotation as Eccube;
use Symfony\Component\Validator\Constraints as Assert;

/**
 * @Eccube\EntityExtension("Eccube\\Entity\\BaseInfo")
 */
trait BaseInfoTrait
{
    /**
     * @ORM\Column(name="company_name_vn", type="string", length=255, nullable=true)
     * @Eccube\FormAppend
     * @Assert\NotBlank(message="Vui lòng nhập thông tin!")
     */
    public $company_name_vn;
}
```

Khi thêm annotation `@FormAppend`, form sẽ tự động có field mới. Nếu muốn kiểm tra dữ liệu nhập, dùng các annotation của Symfony như `@NotBlank`.

Nếu muốn tuỳ biến form chi tiết hơn, dùng `auto_render=true` và chỉ định `form_theme`, `type`, `option`.

```php
<?php

namespace Customize\Entity;

use Doctrine\ORM\Mapping as ORM;
use Eccube\Annotation as Eccube;
use Symfony\Component\Validator\Constraints as Assert;

/**
 * @Eccube\EntityExtension("Eccube\\Entity\\BaseInfo")
 */
trait BaseInfoTrait
{
    /**
     * @ORM\Column(name="company_name_vn", type="string", length=255, nullable=true)
     * @Assert\NotBlank(message="Vui lòng nhập thông tin")
     * @Eccube\FormAppend(
     *     auto_render=true,
     *     form_theme="Form/company_name_vn.twig",
     *     type="\Symfony\Component\Form\Extension\Core\Type\TextType",
     *     options={
     *          "required": true,
     *          "label": "Tên công ty (VN)"
     *     })
     */
    public $company_name_vn;
}
```

