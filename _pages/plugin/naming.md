---
title: Quy tắc đặt tên khuyến nghị cho plugin
keywords: plugin quy tắc đặt tên plugin quy tắc đặt tên
tags: [plugin, naming, conventions]
permalink: plugin_naming_conventions

---

### Mã plugin

Để tránh trùng lặp, khuyến nghị đặt theo dạng `[TênVendor][TênPlugin]`
Viết theo camelCase

```
AcmeCategoryContent
```

### Tên bảng

※ Nếu tạo bảng riêng cho plugin

`plg_[mã plugin dạng snake_case]_xxx`

```php
use Doctrine\ORM\Mapping as ORM;

/**
 * Config
 *
 * @ORM\Table(name="plg_acme_category_content_config")
 * @ORM\Entity(repositoryClass="Plugin\AcmeCategoryContent\Repository\ConfigRepository")
 */
class Config
```

### Tên cột bảng và getter/setter

※ Nếu dùng trait để thêm cột

`[mã plugin dạng snake_case]_xxx`
getter/setter viết theo camelCase

```php
use Eccube\Annotation\EntityExtension;
use Doctrine\ORM\Mapping as ORM;

/**
 * @EntityExtension("Eccube\Entity\Customer")
 */
trait CustomerTrait
{
    /**
     * @ORM\Column(name="acme_category_content_xxx" type="integer", nullable=true)
     */
    private $acme_category_content_xxx;

    public function getAcmeCategoryContentXxx()
    {
    }

    public function setAcmeCategoryContentXxx($xxx)
    {
    }
}
```

### Routing

#### Màn hình front

`[mã plugin dạng snake_case]_xxx`

```php
class PageController extends AbstractController
{
    /**
     * @Route("/acme_category_content/page", name="acme_category_content_page")
     * @Template("@AcmeCategoryContent/page.twig")
     */
    public function index(Request $request)
```

#### Màn hình quản trị

Thêm `admin_` ở đầu

`admin_[mã plugin dạng snake_case]_xxx`

```php
class ConfigController extends AbstractController
{
    /**
     * @Route("/%eccube_admin_route%/acme_category_content/config", name="admin_acme_category_content_config")
     * @Template("@AcmeCategoryContent/admin/config.twig")
     */
    public function index(Request $request)
```

### URL

`/[mã plugin dạng snake_case]/xxx/xxx`

```php
class ConfigController extends AbstractController
{
    /**
     * @Route("/%eccube_admin_route%/acme_category_content/config", name="acme_category_content_admin_config")
     * @Template("@AcmeCategoryContent/admin/config.twig")
     */
    public function index(Request $request)
```

### Field thêm bằng FormExtension

`[mã plugin dạng snake_case]_xxx`

```php
class XxxExtention extends AbstractTypeExtension
{
    public function buildForm(FormBuilderInterface $builder, array $options)
    {
        $builder->add('acme_category_content_name', TextType::class);

```

### ID, class dùng trong html

`[mã plugin dạng snake_case]_xxx`

```html
<div id="acme_category_content_info" class="card rounded border-0 mb-4">
```

### Tên command

`[mã plugin dạng snake_case]:xxx:xxx`

```php
class XxxCommand extends Command
{
    protected static $defaultName = 'acme_category_content:xxx:yyy';
```

### File ngôn ngữ

`[mã plugin dạng snake_case].xxx.xxx`

```yaml
# nav
acme_category_content.admin.nav.category: Danh sách nội dung danh mục

# flash messages
acme_category_content.admin.save.success: Đã đăng ký.
acme_category_content.admin.save.failed: Đăng ký thất bại.
```

Sau phần mã plugin, các quy tắc đặt tên khác tuân theo [quy tắc đặt tên của EC-CUBE](https://github.com/EC-CUBE/ec-cube/pull/3593)

### Tham số

`[mã plugin dạng snake_case].xxx.xxx`

```yaml
parameters:
  acme_category_content.xxx: 1

services:
  acme_category_content.log.formatter.line:
      class: Monolog\Formatter\LineFormatter
      arguments: ...
```
