---
title: Tuỳ biến luồng mua hàng
keywords: core tuỳ biến luồng mua hàng Cart Shopping
tags: [core, service, purchaseflow]
permalink: customize_service
folder: customize
---

## Tuỳ biến giỏ hàng [#2613](https://github.com/EC-CUBE/ec-cube/issues/2613){:target="_blank"}

Bằng cách triển khai class `CartItemComparator` hoặc `CartItemAllocator`, bạn có thể tuỳ biến hành vi khi thêm sản phẩm vào giỏ hàng.

![Sơ đồ chuỗi xử lý](http://www.plantuml.com/plantuml/png/hLNBRjD05DtFLyoobUY6PHP8A18IEoI-m3XJ6idDLAuBB3js7owrQ6cRD4MYfEJPHab3sqK90Jvc6CUVmSpu6JiHgOGLHHwFxxddtdFcUgLOG70PO-CLVWS0o2kwaSSbGyUQXdIuz0IA9o-H_gQeeXnK2WMnVcwWrGMtCg3ab98jj_fXV3TO140LGQfHnALrICqkjKRKil_SRtgjDYXX0q6z-7h5W7WvimlvzNXy-uEI3ZjqAAbIqwPaXv8ktIJUpIMhtumxVMOtnxqzyL3irYbfoS08Z9f7pEP17wcvHqs7clin33dZIu1A1IYO-8K6POagKuHo2L1ombbHqlVBzFT5feCA-tKAKe5mATsoP5YgHPmJ-SwhI843LKSAxzRC_GpvcIzg6Az1z_GhwrMZFN5J7W3PkXHGg6qUhwufkc9WFGTLUO_ISZzAmoxwYB7ESYckJFwEUttYZIm9r_Br3hUuK5T2Dy9_brAwVMOtt4hF5v1kcX4ijNQfLQRc9RMwKgSs9TUilCEEYTSwS6kZKBbk01wxOm8dMpIdolfVlFgs26bmmzcIqh54QtD7Hh4--Scat1pcb8n1kCDsX-xdPe93x4cnKZG3Jcq9gzsnGnjCq9x30w41EHTgdGkhclSB4ueXRHt1SNdWf_blMIi3qH3vpBjmlDy_sVjQAd6f083yapQDJfBVpZbi-bJJiEgxLF5lKPGXgMpqNlPqHaczNfMF5zOxdEdYe361fxA1lCFkjo7hVyfQrUsSkSDAR2jfrUWq9kTRPhY9Y_VKtJg8D8ap4jvNpgSS3BkfXlhNe0ldxRHo7Av2OsAy-aClvTIvWWb_qvp3KMb-qVH8G7Mdsadu-864hlWyUp0XwUnv2CtmT-3iCDVav_R5XgwkAElecORVyk6hQEg69dozcFBbb2zKrxiTiUsc68fMJvxq8-6t2oV--Fq5)

### Tách riêng các dòng sản phẩm giống nhau nhưng khác tuỳ chọn

Mặc định, các dòng sản phẩm trong giỏ sẽ được tách theo từng phân loại sản phẩm.
Ví dụ, khi tuỳ biến thêm tuỳ chọn sản phẩm như gói quà, bạn có thể triển khai `CartItemComparator` để tách dòng sản phẩm theo tuỳ chọn này.

``` php
<?php
namespace Eccube\Service\Cart;

use Eccube\Entity\CartItem;

/**
 * So sánh dòng sản phẩm theo phân loại và tuỳ chọn
 */
class ProductClassAndOptionComparator implements CartItemComparator
{
    /**
     * @param CartItem $Item1 Dòng 1
     * @param CartItem $Item2 Dòng 2
     * @return boolean true nếu là cùng dòng
     */
    public function compare(CartItem $Item1, CartItem $Item2)
    {
        $ProductClass1 = $Item1->getProductClass();
        $ProductClass2 = $Item2->getProductClass();
        $product_class_id1 = $ProductClass1 ? (string) $ProductClass1->getId() : null;
        $product_class_id2 = $ProductClass2 ? (string) $ProductClass2->getId() : null;

        if ($product_class_id1 === $product_class_id2) {
            // Cần tuỳ biến thêm ProductOption
            return $Item1->getProductOption()->getId() === $Item2->getProductOption()->getId();
        }
        return false;
    }
}

```

Để kích hoạt CartItemComparator, tạo file `app/config/eccube/packages/cart.yaml` và thêm định nghĩa:

```yaml
services:
    Eccube\Service\Cart\CartItemComparator:
      class: Eccube\Service\Cart\ProductClassAndOptionComparator

```

### Cho phép thêm sản phẩm có phương thức thanh toán khác nhau vào cùng giỏ

Ví dụ, có các phương thức giao hàng/phương thức thanh toán và sản phẩm như sau:

+ Phương thức giao hàng
    + A: Loại bán A/Thẻ tín dụng
    + B: Loại bán A/Thanh toán khi nhận
+ Sản phẩm
    + A: Loại bán A
    + B: Loại bán B

Ở EC-CUBE 3.0, nếu thêm sản phẩm A vào giỏ, sau đó thêm sản phẩm B sẽ báo lỗi "Không thể mua cùng lúc sản phẩm này".

Bằng cách triển khai `CartItemAllocator`, bạn có thể tách giỏ theo tiêu chí tuỳ ý (ví dụ: sản phẩm đặt trước, v.v.).

``` php
<?php
namespace Eccube\Service\Cart;

use Eccube\Entity\CartItem;

/**
 * Tách giỏ theo loại bán và sản phẩm đặt trước
 */
class SaleTypeAndReserveCartAllocator implements CartItemAllocator
{
    /**
     * Xác định mã giỏ cho sản phẩm
     *
     * @param CartItem $Item
     * @return string
     */
    public function allocate(CartItem $Item)
    {
        $ProductClass = $Item->getProductClass();
        if ($ProductClass && $ProductClass->getSaleType()) {
            $salesTypeId = (string) $ProductClass->getSaleType()->getId();
            // isReserveItem cần tuỳ biến thêm
            if ($ProductClass->isReserveItem()) {
                return $salesTypeId.':R' ;
            }
            return $salesTypeId;
        }
        throw new \InvalidArgumentException('ProductClass/SaleType not found');
    }
}

```

Để kích hoạt CartItemAllocator, tạo file `app/config/eccube/packages/cart.yaml` và thêm định nghĩa:

```yaml
services:
    Eccube\Service\Cart\CartItemAllocator:
      class: Eccube\Service\Cart\SaleTypeAndReserveCartAllocator

```

### Tuỳ biến luồng mua hàng [#2424](https://github.com/EC-CUBE/ec-cube/pull/2424){:target="_blank"}

Các xử lý tổng hợp, kiểm tra tồn kho... là các logic chung liên quan đến đơn hàng.
Trước đây, các xử lý này được cài đặt riêng lẻ ở nhiều nơi, gây khó khăn khi tuỳ biến hoặc tái sử dụng.

Từ EC-CUBE 4, các xử lý này được tách thành PurchaseFlow (điều khiển luồng) và Processor (xử lý từng bước), giúp tuỳ biến dễ dàng hơn.

#### Hoạt động tổng thể

![purchaseflow-activity](https://user-images.githubusercontent.com/8196725/28450154-7bd307a0-6e20-11e7-8827-9ee85c81136d.png)

#### Luồng xử lý tổng hợp

Ví dụ với giỏ hàng, các bước xử lý như sau:

- Tải giỏ hàng từ session
- Kiểm tra trạng thái hiện tại của từng dòng sản phẩm
    - Kiểm tra giới hạn bán
    - Kiểm tra tồn kho
    - Kiểm tra trạng thái hiển thị
    - ...
- Xử lý làm tròn số lượng theo kết quả kiểm tra
    - Giới hạn bán: giảm số lượng về đúng giới hạn
    - Hết hàng: xoá dòng sản phẩm
    - Không hiển thị: xoá dòng sản phẩm
    - ...
- Tổng hợp: tính tổng tiền, phí vận chuyển, phí xử lý...
- Kiểm tra trạng thái tổng thể của giỏ
    - Kiểm tra loại sản phẩm
    - Kiểm tra phương thức thanh toán
    - Kiểm tra vượt giới hạn số tiền mua
- Trả về lỗi nếu có
- Tổng hợp lại
    - Tính tổng tiền, phí vận chuyển, phí xử lý...

![default](https://user-images.githubusercontent.com/8196725/28610103-25570d30-7222-11e7-828c-a0a04e268df3.png)

#### Sơ đồ class

![default](https://user-images.githubusercontent.com/8196725/28611146-c9c6f83c-7225-11e7-9591-dc2e0e154cf5.png)

Vai trò các class chính:

##### ItemIHolderInterface

Interface đại diện cho danh sách dòng sản phẩm (Cart, Order).

##### ItemInterface

Interface đại diện cho từng dòng sản phẩm (CartItem, OrderItem).

##### PurchaseFlow

Class điều khiển toàn bộ luồng xử lý tổng hợp.
Có 2 hàm chính: [calculate()](https://github.com/EC-CUBE/ec-cube/pull/2424/files#diff-1d9b0d44b6269dc98b5c09f331ff0c41R48) và [purchase()](https://github.com/EC-CUBE/ec-cube/pull/2424/files#diff-1d9b0d44b6269dc98b5c09f331ff0c41R80).
Khi gọi, sẽ truyền Item và ItemHolder vào các Processor để xử lý tuần tự, trả về kết quả.

##### ItemValidator

Processor kiểm tra tính hợp lệ của từng dòng sản phẩm.

##### ItemHolderValidator

Processor kiểm tra tính hợp lệ của toàn bộ giỏ/đơn hàng.

##### ItemPreprocessor

Processor tiền xử lý cho từng dòng sản phẩm.

##### ItemHolderPreprocessor

Processor tiền xử lý cho toàn bộ giỏ/đơn hàng (tính thuế, phí vận chuyển...).

##### DiscountProcessor

Processor xử lý giảm giá (điểm thưởng, coupon...).

##### ItemHolderPostValidator

Processor kiểm tra hợp lệ cuối cùng cho giỏ/đơn hàng (ví dụ tổng tiền âm...).

##### PurchaseProcessor

Processor xử lý hoàn tất đơn hàng (cập nhật tồn kho, điểm thưởng...).

##### PurchaseContext

Class lưu trạng thái khi thực thi.

##### PurchaseFlowResult

Class lưu kết quả thực thi PurchaseFlow.

##### Processor

Tuỳ mục đích, kế thừa hoặc implement các interface/class sau:

| Class/Interface           | Mô tả                                              |
|--------------------------|---------------------------------------------------|
| ItemValidator            | Kiểm tra hợp lệ từng dòng (giá, trạng thái hiển thị...) |
| ItemHolderValidator      | Kiểm tra hợp lệ toàn bộ giỏ/đơn hàng (tồn kho, giới hạn bán...) |
| ItemPreprocessor         | Tiền xử lý từng dòng sản phẩm                      |
| ItemHolderPreprocessor   | Tiền xử lý toàn bộ giỏ/đơn hàng (thêm phí vận chuyển...) |
| DiscountProcessor        | Xử lý giảm giá (điểm thưởng, coupon...)            |
| ItemHolderPostValidator  | Kiểm tra hợp lệ cuối cùng cho giỏ/đơn hàng         |
| PurchaseProcessor        | Xử lý hoàn tất đơn hàng (cập nhật tồn kho, điểm thưởng...) |

#### Ví dụ triển khai Processor

`EmptyProcessor::process()` sẽ ghi log khi được gọi.

``` php
<?php

namespace Plugin\PurchaseProcessors\Processor;

use Eccube\Entity\ItemInterface;
use Eccube\Service\PurchaseFlow\ItemPreProcessor;
use Eccube\Service\PurchaseFlow\PurchaseContext;
use Eccube\Service\PurchaseFlow\ProcessResult;

class EmptyProcessor implements ItemPreProcessor
{
    /**
     * @param ItemInterface $item
     * @param PurchaseContext $context
     * @return ProcessResult
     */
    public function process(ItemInterface $item, PurchaseContext $context)
    {
        log_info('empty processor executed', [__METHOD__]);
        return ProcessResult::success();
    }
}

```

Nếu `ValidatableEmptyProcessor::validate()` ném ra `Eccube\Service\PurchaseFlow\InvalidItemException`, thì `ValidatableEmptyProcessor::handle()` sẽ được gọi và trả về `PurchaseFlowResult::warn()`.

``` php
<?php

namespace Plugin\PurchaseProcessors\Processor;

use Eccube\Entity\ItemInterface;
use Eccube\Service\PurchaseFlow\InvalidItemException;
use Eccube\Service\PurchaseFlow\PurchaseContext;
use Eccube\Service\PurchaseFlow\ItemValidator;

class ValidatableEmptyProcessor extends ItemValidator
{
    protected function validate(ItemInterface $item, PurchaseContext $context)
    {
        $error = false;
        if ($error) {
            throw new InvalidItemException('Lỗi ValidatableEmptyProcessor');
        }
    }

    protected function handle(ItemInterface $item, PurchaseContext $context)
    {
        $item->setQuantity(100);
    }
}

```

#### Kích hoạt Processor

Để kích hoạt Processor tự tạo, thêm định nghĩa vào `app/config/eccube/packages/purchaseflow.yaml` hoặc dùng annotation chỉ định flow.

##### Định nghĩa trong `purchaseflow.yaml`

```yaml
    eccube.purchase.flow.cart.item_processors:
        class: Doctrine\Common\Collections\ArrayCollection
        arguments:
            - #
                - '@Plugin\PurchaseProcessors\Processor\EmptyProcessor' # Thêm
                - '@Eccube\Service\PurchaseFlow\Processor\DisplayStatusValidator'
                - '@Eccube\Service\PurchaseFlow\Processor\SaleLimitValidator'
                - '@Eccube\Service\PurchaseFlow\Processor\DeliverySettingValidator'
                - '@Eccube\Service\PurchaseFlow\Processor\StockValidator'
                - '@Eccube\Service\PurchaseFlow\Processor\ProductStatusValidator'
                - '@Plugin\PurchaseProcessors\Processor\ValidatableEmptyProcessor' # Thêm
```

##### Chỉ định flow bằng annotation

Dùng annotation `@CartFlow`, `@ShoppingFlow`, `@OrderFlow` để chỉ định flow cần thêm Processor.

| Annotation    | Mô tả                                              |
|--------------|----------------------------------------------------|
| @CartFlow    | Thêm Processor vào PurchaseFlow của giỏ hàng        |
| @ShoppingFlow| Thêm Processor vào PurchaseFlow của luồng mua hàng  |
| @OrderFlow   | Thêm Processor vào PurchaseFlow của quản trị        |

```php
<?php

namespace Customize\Service\PurchaseFlow\Processor;

use Eccube\Annotation\CartFlow;
use Eccube\Annotation\OrderFlow;
use Eccube\Annotation\ShoppingFlow;
use Eccube\Entity\ItemInterface;
use Eccube\Service\PurchaseFlow\PurchaseContext;
use Eccube\Service\PurchaseFlow\ItemValidator;

/**
 * Kích hoạt Processor cho tất cả các flow
 *
 * @CartFlow
 * @ShoppingFlow
 * @OrderFlow
 */
class SampleValidator extends ItemValidator
{
    protected function validate(ItemInterface $item, PurchaseContext $context)
    {
        // Bỏ qua
    }

    protected function handle(ItemInterface $item, PurchaseContext $context)
    {
        // Bỏ qua
    }
}
```
