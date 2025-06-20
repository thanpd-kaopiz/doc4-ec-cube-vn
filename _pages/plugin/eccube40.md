---
title: Lưu ý khi sử dụng EC-CUBE4.0 (Composer v1)
keywords: plugin EC-CUBE4.0 Composer1
tags: [plugin, eccube, composer]
permalink: plugin_eccube40

---

Có thông báo rằng metadata của Composer v1 sử dụng trong EC-CUBE4.0 sẽ bị ngừng cung cấp từ sau ngày 1/8/2025.

[https://blog.packagist.com/shutting-down-packagist-org-support-for-composer-1-x/](https://blog.packagist.com/shutting-down-packagist-org-support-for-composer-1-x/){:target="_blank"}

EC-CUBE4.0 sử dụng Composer v1 để quản lý plugin, điều này ảnh hưởng đến việc cài đặt/kích hoạt/vô hiệu hóa/xóa/cập nhật plugin.

Việc ngừng cung cấp chỉ ảnh hưởng đến truy cập metadata của Composer v1 (thông tin version package, URL tải về, v.v.), nên thông thường sẽ không bị ảnh hưởng nếu không cập nhật dependency.

File composer.lock đã lưu URL tải về, nên việc cài đặt package bằng composer install vẫn thực hiện như trước.

Tuy nhiên, do lịch sử phát triển, EC-CUBE4.0 có thể cần truy cập metadata Composer v1 không cần thiết khi cài đặt/kích hoạt/vô hiệu hóa/xóa/cập nhật plugin.

## Cách xử lý

### Sửa file composer.json

1. Xóa phần require-dev.
   Xóa phần require-dev như bên dưới. Phần này chỉ dùng khi phát triển nên xóa không ảnh hưởng.

   ``` json
    "require-dev": {
        "bheller/images-generator": "^1.0",
        "captbaritone/mailcatcher-codeception-module": "^1.2",
        "codeception/codeception": "~2.4.5",
        "dama/doctrine-test-bundle": "^5.0",
        "fzaninotto/faker": "^1.7",
        "mikey179/vfsstream": "^1.6",
        "phpstan/phpstan": "^0.12",
        "phpunit/phpunit": "^6.5",
        "symfony/browser-kit": "^3.4",
        "symfony/phpunit-bridge": "^3.4"
    },
    ```

2. Thêm cấu hình vào phần repositories.
   Thêm cấu hình tham chiếu eccube-plugin-installer vào GitHub và vô hiệu hóa packagist.org để tránh lỗi không mong muốn.
   // ここから // ここまで cần xóa khi thêm vào thực tế để tránh lỗi cú pháp.

   ``` json
    "repositories": {
        "eccube": {
            "type": "composer",
            "url": "https://package-api.ec-cube.net",
            "options": {
                "http": {
                    "header": ["X-ECCUBE-KEY: <chuỗi key xác thực>"]
                }
            }
        }
        // ここから
        ,
        "packagist.org": false,
        "eccube/plugin-installer": {
            "type": "vcs",
            "url": "https://github.com/EC-CUBE/eccube-plugin-installer",
            "no-api": true
        }
        // ここまで
    }
   ```

### Chạy lệnh composer install

Tiếp theo, dùng ssh để chạy lệnh composer install --no-scripts --no-plugins. Cần thiết để đảm bảo tính nhất quán dưới vendor. Không thêm --no-dev để cài luôn các package trong require-dev (dù đã xóa khỏi composer.json nhưng composer.lock vẫn còn thông tin).

```
composer install --no-scripts --no-plugins
```

Sau khi sửa composer.json và chạy composer install, có thể cài đặt/kích hoạt/vô hiệu hóa/xóa/cập nhật plugin mà không cần cập nhật dependency.

## Lưu ý

### Trường hợp plugin phụ thuộc package khác

Ví dụ như [Web API Plugin](https://www.ec-cube.net/products/detail.php?product_id=2121), nếu plugin phụ thuộc package khác sẽ bị ảnh hưởng bởi việc ngừng metadata Composer v1.

Có thể xử lý bằng cách thêm cấu hình GitHub của package phụ thuộc vào composer.json.

Nếu trong require của app/Plugin/<mã plugin>/composer.json có package ngoài ec-cube/plugin-installer thì là có phụ thuộc.

```
"require": {
    "ec-cube/plugin-installer": "~0.0.6 || ^2.0",
    "trikoder/oauth2-bundle": "^2.1",
    "nyholm/psr7": "^1.2",
    "webonyx/graphql-php": "^14.0"
  },
```

**Cách xử lý**

Ví dụ với [Web API Plugin](https://www.ec-cube.net/products/detail.php?product_id=2121){:target="_blank"}, thêm cấu hình GitHub của các package phụ thuộc vào repositories.

***// ここから // ここまで** cần xóa khi thêm vào thực tế để tránh lỗi cú pháp*

```
    "repositories": {
        "eccube": {
            "type": "composer",
            "url": "https://package-api.ec-cube.net",
            "options": {
                "http": {
                    "header": ["X-ECCUBE-KEY: <KEY xác thực>"]
                }
            }
        },
        "packagist.org": false,
        "eccube/plugin-installer": {
            "type": "vcs",
            "url": "https://github.com/EC-CUBE/eccube-plugin-installer",
            "no-api": true
        }
        // ここから
        ,
        "trikoder/oauth2-bundle": {
            "type": "vcs",
            "url": "https://github.com/trikoder/oauth2-bundle",
            "no-api": true
        },
        "nyholm/psr7": {
            "type": "vcs",
            "url": "https://github.com/Nyholm/psr7",
            "no-api": true
        },
        "webonyx/graphql-php": {
            "type": "vcs",
            "url": "https://github.com/webonyx/graphql-php",
            "no-api": true
        },
        "php-http/message-factory": {
            "type": "vcs",
            "url": "https://github.com/php-http/message-factory",
            "no-api": true
        },
        "psr/http-message": {
            "type": "vcs",
            "url": "https://github.com/php-fig/http-message",
            "no-api": true
        },
        "psr/http-factory": {
            "type": "vcs",
            "url": "https://github.com/php-fig/http-factory",
            "no-api": true
        },
        "league/oauth2-server": {
            "type": "vcs",
            "url": "https://github.com/thephpleague/oauth2-server",
            "no-api": true
        },
        "symfony/psr-http-message-bridge": {
            "type": "vcs",
            "url": "https://github.com/symfony/psr-http-message-bridge",
            "no-api": true
        },
        "league/event": {
            "type": "vcs",
            "url": "https://github.com/thephpleague/event",
            "no-api": true
        },
        "lcobucci/jwt": {
            "type": "vcs",
            "url": "https://github.com/lcobucci/jwt",
            "no-api": true
        },
        "defuse/php-encryption": {
            "type": "vcs",
            "url": "https://github.com/defuse/php-encryption",
            "no-api": true
        },
        "paragonie/random_compat": {
            "type": "vcs",
            "url": "https://github.com/paragonie/random_compat",
            "no-api": true
        }
        // ここまで
    }
```

### Khuyến nghị cài đặt/xóa/cập nhật plugin bằng dòng lệnh

Composer v1 sử dụng trong EC-CUBE4.0 cần nhiều tài nguyên, nên trên môi trường shared hosting hoặc tài nguyên hạn chế, việc cài đặt/xóa/cập nhật plugin từ quản trị có thể thất bại.

Ngay cả khi có vẻ hoạt động bình thường, có thể xảy ra bất nhất giữa danh sách package trong composer.json, file dưới app/Plugin, và dữ liệu dtb_plugin.

Khuyến nghị thao tác plugin bằng dòng lệnh để đảm bảo ổn định hơn.

[https://qiita.com/nanasess/items/791c9ec98f69ada93ea0#コマンドラインでのプラグインインストール](https://qiita.com/nanasess/items/791c9ec98f69ada93ea0#%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E3%83%A9%E3%82%A4%E3%83%B3%E3%81%A7%E3%81%AE%E3%83%97%E3%83%A9%E3%82%B0%E3%82%A4%E3%83%B3%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB){:target="_blank"}

### Khuyến nghị nâng cấp EC-CUBE

Do không thể cập nhật các thư viện liên quan qua Composer, khuyến nghị nâng cấp lên EC-CUBE4.3 trở lên.

Nếu khó nâng cấp lên 4.3, hãy cố gắng nâng cấp lên 4.1 trở lên. EC-CUBE4.0 và 4.1 tương thích plugin nên nâng cấp ít tốn công hơn.

### Xử lý sự cố

**Q) Khi cập nhật plugin từ quản trị bị lỗi.**

A) Có thể đã xảy ra bất nhất plugin. Hãy kiểm tra nội dung lỗi và thử cập nhật bằng dòng lệnh.

- Nếu gặp lỗi truy cập metadata packagist.org
    
    ```diff
    Your requirements could not be resolved to an installable set of packages.
    
      Problem 1
        - ec-cube/Api 2.1.2 requires nyholm/psr7 ^1.2 -> no matching package found.
        - ec-cube/Api 2.1.1 requires nyholm/psr7 ^1.2 -> no matching package found.
        - ec-cube/Api 2.1.4 requires nyholm/psr7 ^1.2 -> no matching package found.
        - ec-cube/Api 2.1.3 requires nyholm/psr7 ^1.2 -> no matching package found.
        - ec-cube/Api 2.1.0 requires nyholm/psr7 ^1.2 -> no matching package found.
        - Installation request for ec-cube/api ^2.1 -> satisfiable by ec-cube/Api[2.1.0, 2.1.3, 2.1.4, 2.1.1, 2.1.2].
    ```
    
    Nếu gặp lỗi "no matching package found.", có thể do ảnh hưởng của việc ngừng metadata Composer v1. Hãy tham khảo [tại đây](/plugin_eccube40#%E4%BB%96%E3%81%AE%E3%83%91%E3%83%83%E3%82%B1%E3%83%BC%E3%82%B8%E3%81%A8%E4%BE%9D%E5%AD%98%E9%96%A2%E4%BF%82%E3%81%AE%E3%81%82%E3%82%8B%E3%83%97%E3%83%A9%E3%82%B0%E3%82%A4%E3%83%B3%E3%81%AE%E5%A0%B4%E5%90%88) để thêm package phụ thuộc vào composer.json
    

- Nếu gặp lỗi khi cập nhật dependency
    
    ```
    [21.1MiB/8.61s] Package operations: 0 installs, 0 updates, 42 removals
    [21.1MiB/8.61s]   - Removing webmozart/assert (1.6.0)
    
    In Filesystem.php line 217:
                                                                                   
      Could not delete /var/www/html/vendor/webmozart/assert/CHANGELOG.md: The ty  
      pe "datetimetz" was implicitly marked as commented due to the configuration  
      . This is deprecated and will be removed in DoctrineBundle 2.0. Either set   
      the "commented" attribute in the configuration to "false" or mark the type   
      as commented in "Eccube\Doctrine\DBAL\Types\UTCDateTimeTzType::requiresSQLC  
      ommentHint()."
    ```
    
    Nếu gặp lỗi "Could not delete ...", có thể do không thể giao tiếp với Composer v1. Hãy cập nhật bằng dòng lệnh.
    

**Q) Làm sao tìm GitHub của package phụ thuộc?**

A) Trên [packagist.org](http://packagist.org){:target="_blank"} ở phần detail bên phải sẽ có link GitHub.

### Cách cài đặt Composer v1

Theo https://getcomposer.org/download/, sau 8/2025 có thể không còn setup v1, nên hướng dẫn cách tải trực tiếp v1.

1. Di chuyển vào thư mục cài đặt EC-CUBE
    
    ```
    cd path/to/ec-cube
    ```
    
2. Tải composer.phar
    
    ```
    curl -O https://getcomposer.org/download/1.10.27/composer.phar
    ```
    
3. Đổi tên thành composer
    
    ```
    mv composer.phar composer
    ```
    

Chạy lệnh sau, nếu hiện logo composer là cài đặt thành công.

```
php composer list

   ______
  / ____/___  ____ ___  ____  ____  ________  _____
 / /   / __ \/ __ `__ \/ __ \/ __ \/ ___/ _ \/ ___/
/ /___/ /_/ / / / / / / /_/ / /_/ (__  )  __/ /
\____/\____/_/ /_/ /_/ .___/\____/____/\___/_/
                    /_/
Composer version 1.10.27 2023-09-29 10:50:23

Usage:
  command [options] [arguments]
...(省略)
```

Trong bài này, lệnh `composer` nghĩa là chạy `php composer`.

Nếu gặp lỗi command not found trên shared hosting, có thể PHP cài ở vị trí khác. Hãy tham khảo tài liệu server và chỉ định đường dẫn PHP như sau:

```
# Ví dụ trên Xserver
/usr/bin/php7.4 composer list
```


