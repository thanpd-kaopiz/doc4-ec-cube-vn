---
title: Thêm video YouTube vào trang chi tiết sản phẩm
keywords: core tuỳ biến Entity Product
tags: [core, entity, product]
permalink: reverse-lookup/sample-code/add-youtube-to-product-detail
folder: sample-code
---

## Thêm video YouTube vào trang chi tiết sản phẩm

1. Tạo ProductTrait
1. Tạo proxy và cập nhật DB schema
1. Thêm thẻ youtube vào detail.twig

### Tạo ProductTrait

Có thể mở rộng field của ProductEntity bằng trait và annotation `@EntityExtension`.
Việc này cho phép tạo Proxy class mà không cần kế thừa, giúp nhiều plugin hoặc tuỳ biến cùng mở rộng mà không xung đột.

``` php
<?php

namespace Customize\Entity;

use Doctrine\ORM\Mapping as ORM;
use Eccube\Annotation\EntityExtension;

/**
  * @EntityExtension("Eccube\Entity\Product")
 */
trait ProductTrait
{
    /**
     * @ORM\Column(type="string", nullable=true)
     */
    public $youtube_url;
}
```

Tham số của annotation `@EntityExtension` là class muốn áp dụng trait.
Trong trait, định nghĩa các field muốn thêm.
Dùng annotation của Doctrine ORM như `@ORM\Column` để định nghĩa DB.

#### Hiển thị form trên quản trị

Nếu thêm annotation `@FormAppend` vào field mở rộng bằng `@EntityExtension`, form sẽ tự động sinh ra.

``` php
<?php

namespace Customize\Entity;

use Doctrine\ORM\Mapping as ORM;
use Eccube\Annotation as Eccube;
use Symfony\Component\Validator\Constraints as Assert;

/**
 * @Eccube\EntityExtension("Eccube\Entity\Product")
 */
trait ProductTrait
{
    /**
     * @ORM\Column(type="string", nullable=true)
     * @Eccube\FormAppend(
     *     auto_render=true,
     *     type="\Symfony\Component\Form\Extension\Core\Type\TextType",
     *     options={
     *          "required": false,
     *          "label": "YouTube URL"
     *     })
     */
    public $youtube_url;

    /**
     * Không bắt buộc nhưng nên có
     */
    public function getYoutubeUrl()
    {
        return $this->youtube_url;
    }

    /**
     * Không bắt buộc nhưng nên có
     */
    public function setYoutubeUrl($url = null)
    {
        $this->youtube_url = $url;
        return $this;
    }
}

```

Khi thêm annotation `@FormAppend`, form của field sẽ tự động được thêm vào các form sử dụng entity đó.
Nếu muốn kiểm tra dữ liệu nhập, có thể dùng các annotation chuẩn của Symfony như `@NotBlank`.

Nếu muốn tuỳ biến form chi tiết, hãy dùng `auto_render=true` và chỉ định `form_theme`, `type`, `option`.

### Tạo proxy và cập nhật DB schema

Sau khi tạo trait, chạy lệnh `bin/console eccube:generate:proxies` để sinh Proxy class.

```
bin/console eccube:generate:proxies
```

Sau khi sinh Proxy, chạy lệnh `bin/console doctrine:schema:update` để cập nhật DB.

```
## Xoá cache để nhận Proxy mới
bin/console cache:clear --no-warmup

## Xem trước SQL
bin/console doctrine:schema:update --dump-sql

## Thực thi SQL
bin/console doctrine:schema:update --dump-sql --force
```

Sau đó, form nhập URL YouTube sẽ tự động xuất hiện trên quản trị.

<img width="914" alt="ss2021-01-12 16 11 00" src="https://user-images.githubusercontent.com/485749/104288126-bf1f7880-54fa-11eb-816d-75b0d947abef.png">

### Thêm thẻ youtube vào detail.twig

Thêm thẻ YouTube vào vị trí muốn hiển thị trong template ``Prdoduct/detail.twig``.

<script src="https://gist.github.com/tao-s/3b67f9f6dc19f78593eda49877df3b6b.js"></script>

Hãy kiểm tra biến `youtube_url` đã được định nghĩa chưa, chỉ hiển thị thẻ YouTube khi có giá trị.

Kết quả hiển thị ở front sẽ như sau.

<img width="1204" alt="スクリーンショット 2021-01-12 17 16 05" src="https://user-images.githubusercontent.com/485749/104288010-94cdbb00-54fa-11eb-80b0-2c524478ed5e.png">
