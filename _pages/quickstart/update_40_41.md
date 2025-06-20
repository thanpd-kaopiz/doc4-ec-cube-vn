---
layout: single
title: Di chuyển từ 4.0 lên 4.1
keywords: cách cập nhật
tags: [quickstart, getting_started]
permalink: update-40-41
summary : Mô tả về di chuyển từ EC-CUBE 4.0 lên 4.1.
---

Giải thích về di chuyển từ EC-CUBE 4.0 lên 4.1.

Tổng hợp các phần cần chuyển mã để EC-CUBE 4.1 tương thích với EC-CUBE bản chính và một số plugin chính thức.

- [Lộ trình EC-CUBE 4.1](https://github.com/EC-CUBE/ec-cube/issues/4603){:target="_blank"}
- [Nhánh GitHub 4.1](https://github.com/EC-CUBE/ec-cube/tree/4.1){:target="_blank"}
- [Plugin Web API: Tương thích Symfony 4.4](https://github.com/EC-CUBE/eccube-api4/pull/106){:target="_blank"}
- [Plugin Đánh giá sản phẩm: Tương thích Symfony 4.4](https://github.com/EC-CUBE/ProductReview-plugin/pull/55){:target="_blank"}

## Tương thích Composer2.0

Cần thay đổi composer.json của plugin để tương thích với Composer 2.0.

### name

`ec-cube/<PluginCode viết thường>`

PluginCode cần tương ứng với namespace của plugin và phải viết thường.

```php
<?php
namespace Plugin\ExamplePlugin;

// Với namespace trên, name trong composer.json sẽ là ec-cube/exampleplugin.
```

### require

Cần bao gồm `ec-cube/plugin-installer: "~0.0.6 || ^2.0"`

```json
  "require": {
    "ec-cube/plugin-installer": "~0.0.6 || ^2.0"
  },
```

### Ví dụ thay đổi composer.json

```diff
{
-   "name": "ec-cube/ExamplePlugin",
+   "name": "ec-cube/exampleplugin",
-  "version": "1.0.0",
+  "version": "2.0.0",
  "description": "Plugin mẫu",
  "type": "eccube-plugin",
  "require": {
-     "ec-cube/plugin-installer": "~0.0.6"
+     "ec-cube/plugin-installer": "~0.0.6 || ^2.0"
   },
  "extra": {
    "code": "ExamplePlugin"
  }
}
```

Xem chi tiết về nội dung sửa đổi tại [Issue trên GitHub](https://github.com/EC-CUBE/ec-cube/issues/4737){:target="_blank"}.

Tính đến ngày 09/12/2020, phía package-api của Owner's Store mà EC-CUBE giao tiếp chưa hỗ trợ 4.1.

Việc kiểm tra cài đặt plugin trên 4.1 có thể thực hiện tương tự như trên 4.0 thông qua [kiểm tra cài đặt qua Owner's Store](plugin_mock_package_api).

## Tương thích Symfony4.4

Không thể bao quát hết các thay đổi trong Symfony4.4, nếu có vấn đề không được đề cập, hãy tham khảo tài liệu UPGRADE của Symfony.

- [UPGRADE-4.0.md](https://github.com/symfony/symfony/blob/4.4/UPGRADE-4.0.md){:target="_blank"}

Ngoài ra, để duy trì tính tương thích giữa EC-CUBE4.0 và EC-CUBE4.1, có một số phần không sửa đổi các thông báo deprecation.

※ Có thể xuất hiện thông báo `User Deprecated: xxx` trong log, nhưng không ảnh hưởng đến hoạt động.

Dù thực hiện sửa đổi này, EC-CUBE vẫn hoạt động trên cả Symfony3.4/4.4, ngoại trừ mục [Lấy container trong mã kiểm tra](#コンテナの取得).

### Liên quan đến Form

#### Xác thực Form

Không thể gọi `isValid()` một mình. Hãy kiểm tra bằng `isSubmitted() && isValid()`.

```diff
- if ($form->isValid()) {
+ if ($form->isSubmitted() && $form->isValid()) {
     // do something...
 }
```

#### FormExtension

Thêm phương thức `getExtendedTypes`.

Để duy trì tính tương thích với EC-CUBE4.0.x(Symfony3.4), cần giữ lại phương thức `getExtendedType`.

```diff
    /**
     * {@inheritdoc}
     */
    public function getExtendedType()
    {
        return EntryType::class;
    }
+
+    /**
+     * Return the class of the type being extended.
+     */
+    public static function getExtendedTypes(): iterable
+    {
+        return [EntryType::class];
+    }
```

### Liên quan đến Translator

#### message.[locale].yaml

Nếu sử dụng biến, cần đặt trong dấu nháy đơn.

```diff
- common.password_sample: 半角英数記号%min%〜%max%文字
+ common.password_sample: '半角英数記号%min%〜%max%文字'
```

### Liên quan đến Log

#### Cài đặt monolog

Nếu có ghi đè `channels`, hãy xóa.

```diff
monolog:
    channels: ['sample_payment']
    handlers:
        sample_payment:
            type: fingers_crossed
            action_level: info
            passthru_level: info
            handler: sample_payment_rotating_file
            channels: ['sample_payment']
-            channels: ['!event', '!doctrine']
        sample_payment_rotating_file:
            type: rotating_file
            max_files: 60
            path: '%kernel.logs_dir%/%kernel.environment%/sample_payment.log'
            formatter: eccube.log.formatter.line
            level: debug
```

### Liên quan đến Container

#### Chỉ định interface khi injection

Khi sử dụng constructor injection hoặc method injection, nếu chỉ định class cụ thể, hãy chỉ định interface.

```diff
- public function __construct(Session $session)
+ public function __construct(SessionInterface $session)

- public function index(Request $request, $page_no = 1, Paginator $paginator)
+ public function index(Request $request, $page_no = 1, PaginatorInterface $paginator)
```

#### Hạn chế lấy dịch vụ từ container

Ngoại trừ một số dịch vụ (như doctrine), không thể lấy dịch vụ bằng `$container->get(Hoge::class)`.

Hãy sử dụng injection hoặc thiết lập dịch vụ là public trong services.yaml.

※ Tuy nhiên, nếu thay đổi thành public, sẽ ảnh hưởng đến hiệu suất. Nên sử dụng injection.

Ví dụ về sử dụng injection:

```diff
-
- public function index()
- {
-     $customerRepository = $this->container->get(CustomerRepository::class);
-     $customerRepository->find(1);
- }

+
+ public function __construct(CustomerRepository $customerRepository)
+ {
+     $this->customerRepository = $customerRepository;
+ }
+
+ public function index()
+ {
+     $this->customerRepository->find(1);
+ }
```

Ví dụ về services.yaml:

```diff
+ services:
+      Plugin\SamplePayment\Service\HogeService
+          public: true
```

Trong PluginManager, không thể sử dụng injection. Khi lấy Repository, hãy sử dụng mã sau.

```diff
- $pageRepository = $container->get(PageRepository::class);
+ $entityManager = $container->get('doctrine')->getManager();
+ $pageRepository = $entityManager->getRepository(Page::class);
```

### Mã kiểm tra

#### Lấy container

Container đã được thay đổi từ biến thành viên sang biến lớp.

```diff
    public function setUp()
    {
        parent::setUp();

-       $this->helper = $this->container->get(OrderHelper::class);
+       $this->helper = self::$container->get(OrderHelper::class);
    }
```

#### Thông điệp xác thực

Một số thông điệp xác thực đã thay đổi. Các bài kiểm tra tự động kiểm tra thông điệp xác thực có thể cần sửa đổi. Không cần sửa mã sản phẩm.

### Các thay đổi khác

#### Thay đổi cách lấy thông tin khách hàng khi mua hàng không đăng ký

Khi mua hàng không đăng ký, thông tin khách hàng được lưu trong session, nhưng định dạng lưu trữ đã thay đổi từ entity sang mảng. Nếu có tùy chỉnh để lấy hoặc thay đổi thông tin khách hàng khi mua hàng không đăng ký, cần sửa đổi.

```diff
- $NonMember = $this->session->get('eccube.front.shopping.nonmember')
+ $NonMember = $this->orderHelper->getNonMember('eccube.front.shopping.nonmember')
```

[Xem chi tiết về sửa đổi do Serializable của Customer](https://github.com/EC-CUBE/ec-cube/commit/9a84daf16d92a5129eb169ac14f9b219e81c5d90){:target="_blank"}

## Tương thích WebAPI

EC-CUBE 4.1 đóng gói Plugin Web API, cho phép sử dụng Web API khi cài đặt EC-CUBE.

Dữ liệu có thể lấy qua Web API theo danh sách cho phép, do đó, Entity được thêm bởi plugin không thể lấy mặc định.

Để cho phép lấy Entity được thêm, hãy định nghĩa component với tag `eccube.api.allow_list`.

ID dịch vụ nên có dạng `[PluginCode].api.allow_list`.

Ví dụ, trong plugin quản lý nhà sản xuất, thêm định nghĩa ArrayObject sau vào services.yaml của plugin.

```yaml
services:
    maker4.api.allow_list:
        class: ArrayObject
        tags: ['eccube.api.allow_list']
        arguments:
            - #
                Eccube\Entity\Product: ['maker_url', 'Maker']
                Plugin\Maker4\Entity\Maker: ['id', 'name', 'sort_no', 'create_date', 'update_date']
```

Xem chi tiết tại [tài liệu plugin Web API](https://doc.ec-cube.net/eccube-api4/customize/allow_list){:target="_blank"}.

### Các hàm và tính năng bị xóa khác

#### Application.php

Eccube\Application đã bị xóa. Do đó, ServiceProvider cũng bị loại bỏ. Hãy sử dụng Container của Symfony.

##### Ví dụ thay đổi khi lấy session bằng app['session']

**Đến 4.0**

``` php
    public function index(Application $app, Request $request)
    {
        // Lấy session từ SessionServiceProvider
        $session = $app['session'];
    }

 ```

**Từ 4.1 trở đi**

 ```php
    use Symfony\Component\HttpFoundation\Session\SessionInterface;

    /** @var SessionInterface */
    protected $session

    /**
     * @param SessionInterface $session
     */
    public function __construct(SessionInterface $session)
    {
        $this->session = $session;
    }

    public function index(Request $request)
    {
        // Lấy session qua constructor injection
        $session = $this->session;
    }
 ```


## Kiểm tra cài đặt plugin qua Owner's Store

EC-CUBE 4.1 yêu cầu tương thích với Composer2.
Do đó, endpoint khi cài đặt plugin qua Owner's Store đã thay đổi.
Nếu muốn kiểm tra trên EC-CUBE 4.1 beta3 trở về trước, có thể chuyển sang endpoint tương thích với Composer2 bằng cách thiết lập biến môi trường sau trong EC-CUBE.
Nhánh 4.1 mới nhất trên GitHub không cần thực hiện điều này.

```
ECCUBE_PACKAGE_API_URL=https://package-api-c2.ec-cube.net
```
