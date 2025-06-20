---
title: Mở rộng thanh điều hướng quản trị
keywords: plugin admin nav plugin quản trị điều hướng
tags: [plugin, admin, nav]
permalink: plugin_admin_nav

---

Thêm menu plugin vào màn hình quản trị.
Bằng cách triển khai EccubeNav như bên dưới, bạn có thể ghi đè/thêm menu.
Nếu thêm mới, menu sẽ được thêm vào cuối menu mục tiêu.
Hãy tham khảo cấu trúc định nghĩa nav của hệ thống chính.
Với plugin, menu chỉ hiển thị khi plugin được kích hoạt.
Thanh điều hướng quản trị của hệ thống chính được định nghĩa tại `/app/config/eccube/packages/eccube_nav.yaml`.

```php
class Nav implements EccubeNav
{
    public static function getNav()
    {
        return [
            'product' => [
                'children' => [
                    'hoge' => [
                        'name' => 'Thêm con vào Quản lý sản phẩm',
                        'url' => 'admin_homepage',
                    ],
                ],
            ],
            'piyo' => [
                'name' => 'Menu cấp 1 (thêm mới)',
                'icon' => 'fa-cube',
                'children' => [
                    'piyopiyo1' => [
                        'name' => 'Menu cấp 2 (không có con)',
                        'url' => 'admin_homepage',
                    ],
                    'piyopiyo2' => [
                        'name' => 'Menu cấp 2 (có con)',
                        'children' => [
                            'piyopiyopiyo1' => [
                                'name' => 'Menu cấp 3 - 1',
                                'url' => 'admin_homepage',
                            ],
                            'piyopiyopiyo2' => [
                                'name' => 'Menu cấp 3 - 2',
                                'url' => 'admin_homepage',
                            ],
                        ],
                    ],
                ],
            ],
        ];
    }
}
```
