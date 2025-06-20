---
layout: single
title: Tuỳ biến Controller
keywords: core tuỳ biến controller
tags: [core, controller]
permalink: customize_controller
folder: customize
---

---

## Thêm routing mới

Bạn có thể thêm routing mới cho site bằng cách đặt file class có annotation `@Route` vào thư mục `./app/Customize/Controller/`.

Ví dụ đơn giản nhất dưới đây sẽ thêm routing để khi truy cập `http://siteURL/sample` sẽ hiển thị "Hello sample page !".

### File Controller

./app/Customize/Controller/SamplePageController.php

```php
<?php

namespace Customize\Controller;

use Sensio\Bundle\FrameworkExtraBundle\Configuration\Method;
use Sensio\Bundle\FrameworkExtraBundle\Configuration\Route;
use Symfony\Component\HttpFoundation\Response;

class SamplePageController
{
    /**
     * @Method("GET")
     * @Route("/sample")
     */
    public function testMethod()
    {
        return new Response('Hello sample page !');
    }
}
```

## Sử dụng file template

Bạn có thể sử dụng file template Twig bằng annotation `@Template`.
Ví dụ sau sẽ hiển thị "Hello EC-CUBE !" khi truy cập `http://siteURL/sample`.

### File Controller

```php
<?php

namespace Customize\Controller;

use Sensio\Bundle\FrameworkExtraBundle\Configuration\Method;
use Sensio\Bundle\FrameworkExtraBundle\Configuration\Route;
use Sensio\Bundle\FrameworkExtraBundle\Configuration\Template;
use Symfony\Component\HttpFoundation\Response;

class SamplePageController
{
    /**
     * @Method("GET")
     * @Route("/sample")
     * @Template("Sample/index.twig")
     */
    public function testMethod()
    {
        return ['name' => 'EC-CUBE'];
    }
}
```

### File Twig

./app/template/default/Sample/index.twig

```twig
<h3>Hello {{ name }} !</h3>
```

## Một số mẹo tuỳ biến

### Nhận tham số từ URL

Bạn có thể nhận tham số từ URL như `http://siteURL/sample/1` bằng cách khai báo `{id}` trong @Route và nhận biến `$id` cùng tên.

```php
    /**
     * @Method("GET")
     * @Route("/sample/{id}")
     */
    public function testMethod($id)
    {
        return new Response('Parameter is '.$id);
    }
```

### Tạo link đến routing vừa thêm

Để tạo link đến routing vừa thêm từ template khác, bạn cần đặt tên cho routing bằng tham số `name` trong @Route.

```php
    /**
     * @Method("GET")
     * @Route("/sample/{id}", name="sample_page")
     */
    public function testMethod($id)
    {
        return new Response('Parameter is '.$id);
    }
```

Từ file template khác, bạn có thể tạo link như sau (có thể truyền tham số):

```twig
{% raw %}
<a href="{{ url('sample_page', { id : 2}) }}">Link đến trang Sample</a>
{% endraw %}
```

### Ghi đè routing sẵn có của EC-CUBE

Để ghi đè routing sẵn có, chỉ cần định nghĩa routing mới với cùng path và name.
Ví dụ sau sẽ ghi đè trang "Về chúng tôi".

```php
    /**
     * @Method("GET")
     * @Route("/help/about", name="help_about")
     */
    public function testMethod()
    {
        return new Response('Overwrite /help/about page');
    }
```

### Thêm routing cho trang quản trị

Để chỉ cho phép user đã đăng nhập admin truy cập, hãy dùng `/%eccube_admin_route%` trong path.

```php
    /**
     * @Method("GET")
     * @Route("/%eccube_admin_route%/sample")
     */
    public function testMethod()
    {
        return new Response('admin page');
    }
```

Tương tự, routing cho UserData dùng `/%eccube_user_data_route%`.

### Redirect

Kế thừa `AbstractController` và dùng hàm `redirectToRoute` để redirect.
Ví dụ sau sẽ redirect về trang "Về chúng tôi" khi có truy cập.

```php
    /**
     * @Method("GET")
     * @Route("/sample")
     */
    public function testMethod()
    {
        return $this->redirectToRoute('help_about');
    }
```

Dùng `forwardToRoute` để chuyển xử lý sang controller khác mà không redirect.

### Sử dụng service trong Controller

Kế thừa `AbstractController` để sử dụng các service thường dùng. Ví dụ sau dùng EntityManager để lấy Entity sản phẩm.

```php
<?php

namespace Customize\Controller;

use Eccube\Controller\AbstractController;
use Eccube\Entity\Product;
use Sensio\Bundle\FrameworkExtraBundle\Configuration\Method;
use Sensio\Bundle\FrameworkExtraBundle\Configuration\Route;
use Symfony\Component\HttpFoundation\Response;

class SamplePageController extends AbstractController
{
    /**
     * @Method("GET")
     * @Route("/sample")
     */
    public function testMethod()
    {
        /** @var Product $product */
        $product = $this->entityManager->getRepository('Eccube\Entity\Product')->find(1);

        return new Response('Product is '.$product->getName());
    }
}
```

Các service khác có thể dùng khi kế thừa AbstractController, xem tại `./src/Eccube/Controller/AbstractController.php`.

#### Sử dụng service không có trong AbstractController

Bạn có thể inject service vào constructor. Ví dụ sau lấy tên shop từ BaseInfo.

```php
<?php

namespace Customize\Controller;

use Sensio\Bundle\FrameworkExtraBundle\Configuration\Method;
use Sensio\Bundle\FrameworkExtraBundle\Configuration\Route;
use Symfony\Component\HttpFoundation\Response;

class SamplePageController
{
    /** @var \Eccube\Entity\BaseInfo */
    protected $BaseInfo;

    /**
     * SamplePageController constructor.
     * @param \Eccube\Repository\BaseInfoRepository $baseInfoRepository
     */
    public function __construct(\Eccube\Repository\BaseInfoRepository $baseInfoRepository)
    {
        $this->BaseInfo = $baseInfoRepository->get();
    }

    /**
     * @Method("GET")
     * @Route("/sample")
     */
    public function testMethod()
    {
        return new Response('Shop name is '.$this->BaseInfo->getShopName());
    }
}
```

### Tạo controller không cần hiển thị màn hình

Ngay cả khi controller không trả về view, bạn vẫn phải trả về đối tượng Response (không dùng `exit()`).

Bạn cũng có thể chỉ định mã response và header.

```php
    /**
     * @Method("GET")
     * @Route("/sample")
     */
    public function testMethod()
    {
        return new Response(
          '',
          Response::HTTP_OK,
          array('Content-Type' => 'text/plain; charset=utf-8')
        );
    }
```

```
$ curl -D - http://siteURL/sample
HTTP/1.1 200 OK
Content-Type: text/plain; charset=utf-8
```

## Tham khảo

EC-CUBE 4 sử dụng cơ chế Controller của Symfony.
Tham khảo thêm các cách tuỳ biến khác tại tài liệu Symfony:

[Controller](https://symfony.com/doc/current/controller.html){:target="_blank"}