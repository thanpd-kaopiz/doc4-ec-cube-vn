---
layout: single
title: Di chuyển từ 4.2 lên 4.3
keywords: cách cập nhật
tags: [quickstart, getting_started]
permalink: update-42-43
summary : Mô tả về di chuyển từ EC-CUBE 4.2 lên 4.3.
---

Giải thích về di chuyển từ EC-CUBE 4.2 lên 4.3.

Tổng hợp các phần cần chuyển mã để EC-CUBE 4.3 tương thích với EC-CUBE bản chính và một số plugin chính thức.

- [Lộ trình EC-CUBE 4.3](https://github.com/EC-CUBE/ec-cube/issues/6069){:target="_blank"}
- [Tương thích Symfony6](https://github.com/EC-CUBE/ec-cube/pull/6073){:target="_blank"}
- [Plugin Đánh giá sản phẩm: Tương thích Symfony 6](https://github.com/EC-CUBE/ProductReview-plugin/pull/93){:target="_blank"}
- [Plugin API: Tương thích Symfony 6](https://github.com/EC-CUBE/eccube-api4/pull/164){:target="_blank"}
- [Plugin Mail Magazine: Tương thích Symfony 6](https://github.com/EC-CUBE/mail-magazine-plugin/pull/146){:target="_blank"}

## Về tính tương thích của plugin

EC-CUBE 4.2 và 4.3 đảm bảo tính tương thích của plugin.

Bằng cách thực hiện các sửa đổi trong tài liệu này, có thể chạy plugin trên cả hai phiên bản.

Nếu chạy plugin trên cả hai phiên bản, không cần thay đổi mã plugin trong `composer.json`.

## Tương thích PHP8.3

Trong EC-CUBE 4.3, yêu cầu hệ thống PHP là 8.1〜8.3.

Các cảnh báo không khuyến khích trong PHP7.4〜8.1, đặc biệt là liên quan đến tham số kiểu, sẽ trở thành lỗi và không hoạt động.

Dưới đây là một ví dụ về lỗi.

```
$ bin/console
PHP Fatal error:  Declaration of Eccube\Kernel::getCacheDir() must be compatible with Symfony\Component\HttpKernel\Kernel::getCacheDir(): string in /path/to/ec-cube/src/Eccube/Kernel.php on line 68
Symfony\Component\ErrorHandler\Error\FatalError^ {#45
  #message: "Compile Error: Declaration of Eccube\Kernel::getCacheDir() must be compatible with Symfony\Component\HttpKernel\Kernel::getCacheDir(): string"
  #code: 0
  #file: "./src/Eccube/Kernel.php"
  #line: 68
  -error: array:4 [
    "type" => 64
    "message" => "Declaration of Eccube\Kernel::getCacheDir() must be compatible with Symfony\Component\HttpKernel\Kernel::getCacheDir(): string"
    "file" => "/path/to/ec-cube/src/Eccube/Kernel.php"
    "line" => 68
  ]
}

```

Nếu gặp lỗi như vậy, có thể giải quyết bằng cách chỉ định tham số kiểu cho tham số và giá trị trả về.

Dưới đây là ví dụ sửa lỗi trên.

```diff
class Kernel extends BaseKernel
{

...

-    public function getCacheDir()
+    public function getCacheDir(): string
    {
        return $this->getProjectDir().'/var/cache/'.$this->environment;
    }
```

Về các thay đổi không tương thích của PHP, hãy tham khảo hướng dẫn di chuyển trên php.net.

- https://www.php.net/manual/ja/migration82.php
- https://www.php.net/manual/ja/migration83.php

## Tương thích Symfony6

Không thể bao quát hết các thay đổi trong Symfony6, nếu có vấn đề không được đề cập, hãy tham khảo tài liệu UPGRADE của Symfony.

- [UPGRADE-6.0.md](https://github.com/symfony/symfony/blob/6.4/UPGRADE-6.0.md){:target="_blank"}

Ngoài ra, để duy trì tính tương thích giữa EC-CUBE4.2 và EC-CUBE4.3, có một số phần không sửa đổi các thông báo deprecation.

※ Có thể xuất hiện thông báo `User Deprecated: xxx` trong log, nhưng không ảnh hưởng đến hoạt động.

Dù thực hiện sửa đổi này, EC-CUBE vẫn hoạt động trên cả EC-CUBE 4.2/4.3.

### Liên quan đến Session

#### Bỏ injection của SessionInterface

Injection bằng `SessionInterface` đã bị loại bỏ.

Khi sử dụng `Session`, hãy lấy từ `RequestStack`.

```diff
- use Symfony\Component\HttpFoundation\Session\SessionInterface;
+ use Symfony\Component\HttpFoundation\RequestStack; 
...

- public function index(SessionInterface $session)
+ public function index(RequestStack $requestStack)
{
+    $session = $requestStack->getSession();    
    $session->get('key');
}
```

Nếu không cần chạy trên EC-CUBE 4.2 (chỉ hỗ trợ 4.3), có thể sử dụng `Eccube\Session\Session`.

```diff
- use Symfony\Component\HttpFoundation\Session\SessionInterface;
+ use Eccube\Session\Session; 
...

- public function index(SessionInterface $session)
+ public function index(Session $session)
{
    $session->get('key');
}
```

### Liên quan đến Container

#### Hạn chế lấy dịch vụ từ container

Khi lấy dịch vụ bằng `$container->get(Hoge::class)`, cần chỉ định là service locator.

Ngoài ra, khi sử dụng container class, hãy sử dụng `Psr\Container\ContainerInterface` thay vì `Symfony\Component\DependencyInjection\ContainerInterface`.

```diff
- use Symfony\Component\DependencyInjection\ContainerInterface;
+ use Psr\Container\ContainerInterface;

...

public function __construct(ContainerInterface $container)
{
    $this->customerRepository = $this->container->get(CustomerRepository::class);
}

```

Ví dụ về services.yaml:

```
services
    Eccube\Controller\SampleController:
        arguments:
            $container: !service_locator
                Eccube\Repository\CustomerRepository: '@Eccube\Repository\CustomerRepository'
```

Việc gọi dịch vụ trong PluginManager cũng bị ảnh hưởng bởi thay đổi này.

Có thể lấy dịch vụ từ container như sau.

```
// ManagerRegistory
- $container->get('doctrine');
- $container->get(ManagerRegistry::class);

// EntityManager
- $container->get('doctrine.orm.default_entity_manager');
- $container->get('doctrine.orm.entity_manager');
- $container->get(EntityManagerInterface::class);

// EccubeConfig
- $container->get(EccubeConfig::class);
```

#### Thay đổi cách lấy tham số

Không thể lấy tham số bằng `$container->getParameter('key')`.

Thay vào đó, hãy sử dụng `Eccube\Common\EccubeConfig`.

```diff
- use Symfony\Component\DependencyInjection\ContainerInterface;
+ use Eccube\Common\EccubeConfig; 

...

- public function index(ContainerInterface $container)
+ public function index(EccubeConfig $eccubeConfig)
{
-    $projectDir = $container->getParameter('kernel.project_dir');
+    $projectDir = $eccubeConfig->get('kernel.project_dir');
}
```

### Liên quan đến PasswordEncoder

#### Bỏ PasswordEncoder

`PasswordEncoder` đã bị loại bỏ, thay vào đó sử dụng `PasswordHaser`.

Khi sử dụng `PasswordHaser` để mã hóa mật khẩu, mã sẽ như sau.

```diff
- use Symfony\Component\Security\Core\Encoder\EncoderFactoryInterface;
+ use Symfony\Component\PasswordHasher\Hasher\UserPasswordHasherInterface;

...

public function __construct(
-    EncoderFactoryInterface $encoderFactory,
+    UserPasswordHasherInterface $passwordHasher
) {
-    $this->encoderFactory = $encoderFactory;
+    $this->passwordHasher = $passwordHasher;
}

...

- $encoder = $this->encoderFactory->getEncoder($Customer);

if ($Customer->getPlainPassword() !== $this->eccubeConfig['eccube_default_password']) {
-    $Customer->setPassword($encoder->encodePassword($Customer->getPlainPassword(), $Customer->getSalt()));
+    $Customer->setPassword($this->passwordHasher->hashPassword($Customer, $Customer->getPlainPassword()));
}
```

Nếu tự triển khai PasswordEncoder, hãy thay đổi để sử dụng PasswordHasher như sau.

```diff
- class UserPasswordEncoder implements UserPasswordEncoderInterface
+ class UserPasswordEncoder
```

```diff
Plugin\Api42\EventListener\UserResolveListener:
    arguments:
        - '@Eccube\Security\Core\User\MemberProvider'
-        - '@Plugin\Api42\Security\Core\Encoder\UserPasswordEncoder'
+        - '@Symfony\Component\PasswordHasher\Hasher\UserPasswordHasherInterface'
```

Nếu thay thế bằng `@Symfony\Component\PasswordHasher\Hasher\UserPasswordHasherInterface` và hoạt động, có thể xóa PasswordEncoder.

#### Tự động cập nhật thuật toán mã hóa mật khẩu

Bằng cách sử dụng `PasswordHaser`, thuật toán mã hóa mật khẩu sẽ tự động cập nhật.

Kiểm tra thuật toán sử dụng sẽ được thực hiện khi người dùng đăng nhập, nếu cần cập nhật thuật toán, mật khẩu sẽ được mã hóa lại bằng thuật toán mới và lưu vào DB.

Nếu sử dụng thuật toán AUTH_MAGIC truyền thống của EC-CUBE, thuật toán sẽ được cập nhật khi đăng nhập. Thuật toán mới sẽ bao gồm giá trị salt trong mật khẩu đã mã hóa, do đó, cột salt trong dtb_member/customer sẽ không còn sử dụng.

Tham khảo thêm [Password Hashing and Verification](https://symfony.com/doc/current/security/passwords.html){:target="_blank"}.

### Mã kiểm tra

#### Không thể kiểm tra bằng expectOutputRegex

Khi kiểm tra phản hồi tải xuống csv bằng expectOutputRegex, có thể không hoạt động.

Có thể lấy nội dung xuất ra bằng `$client->getInternalResponse()->getContent()`, hãy sử dụng cách này.

```diff
...

- $this->expectOutputRegex("/{$review->getTitle()}/");

$this->client->request(
    'POST',
    $this->generateUrl('product_review_admin_product_review_download')
);

$this->assertTrue($this->client->getResponse()->isSuccessful());

+ $content = $this->client->getInternalResponse()->getContent();
+ $content = mb_convert_encoding($content, 'UTF-8', 'SJIS-win'); // Nếu cần, chuyển đổi mã hóa
+ $this->assertMatchesRegularExpression("/{$review->getTitle()}/", $content);
```

#### Muốn kiểm tra session

Nếu muốn kiểm tra giá trị session, `static::getContainer()->get('session')` không hoạt động.

Hãy sử dụng `Eccube\Tests\Web\AbstractWebTestCase::createSession`.

```diff

- $session = static::getContainer()->get('session');
+ $session = $this->createSession($this->client)
$outPut = $session->getFlashBag()->get('eccube.admin.success');

```

#### Thông điệp xác thực

Một số thông điệp xác thực đã thay đổi. Các bài kiểm tra tự động kiểm tra thông điệp xác thực có thể cần sửa đổi. Không cần sửa mã sản phẩm.

### Các thay đổi khác

## Kiểm tra cài đặt plugin qua Owner's Store

Endpoint khi cài đặt plugin qua Owner's Store đã thay đổi.

Hiện tại (31/01/2024) chưa được triển khai, nhưng dự kiến sẽ là endpoint dưới đây.

```
ECCUBE_PACKAGE_API_URL=https://package-api-c2.ec-cube.net/v43
```

## Thay đổi purchaseflow.yaml
Từ 4.3, định dạng của purchaseflow.yaml đã thay đổi.
Thay đổi từ cách "thiết lập phương thức từ cha đến con" sang cách "thiết lập phương thức cho cha nào".
Ngoài ra, có thể thay đổi thứ tự thực thi trong purchaseflow bằng cách thiết lập priority.
Xem chi tiết tại [đây](https://github.com/EC-CUBE/ec-cube/pull/5147).
### Ví dụ sửa đổi
Lấy ví dụ về thay đổi của ProductStatusValidator.<br>
Dưới đây là định nghĩa trong 4.2.
```yaml
# 4.2_purchaseflow.yaml
eccube.purchase.flow.cart:
    class: Eccube\Service\PurchaseFlow\PurchaseFlow
    calls:
        - [setFlowType, ['cart']]
        - [setItemValidators, ['@eccube.purchase.flow.cart.item_validators']]
            
eccube.purchase.flow.cart.item_validators:
    class: Doctrine\Common\Collections\ArrayCollection
    arguments:
        - #
            - '@Eccube\Service\PurchaseFlow\Processor\ProductStatusValidator' # Kiểm tra trạng thái công khai của sản phẩm
```

Tiếp theo là định nghĩa trong 4.3.
```yaml
# 4.3_purchaseflow.yaml
eccube.purchase.flow.cart:
    class: Eccube\Service\PurchaseFlow\PurchaseFlow
    calls:
        - [ setFlowType, [ 'cart' ] ]

eccube.purchase.flow.item.validator.product.status.validator: # Kiểm tra trạng thái công khai của sản phẩm
    class: Eccube\Service\PurchaseFlow\Processor\ProductStatusValidator
    tags:
        - { name: eccube.item.validator, flow_type: cart, priority: 900 }
```

### Hỗ trợ cả hai phiên bản 4.2/4.3 trong plugin

Khi sử dụng purchase flow trong plugin và muốn hỗ trợ cả hai phiên bản 4.2/4.3, hãy làm theo hướng dẫn dưới đây.

#### Khi chỉ định bằng annotation

Các annotation như @CartFlow vẫn có thể sử dụng trong 4.3.

priority luôn là 0 và processor sẽ được thêm vào cuối danh sách như trước.

#### Khi chỉ định bằng tệp yaml

Nếu ghi đè cài đặt hiện có bằng tệp yaml, hãy chuyển sang cài đặt bằng tệp php và phân nhánh theo phiên bản EC-CUBE.

Dưới đây là ví dụ sửa đổi khi thực hiện SampleProcessor trước các processor hiện có.

SampleProcessor
```php
<?php

namespace Plugin\Sample\Service\PurchaseFlow;

use Eccube\Entity\ItemInterface;
use Eccube\Service\PurchaseFlow\ItemValidator;
use Eccube\Service\PurchaseFlow\PurchaseContext;

class SampleProcessor extends ItemValidator
{
    protected function validate(ItemInterface $item, PurchaseContext $context)
    {
        dump(123);
    }
}
```

Cài đặt trong 4.2
```yaml
# Plugin/Sample/Resource/config/services.yaml

eccube.purchase.flow.cart.item_validators:
  class: Doctrine\Common\Collections\ArrayCollection
  arguments:
    - #
      - '@Plugin\Sample\Service\PurchaseFlow\SampleProcessor' # SampleProcessor
      - '@Eccube\Service\PurchaseFlow\Processor\DeliverySettingValidator' # Kiểm tra cài đặt giao hàng
      - '@Eccube\Service\PurchaseFlow\Processor\ProductStatusValidator' # Kiểm tra trạng thái công khai của sản phẩm
      - '@Eccube\Service\PurchaseFlow\Processor\PriceChangeValidator' # Phát hiện thay đổi giá sản phẩm
      - '@Eccube\Service\PurchaseFlow\Processor\StockValidator' # Kiểm tra tồn kho
      - '@Eccube\Service\PurchaseFlow\Processor\SaleLimitValidator' # Kiểm tra giới hạn bán hàng
      - '@Eccube\Service\PurchaseFlow\Processor\ClassCategoryValidator' # Kiểm tra trạng thái công khai của loại sản phẩm
```

Cài đặt hỗ trợ cả hai phiên bản 4.2/4.3

Xóa services.yaml và tạo services.php. Phân nhánh theo phiên bản EC-CUBE trong services.php.
```php
# Plugin/Sample/Resource/config/services.php

<?php

namespace Symfony\Component\DependencyInjection\Loader\Configurator;

use Doctrine\Common\Collections\ArrayCollection;
use Eccube\Common\Constant;
use Plugin\Sample\Service\PurchaseFlow\SampleProcessor;

return function(ContainerConfigurator $containerConfigurator) {
    $services = $containerConfigurator->services();

    // 4.3
    if (version_compare(Constant::VERSION, '4.3', '>=')) {
        $services
            ->set(SampleProcessor::class)
            ->tag('eccube.item.validator', ['flow_type' => 'cart', 'priority' => 2000]); // Thực hiện trước, priority lớn hơn các processor hiện có
    // 4.2
    } else {
        $services
            ->set(SampleProcessor::class);

        $services
            ->set('eccube.purchase.flow.cart.item_validators')
            ->class(ArrayCollection::class)
            ->args([[service('Plugin\Sample\Service\PurchaseFlow\SampleProcessor'), # SampleProcessor
                service('Eccube\Service\PurchaseFlow\Processor\DeliverySettingValidator'), # Kiểm tra cài đặt giao hàng
                service('Eccube\Service\PurchaseFlow\Processor\ProductStatusValidator'), # Kiểm tra trạng thái công khai của sản phẩm
                service('Eccube\Service\PurchaseFlow\Processor\PriceChangeValidator'), # Phát hiện thay đổi giá sản phẩm
                service('Eccube\Service\PurchaseFlow\Processor\StockValidator'), # Kiểm tra tồn kho
                service('Eccube\Service\PurchaseFlow\Processor\SaleLimitValidator'), # Kiểm tra giới hạn bán hàng
                service('Eccube\Service\PurchaseFlow\Processor\ClassCategoryValidator'), # Kiểm tra trạng thái công khai của loại sản phẩm
            ]]);
    }
};
```
