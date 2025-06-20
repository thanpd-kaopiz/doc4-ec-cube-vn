---
title: Hướng dẫn sử dụng thư mục Customize trên ec-cube.co
keywords: co ec-cube.co Cloud version Hướng dẫn sử dụng thư mục Customize
tags: [co, ec-cube.co]
permalink: co/co_customize_dir_usage
folder: co
---

---

Mã nguồn EC-CUBE chính đang chạy trên .co là branch co/master (với 4.0), co/4.1 (với 4.1) của repository EC-CUBE.
Khởi động EC-CUBE bằng các branch này và thực hiện tuỳ biến tại thư mục app/Customize.

## Các bước thiết lập môi trường local

### Thiết lập khoá công khai (public key)

Truy cập [SSH認証鍵](https://source.cloud.google.com/user/ssh_keys?register=true){:target="_blank"} để đăng ký khoá công khai.
Khi đó, hãy đảm bảo bạn đăng nhập bằng tài khoản Google đã chia sẻ với EC-CUBE khi đăng ký hoặc nâng cấp gói Standard.

※ Về cách thiết lập chi tiết, vui lòng xem liên kết "Chi tiết" trên trang trên hoặc [tại đây](https://cloud.google.com/source-repositories/docs/authentication#ssh){:target="_blank"}.

#### Trường hợp sử dụng tài khoản Google Group

Ví dụ với các địa chỉ email sau:
- Địa chỉ Google group: example@googlegroups.com
- Địa chỉ email của thành viên trong group: user1@example.com

1. Truy cập [SSH認証鍵](https://source.cloud.google.com/user/ssh_keys?register=true){:target="_blank"} và đăng ký khoá công khai bằng tài khoản "user1@example.com".
1. Khi git clone, chỉ định "user1@example.com".

### Clone repository ec-cube.co

```
$ git clone <URL repository> eccube-co-customize
$ cd eccube-co-customize
```

### Thêm repository EC-CUBE để theo dõi

```
$ git remote add ec-cube https://github.com/EC-CUBE/ec-cube.git
$ git fetch ec-cube
```

### Tạo branch develop cho phát triển local

```
$ git checkout -b develop origin/develop
```

### Theo dõi branch co

```
$ git merge --allow-unrelated-histories ec-cube/<tên branch co>
```

Branch co sẽ khác nhau tuỳ phiên bản:

- 4.0 -> co/master
- 4.1 -> co/4.1
- 4.2 -> co/4.2

Ví dụ sử dụng môi trường 4.2, merge như sau:

```
$ git merge --allow-unrelated-histories ec-cube/co/4.2
```

## Cách phản ánh lên môi trường test/production

Push branch lên repository .co sẽ tự động cập nhật lên site (mất khoảng 1 phút).

※ Có thể push các file ngoài app/Customize, nhưng chỉ các file được quy định trong chức năng quản lý Git mới được phản ánh lên site.

### Phản ánh lên môi trường test

```
$ git push origin develop -u
```

### Phản ánh lên môi trường production

```
$ git checkout master
$ git merge develop
$ git push origin master -u
```

## Khởi động môi trường local

### Khởi động môi trường local

```
$ docker-compose -f docker-compose.yml -f docker-compose.pgsql.yml -f docker-compose.dev.yml up
$ docker-compose exec -u www-data ec-cube bin/console eccube:install --no-interaction
$ docker-compose exec -u www-data ec-cube bin/console eccube:generate:proxies
$ docker-compose exec -u www-data ec-cube bin/console doctrine:schema:update --force --dump-sql
$ docker-compose exec -u www-data ec-cube bin/console doctrine:migrations:migrate
```

### Mở trên trình duyệt

```
$ open http://127.0.0.1:8080/
```

## Cách phản ánh plugin đã cài đặt lên môi trường local

Nếu môi trường đã cài plugin, cần cài plugin đó lên local.

### Thêm khoá xác thực

```
$ docker exec <tên container postgres> psql -U dbuser eccubedb -c "update dtb_base_info set authentication_key='<khoá xác thực>' "
```

### Cài đặt và kích hoạt plugin

```
$ docker-compose exec -u www-data ec-cube bin/console eccube:composer:require ec-cube/<mã plugin>
$ docker-compose exec -u www-data ec-cube bin/console eccube:plugin:enable --code=<mã plugin>
```
