---
title: Tuỳ biến Repository
keywords: core tuỳ biến repository
tags: [core, repository]
permalink: customize_repository
folder: customize
---

## Mở rộng QueryBuilder [#2285](https://github.com/EC-CUBE/ec-cube/pull/2285){:target="_blank"}, [#2298](https://github.com/EC-CUBE/ec-cube/pull/2298){:target="_blank"}

Bạn có thể tuỳ biến thứ tự sắp xếp hoặc điều kiện tìm kiếm cho các phương thức tạo QueryBuilder trong các class Repository.
Các phương thức có thể sử dụng như sau:

| Class Repository                                               | QueryKey                             |
|---------------------------------------------------------------|--------------------------------------|
| ProductRepository::getQueryBuilderBySearchData()              | QueryKey::PRODUCT_SEARCH             |
| ProductRepository::getQueryBuilderBySearchDataForAdmin()      | QueryKey::PRODUCT_SEARCH_ADMIN       |
| ProductRepository::getFavoriteProductQueryBuilderByCustomer() | QueryKey::PRODUCT_GET_FAVORITE       |
| CustomerRepository::getQueryBuilderBySearchData()             | QueryKey::CUSTOMER_SEARCH            |
| OrderRepository::getQueryBuilderBySearchData()                | QueryKey::ORDER_SEARCH               |
| OrderRepository.getQueryBuilderBySearchDataForAdmin()         | QueryKey::ORDER_SEARCH_ADMIN         |
| OrderRepository::getQueryBuilderByCustomer()                  | QueryKey::ORDER_SEARCH_BY_CUSTOMER   |
| LoginHistoryRepository::getQueryBuilderBySearchDataForAdmin() | QueryKey::LOGIN_HISTORY_SEARCH_ADMIN |

※ `QueryKey::LOGIN_HISTORY_SEARCH_ADMIN` chỉ có từ EC-CUBE 4.1 trở đi

Các interface để tuỳ biến như sau:

| Interface/Class         | Mô tả                           |
|------------------------|----------------------------------|
| QueryCustomizer        | Tuỳ biến QueryBuilder tự do      |
| OrderByCustomizer      | Tuỳ biến thứ tự sắp xếp          |
| WhereCustomizer        | Thêm điều kiện tìm kiếm           |
| JoinCustomizer         | Thêm bảng join                   |

### Ví dụ triển khai

Ví dụ luôn sắp xếp theo ID sản phẩm trong `ProductRepository::getQueryBuilderBySearchDataForAdmin()`.
Chỉ định phương thức muốn áp dụng bằng hàm `getQueryKey()`, sẽ tự động có hiệu lực.

```php
<?php

namespace Customize\Repository;

use Eccube\Doctrine\Query\OrderByClause;
use Eccube\Doctrine\Query\OrderByCustomizer;
use Eccube\Repository\QueryKey;

class AdminProductListCustomizer extends OrderByCustomizer
{
    /**
     * Luôn sắp xếp theo ID sản phẩm.
     *
     * @param array $params
     * @param $queryKey
     * @return OrderByClause[]
     */
    protected function createStatements($params, $queryKey)
    {
        return [new OrderByClause('p.id')];
    }

    /**
     * Áp dụng cho ProductRepository::getQueryBuilderBySearchDataForAdmin.
     *
     * @return string
     * @see \Eccube\Repository\ProductRepository::getQueryBuilderBySearchDataForAdmin()
     * @see QueryKey
     */
    public function getQueryKey()
    {
        return QueryKey::PRODUCT_SEARCH_ADMIN;
    }
}
```

