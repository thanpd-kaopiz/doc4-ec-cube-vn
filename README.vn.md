# Tài liệu phát triển EC-CUBE 4

Đây là kho lưu trữ của [Tài liệu phát triển EC-CUBE 4](https://doc4.ec-cube.net/).

Trang này cung cấp tài liệu về đặc tả, quy trình, và các mẹo phát triển liên quan đến EC-CUBE 4.

Nếu bạn muốn sửa đổi, bổ sung hoặc tạo tài liệu mới,
vui lòng gửi Pull Request đến kho lưu trữ này.


## Về việc hợp tác phát triển

Khi bạn đóng góp mã nguồn, bổ sung, sửa đổi hoặc hợp tác phát triển "EC-CUBE" (bao gồm gửi Issue, Pull Request, hoạt động trên GitHub),
vui lòng đọc và đồng ý với [Chính sách bản quyền của EC-CUBE](https://github.com/EC-CUBE/ec-cube/wiki/EC-CUBE%E3%81%AE%E3%82%B3%E3%83%94%E3%83%BC%E3%83%A9%E3%82%A4%E3%83%88%E3%83%9D%E3%83%AA%E3%82%B7%E3%83%BC).

Khi gửi Pull Request, bạn được xem là đã đồng ý với chính sách bản quyền của EC-CUBE.

## Công cụ xây dựng trang tài liệu này

Tài liệu phát triển EC-CUBE 4 được host trên [github pages](https://pages.github.com/).

Ngoài ra, sử dụng theme [Minimal Mistakes Jekyll theme](https://mmistakes.github.io/minimal-mistakes/) của [Jekyll](http://jekyllrb-ja.github.io/).

## Cách gửi Pull Request

Hãy tạo tài khoản Github và gửi Pull Request từ kho lưu trữ của bạn.

### Fork doc4.ec-cube.net

Fork kho lưu trữ doc4.ec-cube.net về tài khoản Github của bạn.

### Clone về thư mục tuỳ ý

Clone mã nguồn từ kho của bạn về máy tính bằng lệnh `git clone`.

```
$ git clone https://github.com/[tên-tài-khoản-của-bạn]/doc4.ec-cube.net.git
```

### Đăng ký kho lưu trữ gốc làm remote

Đăng ký kho lưu trữ gốc với tên `upstream` (hoặc tên tuỳ ý).

```
$ cd doc4.ec-cube.net/
$ git remote add upstream https://github.com/EC-CUBE/doc4.ec-cube.net.git
```

### Cập nhật branch local và tạo branch sửa đổi
```
$ git pull upstream master
$ git checkout -b [tên-branch-tuỳ-chọn]
```

### Chỉnh sửa tài liệu

#### Chỉnh sửa nội dung

Bạn có thể chỉnh sửa các file .md trong thư mục _pages/ để thay đổi nội dung trang.

#### Chỉnh sửa sidebar

Thêm mục vào _data/navigation.yml để chỉnh sửa sidebar.

#### File cấu hình

_config.yml là file cấu hình áp dụng cho toàn bộ trang.

### Đẩy thay đổi lên kho của bạn

```
$ git add [file đã sửa]
$ git commit -m "[Nội dung commit]"
$ git push origin [tên-branch]
```

Sau đó, hãy tạo Pull Request từ kho của bạn lên kho gốc.


## Kiểm tra tài liệu đã sửa trên môi trường local

Bạn có thể kiểm tra tài liệu đã sửa trên máy tính cá nhân bằng cách xây dựng môi trường phát triển local.

### Sử dụng Docker

Nếu đã cài đặt [Docker Compose](http://docs.docker.jp/compose/toc.html), bạn có thể dễ dàng tạo môi trường phát triển. Sau khi chạy lệnh, truy cập `http://localhost:4000` trên trình duyệt.

```bash
# Di chuyển vào thư mục dự án
$ cd doc4.ec-cube.net

# Khởi động server (lần đầu)
# * Có thể mất một chút thời gian để khởi động.
# * Khi chỉnh sửa file markdown, HTML sẽ được tạo lại sau vài giây.
$ docker-compose up

# Dừng server
$ docker-compose stop

# Khởi động lại server (từ lần thứ hai trở đi)
$ docker-compose start
```

Đã kiểm tra hoạt động trên cả Windows và Mac.

### Sử dụng môi trường Ruby local

#### Yêu cầu

1. Máy tính đã cài ruby (phiên bản 2.4.0 trở lên).
2. Nếu dùng Windows, nên sử dụng terminal như Git Bash.
3. Cần có tài khoản Github.

※ Kiểm tra phiên bản Ruby

```
$ ruby -v
ruby 2.4.5p335 (2018-10-18 revision 65137) [x64-mingw32]
```

#### Cài đặt gem (thư viện ruby)

Cài đặt gem dựa trên gemfile.lock bằng lệnh `bundle install`.

```
$ bundle install
```

※ Trên Windows, gemfile.lock có thể bị thay đổi, hãy loại khỏi commit.

```
eventmachine (1.2.7-x64-mingw32)
```
#### Khởi động site bằng server local

Chạy lệnh sau để khởi động site.

```
$ bundle exec jekyll serve
（省略）
Server address: http://localhost:4000
Server running... press ctrl-c to stop.
```

Truy cập http://localhost:4000 trên trình duyệt để xem trang tài liệu phát triển EC-CUBE 4. 