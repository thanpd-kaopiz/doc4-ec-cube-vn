---
layout: single
title: Di chuyển từ 4.1 lên 4.2
keywords: cách cập nhật
tags: [quickstart, getting_started]
permalink: update-41-42
summary : Mô tả về di chuyển từ EC-CUBE 4.1 lên 4.2.
---

Giải thích về di chuyển từ EC-CUBE 4.1 lên 4.2.

Tổng hợp các phần cần chuyển mã để EC-CUBE 4.2 tương thích với EC-CUBE bản chính và một số plugin chính thức.

- [Lộ trình EC-CUBE 4.2](https://github.com/EC-CUBE/ec-cube/issues/5356){:target="_blank"}
- [Hỗ trợ Symfony5](https://github.com/EC-CUBE/ec-cube/pull/5353){:target="_blank"}
- [Plugin Mail Magazine](https://github.com/EC-CUBE/mail-magazine-plugin/compare/4.n){:target="_blank"}

## Thay đổi mã plugin

4.2 là phiên bản không tương thích với 4.1.

Do không thể đồng tồn tại mã nguồn, cần triển khai như một plugin riêng biệt so với plugin hỗ trợ 4.0/4.1.

### composer.json

Thay đổi mã plugin trong composer.json.

Dưới đây là ví dụ sửa đổi của plugin Mail Magazine.

```diff
{
-  "name": "ec-cube/mailmagazine4",
+  "name": "ec-cube/mailmagazine42",
  "version": "4.2.0",
  "description": "Plugin Mail Magazine",
  "type": "eccube-plugin",
  "require": {
    "ec-cube/plugin-installer": "~0.0.6 || ^2.0"
  },
  "extra": {
-    "code": "MailMagazine4"
+    "code": "MailMagazine42"
  }
}
```

### Thay đổi namespace

Thay đổi namespace để phù hợp với mã plugin.

Dưới đây là ví dụ sửa đổi của plugin Mail Magazine.

```diff
<?php
- namespace Plugin\MailMagazine4;
+ namespace Plugin\MailMagazine42;

use Eccube\Common\EccubeNav;

class MailMagazineNav implements EccubeNav
{

```

## Tương thích Symfony5.4

Không thể bao quát hết các thay đổi trong Symfony5.4, nếu có vấn đề không được đề cập, hãy tham khảo tài liệu UPGRADE của Symfony.

- [UPGRADE-5.0.md](https://github.com/symfony/symfony/blob/5.4/UPGRADE-5.0.md){:target="_blank"}

### Liên quan đến Form

#### FormExtension

Cần định nghĩa kiểu trả về của getExtendedTypes.

```diff
    /**
     * Return the class of the type being extended.
     */
-    public static function getExtendedTypes()
+    public static function getExtendedTypes(): iterable
    {
        return [EntryType::class];
    }
```

### Liên quan đến Repository

#### ManagerRegistry

Namespace của ManagerRegistry đã thay đổi.

Thay đổi thành `Doctrine\Persistence\ManagerRegistry`.

```diff
<?php

namespace Plugin\MailMagazine4\Repository;

- use Doctrine\Common\Persistence\ManagerRegistry;
+ use Doctrine\Persistence\ManagerRegistry; 
use Eccube\Repository\AbstractRepository;
use Plugin\MailMagazine4\Entity\MailMagazineSendHistory;
use Eccube\Doctrine\Query\Queries;
```

### Liên quan đến twig

#### Sử dụng if trong vòng lặp for

Không thể sử dụng if trong vòng lặp for. Hãy sử dụng filter.

```diff
{% raw %}
- {% for f in searchForm if f.vars.eccube_form_options.auto_render %}
+ {% for f in searchForm|filter(f => f.vars.eccube_form_options.auto_render) %}
{% endraw %}
```

### Liên quan đến SwiftMailer

#### Chuyển sang SymfonyMailer

Thư viện gửi mail đã chuyển từ SwiftMailer sang SymfonyMailer.

Nếu sử dụng trực tiếp SwiftMailer, hãy chuyển sang triển khai với SymfonyMailer.

```diff
-        $message = (new \Swift_Message())
-            ->setSubject('['.$this->BaseInfo->getShopName().'] '.$formData['mail_subject'])
-            ->setFrom([$this->BaseInfo->getEmail01() => $this->BaseInfo->getShopName()])
-            ->setTo([$Order->getEmail()])
-            ->setBcc($this->BaseInfo->getEmail01())
-            ->setReplyTo($this->BaseInfo->getEmail03())
-            ->setReturnPath($this->BaseInfo->getEmail04())
-            ->setBody($formData['tpl_data']);
+        $message = (new Email())
+            ->subject('['.$this->BaseInfo->getShopName().'] '.$formData['mail_subject'])
+            ->from(new Address($this->BaseInfo->getEmail01(), $this->BaseInfo->getShopName()))
+            ->to($Order->getEmail())
+            ->bcc($this->BaseInfo->getEmail01())
+            ->replyTo($this->BaseInfo->getEmail03())
+            ->returnPath($this->BaseInfo->getEmail04())
+            ->text($formData['tpl_data']);
```

Tham khảo thêm sự khác biệt tại đây.

https://github.com/EC-CUBE/ec-cube/pull/5353/commits/ff6a6962736c87fe8e9b7427ba2cbebbb3000c43

### Liên quan đến Event

#### Thay đổi chữ ký của EventDispatcher

Thứ tự tham số của $eventDispatcher->dispatch() đã thay đổi.

Nếu tự định nghĩa hook point, hãy thay đổi thứ tự tham số.

```diff

-        $this->eventDispatcher->dispatch(EccubeEvents::FRONT_ENTRY_INDEX_INITIALIZE, $event);
+        $this->eventDispatcher->dispatch($event, EccubeEvents::FRONT_ENTRY_INDEX_INITIALIZE);

```

### Liên quan đến tham số

#### Tham số env

Không thể sử dụng bool hoặc số trong tham số env.

Nếu sử dụng tham số env trong services.yaml, hãy thay đổi thành chuỗi.

```diff
parameters:

-    env(ECCUBE_FORCE_SSL): false
+    env(ECCUBE_FORCE_SSL): '0'

-    env(ECCUBE_2FA_EXPIRE): 14
+    env(ECCUBE_2FA_EXPIRE): '14'
```

### Mã kiểm tra

#### setUp/tearDown

Cần định nghĩa kiểu trả về cho phương thức setUp/tearDown.

```diff

-   setUp()
+   setUp(): void

-   tearDown()
+   tearDown(): void

```

## Tương thích Bootstrap5

Đã cập nhật Bootstrap lên 5.0.

Dưới đây là một phần nội dung thay đổi. Xem chi tiết tại tài liệu dưới đây.

https://getbootstrap.jp/docs/5.0/migration/

### Biến data có tiền tố bs

Các biến data sử dụng trong bootstrap như modal đã có tiền tố bs.

```diff

- data-keyword
+ data-bs-keyword

- data-dismiss
 data-bs-dismiss

- data-toggle
+ data-bs-toggle

```

## Nút đóng

Tên lớp của nút đóng đã thay đổi.

```diff

- .close 
+ .btn-close

```

### text-right, text-left

Tên lớp căn phải, căn trái đã thay đổi.

```diff

- .text-left
+ .text-start

- .text-right
+ .text-end

```

## Các thay đổi khác

### Các hàm và tính năng bị xóa khác
