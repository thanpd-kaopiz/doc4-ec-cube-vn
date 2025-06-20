---
title: Kiểm thử cài đặt qua Owners Store
keywords: plugin mock plugin Owners Store
tags: [plugin, mock, package-api]
permalink: plugin_mock_package_api

---

Hướng dẫn cách dựng mock server Owners Store để kiểm thử tải plugin như khi tải qua Owners Store thật.
Có thể dùng để kiểm thử plugin trước khi đăng ký lên Owners Store.

### Yêu cầu

Cần cài đặt docker để sử dụng mock server.

Hãy cài đặt docker nếu chưa có.

### Các bước chạy mock server

Các bước chạy mock server như sau:

```
// Di chuyển vào thư mục gốc ec-cube
$ cd /path/to/ec-cube

// Tạo thư mục lưu plugin
$ mkdir ${PWD}/repos

// Khởi động mock server. Ở đây dùng port 9999, có thể đổi nếu cần
$ docker run -d --rm -v ${PWD}/repos:/repos -e MOCK_REPO_DIR=/repos -p 9999:8080 eccube/mock-package-api

// Đặt biến môi trường để tham chiếu mock server
$ echo ECCUBE_PACKAGE_API_URL=http://127.0.0.1:9999 >> .env

// Thiết lập key xác thực
$ psql eccube_db -h 127.0.0.1 -U postgres -c "update dtb_base_info set authentication_key='test';"

// Đặt plugin vào thư mục repos. Đổi đuôi thành tgz
$ cp /path/to/SamplePlugin.tar.gz repos/SamplePlugin.tgz
```

Sau khi thực hiện các bước trên, plugin đặt trong thư mục repos sẽ hiển thị khi tìm kiếm plugin.

![Tìm plugin](/images/plugin/mock-server.png)

