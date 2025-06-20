---
title: Hướng dẫn cài đặt bằng MAMP trên Mac
keywords: cài đặt MAMP
tags: [quickstart, install, gui]
permalink: quickstart/gui_mac_install
folder: quickstart
description: EC-CUBE4系 được cài đặt trên môi trường Mac bằng MAMP.
---

## Trước khi cài đặt
Hướng dẫn cài đặt EC-CUBE trên môi trường Mac bằng MAMP.  
Cấu hình môi trường được mô tả như sau.  
```
// サンプルの構築環境
MacOS 10.15.5(Catalina)
EC-CUBE 4.0.3
MAMP 5.7
```


## MAMP được tải về và cài đặt
Đầu tiên, chuẩn bị MAMP.  

Truy cập [trang tải xuống của MAMP](https://www.mamp.info/en/mac/){:target='_blank'} và di chuyển đến trang tải xuống. Tải xuống phiên bản mới nhất của "MAMP&MAMP PRO" (trong bài này là 5.7).  

Sau khi cài đặt, hai phần mềm MAMP và MAMP PRO sẽ được cài đặt trong ứng dụng.  
Trong hướng dẫn này, chúng tôi sẽ sử dụng MAMP.  


## EC-CUBE được tải về
Tiếp theo, tải về EC-CUBE.  
Từ [trang tải xuống của EC-CUBE](https://www.ec-cube.net/download/){:target='_blank'}, tải xuống phiên bản mới nhất của EC-CUBE (trong bài này là 4.0.3)  
※ Để tải xuống, bạn cần phải đăng nhập.  

Sau khi tải xuống, giải nén.  



## MAMP được cấu hình EC-CUBE
Giải nén EC-CUBE và đặt vào thư mục htdocs (thư mục) của MAMP.  

**Cấu trúc thư mục để xác định URL của trang chủ cửa hàng:**  
`http://localhost:8888/{tên thư mục trong htdocs}/`  


```
Ví dụ: nếu bạn đặt tên thư mục là eccube-4.0.3 và đặt vào thư mục htdocs của shop, thì:
■ Cấu trúc thư mục
/Applications/MAMP/htdocs/shop/

■ URL của trang chủ cửa hàng
http://localhost:8888/shop/
```
※ Ở thời điểm này, EC-CUBE chưa được cài đặt, vì vậy không thể truy cập trang chủ cửa hàng.  


## Cấu hình phiên bản php
EC-CUBE4.0.3 được kiểm tra hoạt động với **php7.1 〜7.3**.  
Thay đổi phiên bản php trong cấu hình môi trường của MAMP.

Khởi động MAMP.  

Nhấp vào "MAMP" ở góc trên bên trái của Mac và chọn "Preferences".  
![MAMP](/images/install/gui-mac/02.png)  


![MAMP](/images/install/gui-mac/03.png)  
  
Màn hình cấu hình sẽ xuất hiện. Nhấp vào "PHP" trong mục "PHP" và kiểm tra "7.3.9", sau đó nhấp "OK".  


## Tạo cơ sở dữ liệu
Khởi động máy chủ từ MAMP.  

![MAMP](/images/install/gui-mac/07.png)  
  
Nhấp vào "Start Server".  

Màn hình trang chủ của MAMP sẽ xuất hiện.  
![MAMP](/images/install/gui-mac/04.png)  
  
Nhấp vào "TOOLS" ở thanh menu và chọn "PHPMYADMIN".  

phpMyAdmin sẽ xuất hiện.  
  
![phpMyAdmin](/images/install/gui-mac/05.png)  
  
Nhấp vào "New" và nhập tên cơ sở dữ liệu, sau đó tạo cơ sở dữ liệu.  
※ Hãy đảm bảo rằng tên cơ sở dữ liệu không dễ dàng được dự đoán từ bên ngoài.  
```
Ví dụ
Tên cơ sở dữ liệu
`eccube123_`

Thứ tự phục vụ là utf8mb4_general_ci, không có vấn đề gì.
``` 

MAMP có tài khoản cơ sở dữ liệu mặc định, chúng ta sẽ sử dụng tài khoản đó để cài đặt EC-CUBE.  
Nếu bạn muốn tạo tài khoản, hãy làm theo mục "User accounts" ở thanh menu.

※ Đối với môi trường sản xuất, hãy tạo tài khoản người dùng. Thông tin kết nối cơ sở dữ liệu (tên cơ sở dữ liệu, thông tin tài khoản, v.v.) có thể bị rò rỉ ngoài ý muốn, gây ra hậu quả nghiêm trọng như lộ thông tin cá nhân, v.v. Hãy chú ý khi quản lý.


## Cài đặt EC-CUBE

Nhấp vào URL sau từ trình duyệt:  
`http://localhost:8888/{tên thư mục EC-CUBE được tải lên}/`  
```
Ví dụ
http://localhost:8888/shop/
``` 
![install step2](/images/install/step1.png)  
Màn hình cài đặt sẽ xuất hiện. Nhấp vào "Tiếp theo" để tiếp tục.  

![install step2](/images/install/step2.png)
Nhấp vào "Tiếp theo" để tiếp tục.


### Cấu hình trang web

![install step3](/images/install/step3.png)

#### Thông tin cơ bản cửa hàng

- **Tên cửa hàng**
  - Nhập tên cửa hàng của bạn. Bạn có thể nhập tiếng Nhật.
- **Email**
  - Email này sẽ được sử dụng để gửi thông báo đặt hàng, v.v.
- **ID đăng nhập trang quản lý**
  - ID đăng nhập để đăng nhập trang quản lý. Đây là người quản lý có quyền lớn nhất, vì vậy hãy tránh sử dụng ID dễ dự đoán như "admin" v.v. Để tránh tối đa rủi ro bất hợp pháp truy cập và lộ thông tin, hãy sử dụng chuỗi ký tự không có ý nghĩa.  
- **Mật khẩu đăng nhập trang quản lý**
  - Nhập mật khẩu để người quản lý đăng nhập. Nếu bạn quên mật khẩu đăng nhập trang quản lý, bạn sẽ **không thể đăng nhập trang quản lý** vì vậy hãy ghi chú để sử dụng.  
  EC-CUBE không có **chức năng phục hồi lại mật khẩu quản lý**.  
  Hãy tạo mật khẩu phức tạp và không có ý nghĩa để người quản lý đăng nhập.  
  Không sử dụng "test1234" hoặc "password" v.v. **ĐỘC LẬP**  
- **Tên thư mục trang quản lý**  
  - Đây là URL để truy cập trang quản lý.  
  http://localhost:8888/{tên thư mục EC-CUBE được cài đặt}/{tên thư mục trang quản lý}/  để truy cập.  
  Hãy không chỉ định tên thư mục này là "admin" hoặc "dashboard" v.v. Để tránh rủi ro, hãy chỉ định tên thư mục không có ý nghĩa.
- **Buộc trang web truy cập qua SSL**  
  - Không cần nhập trong môi trường cục bộ.
- **Giới hạn truy cập trang quản lý đến IP sau**
  - Giới hạn truy cập trang quản lý đến IP cố định.  
  Trong môi trường cục bộ, không cần chỉ định.  
  Nếu bạn chỉ định IP này, chỉ có IP được chỉ định mới có thể truy cập trang quản lý.  
  Nếu bạn không có IP cố định, hãy không chỉ định.

*※ Thông tin đăng nhập trang quản lý bị rò rỉ có thể dẫn đến rủi ro lộ thông tin cá nhân và các hậu quả nghiêm trọng khác. Hãy chú ý khi quản lý.*

#### Cấu hình email
Trong môi trường cục bộ, không cần chỉ định.


### Nhập thông tin cơ sở dữ liệu 
![install step 4](/images/install/gui-win/step5.png)  
  
Nhập thông tin cơ sở dữ liệu.  
**Trong bài này, chúng ta sẽ sử dụng tài khoản cơ sở dữ liệu mặc định của MAMP.**  
  
**Cách xác định thông tin tài khoản cơ sở dữ liệu của MAMP**

Mở MAMP và nhấp vào "Open WebStart page" để khởi động trang chủ của MAMP.
![Open WebStart page](/images/install/gui-mac/01.png)  
  
Cuộn xuống, bạn sẽ thấy mục thông tin tài khoản cơ sở dữ liệu được ghi chú.  
![MySQL account](/images/install/gui-mac/06.png)  

  
Hãy nhập thông tin này theo hướng dẫn.

- **Loại cơ sở dữ liệu**
  - Trong bài này, chúng ta sẽ sử dụng MySQL.
- **Tên máy chủ cơ sở dữ liệu**
  - localhost.
- **Cổng cơ sở dữ liệu**
  - 8889
- **Tên cơ sở dữ liệu**
  - Hãy chỉ định tên cơ sở dữ liệu đã chuẩn bị. Trong ví dụ, đó là "eccube123_".
- **Tên người dùng**
  - root.
- **Mật khẩu**
  - root.

※ Tên người dùng và mật khẩu phải được tạo riêng cho môi trường sản xuất.

Sau khi nhập hết, nhấp vào "Tiếp theo" để tiếp tục.  




### Khởi tạo cơ sở dữ liệu
![install step 6](/images/install/step6.png)

Đăng ký dữ liệu khởi tạo cơ sở dữ liệu.

Nhấp vào "Tiếp theo" để tiếp tục.


### Hoàn thành cài đặt
![install step 6](/images/install/step7.png)

**Chúc mừng bạn!**  
Nếu bạn thấy màn hình này, cài đặt đã hoàn thành.  

Hướng dẫn sử dụng trang quản lý [tại đây](https://www.ec-cube.net/manual/ec-cube4/){:target="_blank"}。

Nhấp vào "Hiển thị trang quản lý" để chuyển hướng đến trang đăng nhập trang quản lý.  
[Thông tin cơ bản cửa hàng](#Thông tin cơ bản cửa hàng) để đăng nhập trang quản lý.  

Nếu bạn không thể đăng nhập, có khả năng bạn đã nhập sai ID đăng nhập hoặc mật khẩu, vì vậy hãy xóa .env của thư mục cài đặt và xóa cơ sở dữ liệu để thực hiện lại quy trình cài đặt.
