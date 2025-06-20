---
title: Thay đổi cách lưu thông tin session
keywords: session_handler
permalink: session_handler_settings
folder: i18n

---

## Tổng quan

Mặc định, dữ liệu session sẽ được lưu trên file hệ thống. Tuy nhiên, khi chạy trên nhiều web server, bạn có thể thay đổi cách lưu session.
EC-CUBE sử dụng session handler riêng (`SameSiteNoneCompatSessionHandler`) để hỗ trợ SameSite Cookie. Để thay đổi cách lưu session, hãy thay đổi session handler được sử dụng trong `SameSiteNoneCompatSessionHandler`.

### Lưu vào RDBMS

#### Ví dụ cấu hình
Để sử dụng cùng database với ứng dụng EC-CUBE, thêm cấu hình sau:

```
services:
  db_session_handler:
    class: Symfony\Component\HttpFoundation\Session\Storage\Handler\PdoSessionHandler
    public: false
    arguments:
      - '%env(DATABASE_URL)%'

  Eccube\Session\Storage\Handler\SameSiteNoneCompatSessionHandler:
    arguments:
      - '@db_session_handler'
```

#### Tạo bảng
Trước khi sử dụng, cần tạo bảng lưu session. Chạy DDL phù hợp với RDBMS bạn dùng:

- PostgreSQL:

    ```
    CREATE TABLE sessions (
        sess_id VARCHAR(128) NOT NULL PRIMARY KEY,
        sess_data BYTEA NOT NULL,
        sess_time INTEGER NOT NULL,
        sess_lifetime INTEGER NOT NULL
    );
    ```
    [pdo_session_storage #postgresql](https://symfony.com/doc/3.4/doctrine/pdo_session_storage.html#postgresql){:target="_blank"}


- MySQL:

    ```
    CREATE TABLE `sessions` (
        `sess_id` VARCHAR(128) NOT NULL PRIMARY KEY,
        `sess_data` BLOB NOT NULL,
        `sess_time` INTEGER UNSIGNED NOT NULL,
        `sess_lifetime` MEDIUMINT NOT NULL
    ) COLLATE utf8_bin, ENGINE = InnoDB;
    ```
    [pdo_session_storage.html #mysql](https://symfony.com/doc/3.4/doctrine/pdo_session_storage.html#mysql){:target="_blank"}


### Lưu vào Memcache

#### Thư viện cần thiết
- [memcached extension](https://www.php.net/manual/ja/book.memcached.php)

#### Ví dụ cấu hình

Nếu Memcache chạy trên localhost port 11211, cấu hình như sau:

```
services:
  memcached:
    class: Memcached
    public: false
    arguments: ['sess']
    calls:
      - [ addServer, [ 'localhost', '11211' ]]

  memcached_session_handler:
    class: Symfony\Component\HttpFoundation\Session\Storage\Handler\MemcachedSessionHandler
    public: false
    arguments: [ '@memcached', { prefix: 'sess', expiretime: '3600' }]

  Eccube\Session\Storage\Handler\SameSiteNoneCompatSessionHandler:
    arguments:
      - '@memcached_session_handler'
```

### Lưu vào MongoDB

#### Thư viện cần thiết
- [MongoDB driver extension](https://www.php.net/manual/ja/set.mongodb.php)
- [mongodb/mongodb package](https://github.com/mongodb/mongo-php-library)

#### Cấu hình

Nếu MongoDB chạy trên localhost port 27017, cấu hình như sau:

```
services:
    mongo_client:
        class: MongoDB\Client
        arguments: ['mongodb://user:password@localhost:27017']
    mongodb_session_handler:
        class: Symfony\Component\HttpFoundation\Session\Storage\Handler\MongoDbSessionHandler
        arguments: ['@mongo_client', { 'database': 'session_db', 'collection': 'sessions' }]

    Eccube\Session\Storage\Handler\SameSiteNoneCompatSessionHandler:
        arguments:
            - '@mongodb_session_handler'
```
