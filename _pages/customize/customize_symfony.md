---
title: Tuỳ biến với chức năng của Symfony
keywords: core tuỳ biến Symfony
tags: [core, symfony]
permalink: customize_symfony
folder: customize

---

## Tổng quan

EC-CUBE được phát triển dựa trên Symfony và Doctrine.
Vì vậy, bạn có thể sử dụng các cơ chế mở rộng mà Symfony và Doctrine cung cấp.

Dưới đây là một số cơ chế mở rộng tiêu biểu và cách triển khai.

## Symfony Event

Bạn có thể sử dụng hệ thống sự kiện của Symfony.

### Tạo event listener hiển thị "hello world"

Tạo file `HelloListener.php` trong `app/Customize/EventListener`.

```php
<?php

namespace Customize\EventListener;

use Symfony\Component\EventDispatcher\EventSubscriberInterface;
use Symfony\Component\HttpKernel\Event\FilterResponseEvent;
use Symfony\Component\HttpKernel\KernelEvents;

class HelloListener implements EventSubscriberInterface
{
    public function onResponse(FilterResponseEvent $event)
    {
        echo 'hello world';
    }

    public static function getSubscribedEvents()
    {
        return [
            KernelEvents::RESPONSE => 'onResponse',
        ];
    }
}
```

Sau khi tạo, hiển thị bất kỳ trang nào sẽ thấy "hello world".

Nếu không hiển thị, hãy xoá cache bằng lệnh `bin/console cache:clear --no-warmup`.
Có thể kiểm tra các event listener đã đăng ký bằng `bin/console debug:event-dispatcher`.

Tham khảo thêm:

- [The HttpKernel Component](https://symfony.com/doc/current/components/http_kernel.html){:target="_blank"}
- [Events and Event Listeners](https://symfony.com/doc/current/event_dispatcher.html){:target="_blank"}
- [Built-in Symfony Events](https://symfony.com/doc/current/reference/events.html){:target="_blank"}

## Command

Bạn có thể tạo command chạy từ `bin/console`.

### Tạo command hiển thị "hello world"

Tạo file `HelloCommand.php` trong `app/Customize/Command`.

```php
<?php

namespace Customize\Command;

use Symfony\Component\Console\Command\Command;
use Symfony\Component\Console\Input\InputInterface;
use Symfony\Component\Console\Output\OutputInterface;
use Symfony\Component\Console\Style\SymfonyStyle;

class HelloCommand extends Command
{
    // Tên command
    protected static $defaultName = 'acme:hello';

    protected function execute(InputInterface $input, OutputInterface $output)
    {
        $io = new SymfonyStyle($input, $output);

        // Hiển thị hello world
        $io->success('hello world');
    }
}
```

- `$defaultName` là tên command.
- `$io->success('hello world')` để hiển thị hello world.

Sau khi tạo, có thể chạy bằng lệnh:

```bash
$ bin/console acme:hello

 [OK] hello world
```

Nếu không nhận diện được command, hãy xoá cache bằng `bin/console cache:clear --no-warmup`.

Tham khảo thêm:

- [Console Commands](https://symfony.com/doc/current/console.html){:target="_blank"}

## Doctrine Event

Bạn có thể sử dụng hệ thống sự kiện của Doctrine.

### Tạo event listener thêm "Chào mừng" vào tên shop

Tạo file `HelloEventSubscriber.php` trong `app/Customize/Doctrine/EventSubscriber`.

```php
<?php

namespace Customize\Doctrine\EventSubscriber;

use Doctrine\Common\EventSubscriber;
use Doctrine\Common\Persistence\Event\LifecycleEventArgs;
use Doctrine\ORM\Events;
use Eccube\Entity\BaseInfo;

class HelloEventSubscriber implements EventSubscriber
{
    public function getSubscribedEvents()
    {
        return [Events::postLoad];
    }

    public function postLoad(LifecycleEventArgs $args)
    {
        $entity = $args->getObject();
        if ($entity instanceof BaseInfo) {
            $shopName = $entity->getShopName();
            $shopName = 'Chào mừng '.$shopName.' đến với shop';
            $entity->setShopName($shopName);
        }
    }
}
```

Sau khi tạo, mở trang chủ sẽ thấy "Chào mừng [Tên shop] đến với shop".

Nếu không hiển thị, hãy xoá cache bằng lệnh `bin/console cache:clear --no-warmup`.

Tham khảo thêm:

- [The Event System](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/events.html){:target="_blank"}
- [Doctrine Event Listeners and Subscribers](https://symfony.com/doc/current/doctrine/event_listeners_subscribers.html){:target="_blank"}

※ [Doctrine Event Listeners and Subscribers](https://symfony.com/doc/current/doctrine/event_listeners_subscribers.html){:target="_blank"} hướng dẫn cấu hình trong `services.yaml`, nhưng EC-CUBE sẽ tự động đăng ký event listener, không cần cấu hình thêm.

## Sử dụng Bundle của Symfony

TODO

