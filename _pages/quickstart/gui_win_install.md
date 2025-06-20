---
title: Hướng dẫn cài đặt bằng XAMPP trên Windows
keywords: cài đặt XAMPP
tags: [quickstart, install, gui]
permalink: quickstart/gui_win_install
folder: quickstart
description: Hướng dẫn cài đặt EC-CUBE4 trên môi trường Windows sử dụng XAMPP.
---

## Trước khi cài đặt
Bài viết này hướng dẫn cài đặt EC-CUBE4 trên môi trường Windows sử dụng XAMPP.  
Hãy kiểm tra phiên bản PHP phù hợp với EC-CUBE bạn sử dụng tại [Yêu cầu hệ thống](/quickstart/requirement).  
Môi trường mẫu trong bài viết này như sau:  
```
// Môi trường mẫu
Windows 10
EC-CUBE 4.0.4
XAMPP 7.4.7
```

## Tải và cài đặt XAMPP
Đầu tiên, hãy chuẩn bị XAMPP.  
EC-CUBE4.0.4 hỗ trợ PHP 7.4.  
Bạn cần tải đúng phiên bản XAMPP phù hợp với phiên bản PHP của EC-CUBE bạn sử dụng.  

Truy cập [Trang chủ XAMPP](https://www.apachefriends.org/jp/index.html){:target='_blank'},
chọn menu để vào trang tải về.  
Tải về phiên bản XAMPP phù hợp.  
Bạn cũng có thể tải các phiên bản cũ hơn tại mục "Other downloads".

Sau khi tải về, hãy cài đặt XAMPP.  

## Tải EC-CUBE
Tiếp theo, hãy tải EC-CUBE.  
Tải phiên bản mới nhất từ [Trang tải về EC-CUBE](https://www.ec-cube.net/download/){:target='_blank'}.  
※ Cần đăng ký thành viên để tải về.  

Sau khi tải về, hãy giải nén file.  

## Đặt EC-CUBE vào XAMPP
Giải nén EC-CUBE và đặt vào thư mục htdocs của XAMPP.  

**URL trang chủ shop sẽ phụ thuộc vào cấu trúc thư mục bạn đặt.**  
`http://127.0.0.1/{tên thư mục bạn tạo trong htdocs}/`  

```
Ví dụ: Tạo thư mục test-shop trong htdocs và đặt eccube-4.0.4 vào đó
■ Cấu trúc thư mục
Windows(C:)\xampp\htdocs\test-shop\eccube-4.0.4\

■ URL trang chủ shop
http://127.0.0.1/test-shop/eccube-4.0.4/
```
※ Chưa cài đặt EC-CUBE nên truy cập URL shop sẽ chưa hiển thị trang web.  
※ Tên thư mục eccube-4.0.4 có thể đổi tùy ý.  

Nếu chỉ đặt eccube-4.0.4 vào htdocs mà không tạo test-shop, URL shop sẽ là:  
`http://127.0.0.1/eccube-4.0.4/`  

## Tạo database
Khởi động XAMPP.  
Nhấn "Start" cho Apache và MySQL, sau đó nhấn "Admin" để mở phpMyAdmin.  
![XAMPP](/images/install/gui-win/xampp1.png)

phpMyAdmin sẽ mở ra.
![phpMyAdmin](/images/install/gui-win/mysql.png)

Nhấn "Tạo mới" và nhập tên database, sau đó tạo database.  
```
Ví dụ
Tên database
`eccube123_`

Collation giữ nguyên utf8mb4_general_ci.
```

XAMPP có sẵn tài khoản database, bạn có thể dùng để cài EC-CUBE.  
Nếu muốn tạo tài khoản mới, vào menu "Tài khoản người dùng" để tạo.

※ Nếu dùng cho môi trường production, hãy tạo tài khoản riêng cho database.  Thông tin kết nối database (tên, tài khoản, v.v.) nếu bị lộ sẽ gây nguy hiểm.  Hãy quản lý cẩn thận.

## Chỉnh sửa file ini

Khởi động XAMPP.  
Nhấn "Start" cho Apache và MySQL.  
![XAMPP](/images/install/gui-win/xampp2.png)

Truy cập trình duyệt với URL:  
`http://127.0.0.1/{tên thư mục chứa EC-CUBE}/`  

Màn hình cài đặt sẽ xuất hiện.  

![install step0](/images/install/gui-win/step0.png)

Nếu xuất hiện lỗi "intl extension chưa được bật".  

Hãy mở file php.ini tại thư mục sau:  
`Windows(C:)\xampp\php\php.ini`  

Tìm kiếm "intl" trong file php.ini.  

```
;extension=intl
```
Tìm dòng trên và xóa dấu ; phía trước.  
Sau đó lưu lại:
```
extension=intl
```

Tiếp theo, chỉnh sửa thời gian timeout trong php.ini.  
Tìm kiếm "max_execution_time" trong file:
```
max_execution_time=30
```
Sửa thành:
```
max_execution_time=120
```
※ Nếu máy yếu, nên tăng giá trị này lên nữa.  

```
// Ví dụ
max_execution_time=300
```
**Khởi động lại XAMPP.**  
Nhấn "Stop" cho Apache và MySQL, đợi 10 giây rồi nhấn "Start" lại.  

Truy cập lại URL:  
`http://127.0.0.1/{tên thư mục chứa EC-CUBE}/`  

![install step1](/images/install/step1.png)

Nếu không còn lỗi "intl extension chưa được bật" thì đã chỉnh xong php.ini.  

Tiếp tục cài đặt EC-CUBE.

Nhấn "Tiếp theo" trên màn hình cài đặt.

## Cài đặt EC-CUBE

![install step2](/images/install/step2.png)
Nhấn "Tiếp theo".

### Thiết lập website

![install step3](/images/install/step3.png)

#### Thông tin cơ bản của cửa hàng

- **Tên cửa hàng của bạn**
  - Nhập tên cửa hàng, có thể dùng tiếng Việt hoặc Nhật.
- **Địa chỉ email**
  - Email này sẽ nhận thông báo đơn hàng.
- **ID đăng nhập quản trị**
  - ID dùng để đăng nhập trang quản trị. Không nên đặt "admin" hoặc các ID dễ đoán để tránh bị tấn công. Nên đặt chuỗi ngẫu nhiên.
- **Mật khẩu quản trị**
  - Mật khẩu đăng nhập quản trị. Hãy ghi nhớ, nếu quên sẽ không đăng nhập được.  EC-CUBE **không có chức năng lấy lại mật khẩu quản trị**.  Nên đặt mật khẩu phức tạp, không dùng "test1234" hay "password".
- **Tên thư mục quản trị**  
  - URL truy cập quản trị sẽ là:  
  http://127.0.0.1/{thư mục EC-CUBE}/{tên thư mục quản trị}/  
  Không nên đặt "admin" hay "dashboard". Nên đặt tên khó đoán.
- **Bắt buộc truy cập site qua SSL**  
  - Không cần nhập ở môi trường local.
- **Giới hạn IP truy cập quản trị**
  - Chỉ cho phép IP nhất định truy cập quản trị. Ở local không cần thiết lập. Nếu có IP cố định thì nên thiết lập để tăng bảo mật.

*Lưu ý: Nếu thông tin truy cập quản trị bị lộ sẽ rất nguy hiểm. Hãy bảo mật cẩn thận!*

#### Thiết lập email
Ở local không cần thiết lập gì thêm.

### Thiết lập database
![install step 4](/images/install/gui-win/step5.png)
Nhập thông tin database.  
**Ở đây dùng tài khoản mặc định của XAMPP.**

- **Loại database**
  - Ở môi trường production nên dùng MySQL hoặc PostgreSQL.
- **Host database**
  - Là localhost.
- **Port database**
  - Có thể để trống.
- **Tên database**
  - Nhập tên database đã tạo, ví dụ "eccube123_".
- **Tên người dùng**
  - Là root.
- **Mật khẩu**
  - Để trống.

※ Ở môi trường production nên tạo tài khoản riêng.

Nhập xong nhấn "Tiếp theo".  

### Khởi tạo database
![install step 6](/images/install/step6.png)

Nhấn "Tiếp theo" để đăng ký dữ liệu khởi tạo vào database.

### Hoàn tất cài đặt
![install step 6](/images/install/step7.png)

**Chúc mừng bạn!**  
Nếu thấy màn hình này là đã cài đặt thành công.  

Hướng dẫn sử dụng trang quản trị: [tại đây](https://www.ec-cube.net/manual/ec-cube4/){:target="_blank"}.

Nhấn *Hiển thị trang quản trị* để vào màn hình đăng nhập quản trị. Đăng nhập bằng thông tin đã nhập ở [Thông tin cơ bản của cửa hàng](#thông-tin-cơ-bản-của-cửa-hàng).

Nếu không đăng nhập được, có thể bạn đã nhập sai ID hoặc mật khẩu quản trị. Hãy xóa file .env trong thư mục cài đặt và làm lại các bước cài đặt từ đầu.
