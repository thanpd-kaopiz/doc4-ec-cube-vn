---
title: Tuỳ biến trạng thái đơn hàng
keywords: core tuỳ biến trạng thái đơn hàng OrderStatus
tags: [core, OrderStatus]
permalink: customize_order_state_machine
folder: customize
---

## Mở rộng trạng thái đơn hàng [#3325](https://github.com/EC-CUBE/ec-cube/pull/3325){:target="_blank"}

![Sơ đồ trạng thái đơn hàng](./images/spec/order-statemachine.png)

Vui lòng xem thêm [Luồng xử lý trạng thái đơn hàng](/spec_order).

### Cách mở rộng cơ bản

Sử dụng [Symfony Workflow Component](https://symfony.com/doc/current/components/workflow.html) để triển khai.

Để thêm xử lý khi chuyển trạng thái, hãy cài đặt event khi chuyển trạng thái.
Các trạng thái được định nghĩa tại [app/config/eccube/packages/order_state_machine.php](https://github.com/EC-CUBE/ec-cube/blob/4.0/app/config/eccube/packages/order_state_machine.php).

Bằng cách cài đặt event, bạn có thể thêm xử lý tuỳ ý khi chuyển trạng thái đơn hàng.

| Từ trạng thái                | Đến trạng thái | Sự kiện                                        |
|------------------------------|---------------|------------------------------------------------|
| Đã nhận mới                  | Đã thanh toán | `workflow.order.transition.pay`                |
| Đã nhận mới, Đã thanh toán   | Đang xử lý    | `workflow.order.transition.packing`            |
| Đã nhận mới, Đang xử lý, Đã thanh toán | Huỷ | `workflow.order.transition.cancel`             |
| Huỷ                         | Đang xử lý    | `workflow.order.transition.back_to_in_progress`|
| Đã nhận mới, Đang xử lý, Đã thanh toán | Đã giao | `workflow.order.transition.ship`              |
| Đã giao                     | Trả hàng      | `workflow.order.transition.return`             |
| Trả hàng                    | Đã giao       | `workflow.order.transition.cancel_return`      |

- Ví dụ) Thêm xử lý khi trả hàng
    - Cài đặt `EventSubscriberInterface` để nhận event `workflow.order.transition.return`.

```php
use Symfony\Component\EventDispatcher\EventSubscriberInterface;
use Eccube\Entity\Order;
use Symfony\Component\Workflow\Event\Event;

class SampleTransitionListener implements EventSubscriberInterface
{
    /**
     * Xử lý khi trả hàng.
     *
     * @param Event $event
     */
    public function onReturn(Event $event)
    {
        /* @var Order $Order */
        $Order = $event->getSubject();
        .... /* Triển khai xử lý */
    }

    /**
     * {@inheritdoc}
     */
    public static function getSubscribedEvents()
    {
        return ['workflow.order.transition.return' => 'onReturn'];
    }
}
```

### Tham khảo

Các event mặc định của EC-CUBE được triển khai tại [src/Eccube/Service/OrderStateMachine.php](https://github.com/EC-CUBE/ec-cube/blob/4.0/src/Eccube/Service/OrderStateMachine.php).

[Using Events](https://symfony.com/doc/current/workflow/usage.html#using-events){:target="_blank"}
