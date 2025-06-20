---
title: Danh sách URL đối tượng kiểm thử
permalink: /penetration-testing/testing/manual_inspection_urls
---
Tổng hợp danh sách URL của EC-CUBE dựa trên output của lệnh `bin/console debug:router`.
Hãy sử dụng để kiểm tra xem đã kiểm thử đầy đủ khi thăm dò thủ công hoặc quét động chưa.

Danh sách URL có thể import vào OWASP ZAP qua `Import → Import a Containing URLs` [tại đây](https://raw.githubusercontent.com/nanasess/ec-cube4-penetration-testing/use-zap/zap/containing_urls.txt?token=AAGHEY5QKWZBN7VQNY2NRJ27MBGPW).

Lưu ý: Hiện đang được cập nhật
{: .notice}

| URL                                                                                | Bắt buộc nhập tiếng Nhật | POST (đang cập nhật) | Chuyển trang bằng mode | Upload file | Khó kiểm thử |
|------------------------------------------------------------------------------------|------------------------|----------------------|-----------------------|-------------|--------------|
| https://ec-cube/                                                                   |                        |                      |                       |             |              |
| https://ec-cube/admin                                                              |                        |                      |                       |             |              |
| https://ec-cube/admin/                                                             |                        |                      |                       |             |              |
| https://ec-cube/admin/change_password                                              |                        |        ○             |                       |             |              |
| https://ec-cube/admin/content                                                      |                        |                      |                       |             |              |
| https://ec-cube/admin/content/block                                                |                        |                      |                       |             |              |
| https://ec-cube/admin/content/block/1                                              |                        |                      |                       |             |              |
| https://ec-cube/admin/content/block/1/delete                                       |                        |        ○             |                       |             |      ○       |
| https://ec-cube/admin/content/block/1/edit                                         |                        |        ○             |                       |             |              |
| https://ec-cube/admin/content/block/new                                            |                        |        ○             |                       |             |              |
| https://ec-cube/admin/content/cache                                                |                        |        ○             |                       |             |              |
| https://ec-cube/admin/content/css                                                  |                        |        ○             |                       |             |              |
| https://ec-cube/admin/content/file_delete                                          |                        |        ○             |                       |             |      ○       |
| https://ec-cube/admin/content/file_delete?select_file=/assets                      |                        |                      |                       |             |      ○       |
| https://ec-cube/admin/content/file_download                                        |                        |                      |                       |             |              |
| https://ec-cube/admin/content/file_download?select_file=%2Fbbb.html                |                        |                      |                       |             |              |
| https://ec-cube/admin/content/file_manager                                         |                        |        ○             |                       |      ○      |              |
| https://ec-cube/admin/content/file_view                                            |                        |                      |                       |             |              |
| https://ec-cube/admin/content/file_view?file=%2Fbbb.html                           |                        |                      |                       |             |              |
| https://ec-cube/admin/content/js                                                   |                        |        ○             |                       |             |              |
| https://ec-cube/admin/content/layout                                               |                        |                      |                       |             |              |
| https://ec-cube/admin/content/layout/1                                             |                        |                      |                       |             |              |
| https://ec-cube/admin/content/layout/1/delete                                      |                        |        ○             |                       |             |      ○       |
| https://ec-cube/admin/content/layout/1/edit                                        |                        |        ○             |                       |             |              |
| https://ec-cube/admin/content/layout/1/preview                                     |                        |                      |                       |             |              |
| https://ec-cube/admin/content/layout/new                                           |                        |        ○             |                       |             |              |
| https://ec-cube/admin/content/layout/view_block                                    |                        |                      |                       |             |              |
| https://ec-cube/admin/content/maintenance                                          |                        |        ○             |                       |             |              |
| https://ec-cube/admin/content/news                                                 |                        |                      |                       |             |              |
| https://ec-cube/admin/content/news/1                                               |                        |                      |                       |             |              |
| https://ec-cube/admin/content/news/1/delete                                        |                        |        ○             |                       |             |      ○       |
| https://ec-cube/admin/content/news/1/edit                                          |                        |        ○             |                       |             |              |
| https://ec-cube/admin/content/news/new                                             |                        |        ○             |                       |             |              |
| https://ec-cube/admin/content/news/page/1                                          |                        |                      |                       |             |              |
| https://ec-cube/admin/content/page                                                 |                        |                      |                       |             |              |
| https://ec-cube/admin/content/page/1                                               |                        |                      |                       |             |              |
| https://ec-cube/admin/content/page/1/delete                                        |                        |        ○             |                       |             |      ○       |
| https://ec-cube/admin/content/page/1/edit                                          |                        |        ○             |                       |             |              |
| https://ec-cube/admin/content/page/new                                             |                        |        ○             |                       |             |              |
| https://ec-cube/admin/customer                                                     |                        |        ○             |                       |             |              |
| https://ec-cube/admin/customer/1                                                   |                        |                      |                       |             |              |
| https://ec-cube/admin/customer/1/delete                                            |                        |        ○             |                       |             |      ○       |
| https://ec-cube/admin/customer/1/delivery                                          |                        |                      |                       |             |              |
| https://ec-cube/admin/customer/1/delivery/1/delete                                 |                        |        ○             |                       |             |      ○       |
| https://ec-cube/admin/customer/1/delivery/1/edit                                   |                        |        ○             |                       |             |              |
| https://ec-cube/admin/customer/1/delivery/2                                        |                        |        ○             |                       |             |              |
| https://ec-cube/admin/customer/1/delivery/2/delete                                 |                        |        ○             |                       |             |      ○       |
| https://ec-cube/admin/customer/1/delivery/2/edit                                   |           ○            |        ○             |                       |             |              |
| https://ec-cube/admin/customer/1/delivery/new                                      |           ○            |        ○             |                       |             |              |
| https://ec-cube/admin/customer/1/edit                                              |           ○            |        ○             |                       |             |              |
| https://ec-cube/admin/customer/1/resend                                            |                        |        ○             |                       |             |              |
| https://ec-cube/admin/customer/export                                              |                        |                      |                       |             |              |
| https://ec-cube/admin/customer/new                                                 |           ○            |        ○             |                       |             |              |
| https://ec-cube/admin/customer/page                                                |                        |                      |                       |             |              |
| https://ec-cube/admin/customer/page/1                                              |                        |        ○             |                       |             |              |
| https://ec-cube/admin/customer/page/1?resume=1                                     |                        |        ○             |                       |             |              |
| https://ec-cube/admin/login                                                        |                        |        ○             |                       |             |              |
| https://ec-cube/admin/logout                                                       |                        |        ○             |                       |             |              |
| https://ec-cube/admin/order                                                        |                        |        ○             |                       |             |              |
| https://ec-cube/admin/order/1                                                      |                        |                      |                       |             |              |
| https://ec-cube/admin/order/1/edit                                                 |           ○            |        ○             |                       |             |              |
| https://ec-cube/admin/order/1/mail                                                 |                        |                      |                       |             |              |
| https://ec-cube/admin/order/bulk_delete                                            |                        |        ○             |                       |             |      ○       |
| https://ec-cube/admin/order/csv_template                                           |                        |                      |                       |             |              |
| https://ec-cube/admin/order/export                                                 |                        |                      |                       |             |              |
| https://ec-cube/admin/order/export/order                                           |                        |                      |                       |             |              |
| https://ec-cube/admin/order/export/pdf                                             |                        |                      |                       |             |              |
| https://ec-cube/admin/order/export/pdf/download                                    |                        |                      |                       |             |              |
| https://ec-cube/admin/order/export/pdf?ids%5B%5D=3                                 |                        |                      |                       |             |              |
| https://ec-cube/admin/order/export/shipping                                        |                        |                      |                       |             |              |
| https://ec-cube/admin/order/mail/view                                              |                        |                      |                       |             |              |
| https://ec-cube/admin/order/new                                                    |           ○            |        ○             |                       |             |              |
| https://ec-cube/admin/order/page/1                                                 |                        |                      |                       |             |              |
| https://ec-cube/admin/order/search/customer/html                                   |                        |                      |                       |             |              |
| https://ec-cube/admin/order/search/customer/html/page/1                            |                        |                      |                       |             |              |
| https://ec-cube/admin/order/search/customer/id                                     |                        |        ○             |                       |             |              |
| https://ec-cube/admin/order/search/order_item_type                                 |                        |                      |                       |             |              |
| https://ec-cube/admin/order/search/product                                         |                        |                      |                       |             |              |
| https://ec-cube/admin/order/search/product/page/1                                  |                        |                      |                       |             |              |
| https://ec-cube/admin/order/shipping_csv_upload                                    |                        |                      |                       |             |              |
| https://ec-cube/admin/order?order_status_id=1                                      |                        |                      |                       |             |              |
| https://ec-cube/admin/order?order_status_id=4                                      |                        |                      |                       |             |              |
| https://ec-cube/admin/order?resume=1                                               |                        |                      |                       |             |              |
| https://ec-cube/admin/product                                                      |                        |                      |                       |             |              |
| https://ec-cube/admin/product/bulk/product-status/1                                |                        |                      |                       |             |              |
| https://ec-cube/admin/product/category                                             |                        |                      |                       |             |              |
| https://ec-cube/admin/product/category/1                                           |                        |                      |                       |             |              |
| https://ec-cube/admin/product/category/1/delete                                    |           ○            |                      |                       |             |      ○       |
| https://ec-cube/admin/product/category/1/edit                                      |                        |                      |                       |             |              |
| https://ec-cube/admin/product/category/export                                      |                        |                      |                       |             |              |
| https://ec-cube/admin/product/category/sort_no/move                                |                        |                      |                       |             |              |
| https://ec-cube/admin/product/category_csv_upload                                  |                        |                      |                       |             |              |
| https://ec-cube/admin/product/class_category                                       |                        |                      |                       |             |              |
| https://ec-cube/admin/product/class_category/1                                     |                        |                      |                       |             |              |
| https://ec-cube/admin/product/class_category/1/1                                   |                        |                      |                       |             |              |
| https://ec-cube/admin/product/class_category/1/1/delete                            |                        |                      |                       |             |      ○       |
| https://ec-cube/admin/product/class_category/1/1/edit                              |                        |                      |                       |             |              |
| https://ec-cube/admin/product/class_category/1/1/visibility                        |                        |                      |                       |             |              |
| https://ec-cube/admin/product/class_category/1/2                                   |                        |                      |                       |             |              |
| https://ec-cube/admin/product/class_category/1/2/edit                              |                        |                      |                       |             |              |
| https://ec-cube/admin/product/class_category/1/2/visibility                        |                        |                      |                       |             |              |
| https://ec-cube/admin/product/class_category/1/3                                   |                        |                      |                       |             |              |
| https://ec-cube/admin/product/class_category/1/3/edit                              |                        |                      |                       |             |              |
| https://ec-cube/admin/product/class_category/1/3/visibility                        |                        |                      |                       |             |              |
| https://ec-cube/admin/product/class_category/sort_no/move                          |                        |                      |                       |             |              |
| https://ec-cube/admin/product/class_name                                           |                        |                      |                       |             |              |
| https://ec-cube/admin/product/class_name/1/delete                                  |                        |                      |                       |             |      ○       |
| https://ec-cube/admin/product/class_name/1/edit                                    |                        |                      |                       |             |              |
| https://ec-cube/admin/product/class_name/sort_no/move                              |                        |                      |                       |             |              |
| https://ec-cube/admin/product/classes/1/load                                       |                        |                      |                       |             |              |
| https://ec-cube/admin/product/csv_template                                         |                        |                      |                       |             |              |
| https://ec-cube/admin/product/csv_template/1                                       |                        |                      |                       |             |              |
| https://ec-cube/admin/product/csv_template/category                                |                        |                      |                       |             |              |
| https://ec-cube/admin/product/csv_template/product                                 |                        |                      |                       |             |              |
| https://ec-cube/admin/product/export                                               |                        |                      |                       |             |              |
| https://ec-cube/admin/product/page                                                 |                        |                      |                       |             |              |
| https://ec-cube/admin/product/page/1                                               |                        |                      |                       |             |              |
| https://ec-cube/admin/product/product                                              |                        |                      |                       |             |              |
| https://ec-cube/admin/product/product/1                                            |                        |                      |                       |             |              |
| https://ec-cube/admin/product/product/1/copy                                       |                        |                      |                       |             |              |
| https://ec-cube/admin/product/product/1/delete                                     |                        |                      |                       |             |      ○       |
| https://ec-cube/admin/product/product/1/display                                    |                        |                      |                       |             |              |
| https://ec-cube/admin/product/product/1/edit                                       |                        |                      |                       |             |              |
| https://ec-cube/admin/product/product/class                                        |                        |                      |                       |             |              |
| https://ec-cube/admin/product/product/class/1                                      |                        |                      |                       |             |              |
| https://ec-cube/admin/product/product/class/1/clear                                |                        |                      |                       |             |              |
| https://ec-cube/admin/product/product/class/1/clear?return_product_list=0          |                        |                      |                       |             |              |
| https://ec-cube/admin/product/product/class/1?return_product_list=0                |                        |                      |                       |             |              |
| https://ec-cube/admin/product/product/class/2                                      |                        |                      |                       |             |              |
| https://ec-cube/admin/product/product/class/2?return_product_list=0                |                        |                      |                       |             |              |
| https://ec-cube/admin/product/product/image/add                                    |                        |                      |                       |      ○      |              |
| https://ec-cube/admin/product/product/new                                          |                        |                      |                       |             |              |
| https://ec-cube/admin/product/product_csv_upload                                   |                        |                      |                       |             |              |
| https://ec-cube/admin/product/tag                                                  |                        |                      |                       |             |              |
| https://ec-cube/admin/product/tag/1/delete                                         |                        |                      |                       |             |      ○       |
| https://ec-cube/admin/product/tag/sort_no/move                                     |                        |                      |                       |             |              |
| https://ec-cube/admin/sale_chart                                                   |                        |                      |                       |             |              |
| https://ec-cube/admin/search_customer                                              |                        |                      |                       |             |              |
| https://ec-cube/admin/search_nonstock                                              |                        |                      |                       |             |              |
| https://ec-cube/admin/setting                                                      |                        |                      |                       |      ○      |              |
| https://ec-cube/admin/setting/shop                                                 |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/shop/csv                                             |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/shop/csv/1                                           |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/shop/csv/2                                           |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/shop/csv/4                                           |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/shop/csv/5                                           |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/shop/delivery                                        |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/shop/delivery/1                                      |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/shop/delivery/1/delete                               |                        |                      |                       |             |      ○       |
| https://ec-cube/admin/setting/shop/delivery/1/edit                                 |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/shop/delivery/1/visibility                           |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/shop/delivery/2                                      |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/shop/delivery/new                                    |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/shop/delivery/sort_no/move                           |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/shop/mail                                            |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/shop/mail/1                                          |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/shop/mail/preview                                    |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/shop/payment                                         |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/shop/payment/1                                       |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/shop/payment/1/delete                                |                        |                      |                       |             |      ○       |
| https://ec-cube/admin/setting/shop/payment/1/edit                                  |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/shop/payment/1/visible                               |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/shop/payment/image/add                               |                        |                      |                       |      ○      |              |
| https://ec-cube/admin/setting/shop/payment/new                                     |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/shop/payment/sort_no/move                            |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/shop/tax                                             |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/shop/tax/1/delete                                    |                        |                      |                       |             |      ○       |
| https://ec-cube/admin/setting/shop/tax/new                                         |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/system                                               |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/system/authority                                     |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/system/log                                           |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/system/masterdata                                    |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/system/masterdata/Eccube-Entity-Master-Work          |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/system/masterdata/Eccube-Entity-Master-Work/edit     |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/system/member                                        |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/system/member/1                                      |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/system/member/1/delete                               |                        |                      |                       |             |      ○       |
| https://ec-cube/admin/setting/system/member/1/down                                 |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/system/member/1/edit                                 |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/system/member/1/up                                   |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/system/member/new                                    |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/system/security                                      |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/system/system                                        |                        |                      |                       |             |              |
| https://ec-cube/admin/setting/system/system/phpinfo                                |                        |                      |                       |             |              |
| https://ec-cube/admin/shipping                                                     |                        |                      |                       |             |              |
| https://ec-cube/admin/shipping/1                                                   |                        |                      |                       |             |              |
| https://ec-cube/admin/shipping/1/edit                                              |           ○            |                      |                       |             |              |
| https://ec-cube/admin/shipping/1/order_status                                      |                        |                      |                       |             |              |
| https://ec-cube/admin/shipping/1/tracking_number                                   |                        |                      |                       |             |              |
| https://ec-cube/admin/shipping/2                                                   |                        |                      |                       |             |              |
| https://ec-cube/admin/shipping/2/edit                                              |           ○            |                      |                       |             |              |
| https://ec-cube/admin/shipping/notify_mail/1                                       |                        |                      |                       |             |              |
| https://ec-cube/admin/shipping/preview_notify_mail/1                               |                        |                      |                       |             |              |
| https://ec-cube/admin/store                                                        |                        |                      |                       |             |              |
| https://ec-cube/admin/store/plugin                                                 |                        |                      |                       |             |              |
| https://ec-cube/admin/store/plugin/1/disable                                       |                        |                      |                       |             |              |
| https://ec-cube/admin/store/plugin/1/enable                                        |                        |                      |                       |             |      ○       |
| https://ec-cube/admin/store/plugin/1/uninstall                                     |                        |                      |                       |             |      ○       |
| https://ec-cube/admin/store/plugin/1/update                                        |                        |                      |                       |             |      ○       |
| https://ec-cube/admin/store/plugin/api                                             |                        |                      |                       |             |      ○       |
| https://ec-cube/admin/store/plugin/api/delete/1/uninstall                          |                        |                      |                       |             |              |
| https://ec-cube/admin/store/plugin/api/install                                     |                        |                      |                       |             |      ○       |
| https://ec-cube/admin/store/plugin/api/install/1/confirm                           |                        |                      |                       |             |      ○       |
| https://ec-cube/admin/store/plugin/api/schema_update                               |                        |                      |                       |             |      ○       |
| https://ec-cube/admin/store/plugin/api/search                                      |                        |                      |                       |             |              |
| https://ec-cube/admin/store/plugin/api/search/page                                 |                        |                      |                       |             |              |
| https://ec-cube/admin/store/plugin/api/search/page/1                               |                        |                      |                       |             |              |
| https://ec-cube/admin/store/plugin/api/update                                      |                        |                      |                       |             |              |
| https://ec-cube/admin/store/plugin/api/upgrade                                     |                        |                      |                       |             |      ○       |
| https://ec-cube/admin/store/plugin/api/upgrade/1/confirm                           |                        |                      |                       |             |      ○       |
| https://ec-cube/admin/store/plugin/authentication_setting                          |                        |                      |                       |             |      ○       |
| https://ec-cube/admin/store/plugin/install                                         |                        |                      |                       |             |              |
| https://ec-cube/admin/store/template                                               |                        |                      |                       |             |              |
| https://ec-cube/admin/store/template/1                                             |                        |                      |                       |             |              |
| https://ec-cube/admin/store/template/1/delete                                      |                        |                      |                       |             |      ○       |
| https://ec-cube/admin/store/template/1/download                                    |                        |                      |                       |             |              |
| https://ec-cube/admin/store/template/install                                       |                        |                      |                       |             |              |
| https://ec-cube/block                                                              |                        |                      |                       |             |              |
| https://ec-cube/block/cart                                                         |                        |                      |                       |             |              |
| https://ec-cube/block/cart_sp                                                      |                        |                      |                       |             |              |
| https://ec-cube/block/search_product                                               |                        |                      |                       |             |              |
| https://ec-cube/block/search_product_sp                                            |                        |                      |                       |             |              |
| https://ec-cube/cart                                                               |                        |                      |                       |             |              |
| https://ec-cube/cart/buystep                                                       |                        |                      |                       |             |              |
| https://ec-cube/cart/buystep/1_1                                                   |                        |                      |                       |             |              |
| https://ec-cube/cart/down                                                          |                        |                      |                       |             |              |
| https://ec-cube/cart/down/1                                                        |                        |                      |                       |             |              |
| https://ec-cube/cart/down/11                                                       |                        |                      |                       |             |              |
| https://ec-cube/cart/remove                                                        |                        |                      |                       |             |      ○       |
| https://ec-cube/cart/remove/11                                                     |                        |                      |                       |             |      ○       |
| https://ec-cube/cart/up                                                            |                        |                      |                       |             |              |
| https://ec-cube/cart/up/1                                                          |                        |                      |                       |             |              |
| https://ec-cube/cart/up/11                                                         |                        |                      |                       |             |              |
| https://ec-cube/contact                                                            |           ○            |                      |           ○           |             |              |
| https://ec-cube/contact/complete                                                   |                        |                      |                       |             |              |
| https://ec-cube/entry                                                              |           ○            |                      |           ○           |             |              |
| https://ec-cube/entry/activate/xxx/1                                               |                        |                      |                       |             |      ○       |
| https://ec-cube/entry/complete                                                     |                        |                      |                       |             |              |
| https://ec-cube/forgot                                                             |                        |                      |                       |             |              |
| https://ec-cube/forgot/complete                                                    |                        |                      |                       |             |              |
| https://ec-cube/forgot/reset/xxx                                                   |                        |                      |                       |             |      ○       |
| https://ec-cube/guide                                                              |                        |                      |                       |             |              |
| https://ec-cube/help                                                               |                        |                      |                       |             |              |
| https://ec-cube/help/about                                                         |                        |                      |                       |             |              |
| https://ec-cube/help/agreement                                                     |                        |                      |                       |             |              |
| https://ec-cube/help/privacy                                                       |                        |                      |                       |             |              |
| https://ec-cube/help/tradelaw                                                      |                        |                      |                       |             |              |
| https://ec-cube/logout                                                             |                        |                      |                       |             |              |
| https://ec-cube/mypage                                                             |                        |                      |                       |             |              |
| https://ec-cube/mypage/                                                            |                        |                      |                       |             |              |
| https://ec-cube/mypage/change                                                      |           ○            |                      |                       |             |              |
| https://ec-cube/mypage/change_complete                                             |                        |                      |                       |             |              |
| https://ec-cube/mypage/delivery                                                    |                        |                      |                       |             |              |
| https://ec-cube/mypage/delivery/1                                                  |                        |                      |                       |             |              |
| https://ec-cube/mypage/delivery/1/delete                                           |           ○            |                      |                       |             |              |
| https://ec-cube/mypage/delivery/1/edit                                             |           ○            |                      |                       |             |              |
| https://ec-cube/mypage/delivery/new                                                |           ○            |                      |                       |             |              |
| https://ec-cube/mypage/favorite                                                    |                        |                      |                       |             |              |
| https://ec-cube/mypage/favorite/1/delete                                           |           ○            |                      |                       |             |              |
| https://ec-cube/mypage/history                                                     |                        |                      |                       |             |              |
| https://ec-cube/mypage/history/1                                                   |                        |                      |                       |             |              |
| https://ec-cube/mypage/history/2                                                   |                        |                      |                       |             |              |
| https://ec-cube/mypage/login                                                       |                        |                      |                       |             |              |
| https://ec-cube/mypage/order/1                                                     |                        |                      |                       |             |              |
| https://ec-cube/mypage/withdraw                                                    |                        |        ○             |           ○           |             |              |
| https://ec-cube/mypage/withdraw_complete                                           |                        |                      |                       |             |              |
| https://ec-cube/products                                                           |                        |                      |                       |             |              |
| https://ec-cube/products/add_cart                                                  |                        |                      |                       |             |              |
| https://ec-cube/products/add_cart/1                                                |                        |                      |                       |             |              |
| https://ec-cube/products/add_cart/2                                                |                        |                      |                       |             |              |
| https://ec-cube/products/add_favorite                                              |                        |                      |                       |             |              |
| https://ec-cube/products/add_favorite/1                                            |                        |                      |                       |             |              |
| https://ec-cube/products/add_favorite/2                                            |                        |                      |                       |             |              |
| https://ec-cube/products/detail                                                    |                        |                      |                       |             |              |
| https://ec-cube/products/detail/1                                                  |                        |                      |                       |             |              |
| https://ec-cube/products/list                                                      |                        |                      |                       |             |              |
| https://ec-cube/products/list?category_id&disp_number=0&mode&name&orderby=0&pageno |                        |                      |                       |             |              |
| https://ec-cube/products/list?category_id=6                                        |                        |                      |                       |             |              |
| https://ec-cube/robots.txt                                                         |                        |                      |                       |             |              |
| https://ec-cube/shopping                                                           |                        |                      |                       |             |              |
| https://ec-cube/shopping/checkout                                                  |                        |                      |                       |             |              |
| https://ec-cube/shopping/complete                                                  |                        |                      |                       |             |      ○       |
| https://ec-cube/shopping/confirm                                                   |                        |                      |                       |             |              |
| https://ec-cube/shopping/customer                                                  |                        |                      |                       |             |              |
| https://ec-cube/shopping/error                                                     |                        |                      |                       |             |              |
| https://ec-cube/shopping/login                                                     |                        |                      |                       |             |              |
| https://ec-cube/shopping/nonmember                                                 |           ○            |                      |                       |             |              |
| https://ec-cube/shopping/redirect_to                                               |                        |                      |                       |             |              |
| https://ec-cube/shopping/shipping                                                  |                        |                      |                       |             |              |
| https://ec-cube/shopping/shipping/1                                                |                        |                      |                       |             |              |
| https://ec-cube/shopping/shipping/4                                                |                        |                      |                       |             |              |
| https://ec-cube/shopping/shipping_edit                                             |                        |                      |                       |             |              |
| https://ec-cube/shopping/shipping_edit/1                                           |           ○            |                      |                       |             |              |
| https://ec-cube/shopping/shipping_multiple                                         |                        |                      |                       |             |              |
| https://ec-cube/shopping/shipping_multiple_edit                                    |                        |                      |                       |             |              |
| https://ec-cube/user_data/xxx                                                      |                        |                      |                       |             |      ○       |
