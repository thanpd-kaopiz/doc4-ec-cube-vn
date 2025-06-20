---
title: Cài đặt lên máy chủ
keywords: install
tags: [quickstart, install]
permalink: quickstart/web-installer
folder: quickstart
description: Hướng dẫn cài đặt EC-CUBE 4.
---

## Trước khi cài đặt
Hãy kiểm tra xem bạn có đáp ứng [yêu cầu hệ thống](/quickstart/requirement) hay không.

Hướng dẫn cài đặt này không giải thích về cấu hình máy chủ, cấu hình phần mềm FTP, hoặc cách sử dụng chúng. Hãy tham khảo tài liệu của nhà cung cấp máy chủ của bạn khi cần thiết.
- Sakura Internet: [https://help.sakura.ad.jp/206054522/](https://help.sakura.ad.jp/206054522/){:target="_blank"}
- Xserver: [https://www.xserver.ne.jp/manual/man_ftp_setting.php](https://www.xserver.ne.jp/manual/man_ftp_setting.php){:target="_blank"}

**Bước tiếp theo**
- [Chuẩn bị cơ sở dữ liệu](#chuẩn bị cơ sở dữ liệu)

----

## Chuẩn bị cơ sở dữ liệu
EC-CUBE sử dụng cơ sở dữ liệu MySQL hoặc PostgreSQL.
Bạn cần tạo một cơ sở dữ liệu trống mới.
Hãy tham khảo hướng dẫn của từng nhà cung cấp dịch vụ lưu trữ để biết cách tạo cơ sở dữ liệu.
- Sakura Internet: [https://help.sakura.ad.jp/360000225021/](https://help.sakura.ad.jp/360000225021/){:target="_blank"}
- Xserver: [https://www.xserver.ne.jp/manual/man_db_setting.php](https://www.xserver.ne.jp/manual/man_db_setting.php){:target="_blank"}

Sau khi tạo cơ sở dữ liệu, hãy ghi lại 4 thông tin sau:
- Tên người dùng cơ sở dữ liệu
  - Ví dụ: eccube
- Mật khẩu người dùng cơ sở dữ liệu
  - Ví dụ: ht4379reguhfdoj
- Tên máy chủ cơ sở dữ liệu
  - Ví dụ: localhost
- Tên cơ sở dữ liệu
  - Ví dụ: eccube_db

*Thông tin kết nối cơ sở dữ liệu bị rò rỉ ra ngoài có thể dẫn đến rò rỉ thông tin cá nhân. Hãy quản lý cẩn thận.*

**Bước tiếp theo**
- [Chuẩn bị tài khoản email](#chuẩn bị tài khoản email)

----

## Chuẩn bị tài khoản email
EC-CUBE sẽ tự động gửi email như email cảm ơn và email đăng ký thành viên.
Bạn cần có thông tin cấu hình của địa chỉ gửi email và máy chủ email. Hãy chuẩn bị thông tin tài khoản email theo hướng dẫn của dịch vụ email bạn sử dụng.

Thông tin cần thiết là
- Địa chỉ email
- Tên người dùng tài khoản email
- Mật khẩu tài khoản email
- Địa chỉ máy chủ email

*Thông tin tài khoản email bị rò rỉ ra ngoài có thể dẫn đến rò rỉ thông tin cá nhân. Hãy quản lý cẩn thận.*

**Bước tiếp theo**
- [Tải lên tệp mã nguồn EC-CUBE lên máy chủ](#tải lên tệp mã nguồn ec-cube lên máy chủ)

----

## Tải lên tệp mã nguồn EC-CUBE lên máy chủ
Để cài đặt, cần phải có tệp mã nguồn của EC-CUBE được triển khai trên máy chủ.

Bạn có thể sử dụng phần mềm chuyển tệp như FileZilla, nhưng do số lượng tệp của EC-CUBE rất lớn, nên có thể gặp lỗi khi tải lên tất cả các tệp cùng một lúc. Vì vậy, chúng tôi khuyên bạn nên sử dụng [EC-CUBE Downloader](#ec-cube-downloader-sử-dụng-để-giải-nén-tệp-mã-nguồn) để giải nén tệp mã nguồn.

**Bước tiếp theo**
- [EC-CUBE Downloader](#ec-cube-downloader-sử-dụng-để-giải-nén-tệp-mã-nguồn)
- [Tải lên tệp mã nguồn EC-CUBE lên máy chủ](#tải lên tệp mã nguồn ec-cube lên máy chủ)

----

### EC-CUBE Downloader
EC-CUBE Downloader là phần mềm được phát triển bởi cộng đồng và có thể giải nén tệp mã nguồn của EC-CUBE một cách đơn giản.
![EC-CUBE Donwloader screen shot](https://github.com/tao-s/eccube-downloader/raw/master/EC-CUBE_downloader.gif)

[Tải EC-CUBE Downloader từ đây](https://github.com/tao-s/eccube-downloader/archive/master.zip) và làm theo các bước sau:

1. Giải nén tệp master.zip.
1. Sao chép tệp **dw.php** từ thư mục đã giải nén vào thư mục của bạn trên máy chủ. Ví dụ: public_html/ 
1. Truy cập **dw.php** từ trình duyệt (chúng tôi khuyên nên sử dụng Google Chrome). Ví dụ: https://www.example.co.jp/dw.php
1. Nhấp vào "**Bắt đầu tải xuống**".
1. Sau một lúc, màn hình cài đặt EC-CUBE sẽ xuất hiện.

Nếu màn hình cài đặt EC-CUBE xuất hiện, hãy tiếp tục đến [Trình hướng dẫn cài đặt](#trình-hướng-dẫn-cài-đặt)

**Bước tiếp theo**
- [Trình hướng dẫn cài đặt](#trình-hướng-dẫn-cài-đặt)

----

### Tải lên tệp mã nguồn EC-CUBE lên máy chủ
**Nếu bạn đã sử dụng [EC-CUBE Downloader](#ec-cube-downloader-sử-dụng-để-giải-nén-tệp-mã-nguồn), bạn có thể bỏ qua bước này.**

Tải [EC-CUBE 4 Package](https://www.ec-cube.net/download/){:target='_blank'} và giải nén nó.

Sử dụng phần mềm chuyển tệp như FileZilla để tải tệp lên máy chủ.  
*Lưu ý: Do số lượng tệp lớn, có thể gặp lỗi khi tải lên tất cả các tệp cùng một lúc. Nếu gặp lỗi, hãy tải lên từng phần.*

Truy cập trình duyệt EC-CUBE từ địa chỉ:  
- Ví dụ: `http://example.com/{EC-CUBE được tải lên thư mục}`

Nếu màn hình cài đặt EC-CUBE xuất hiện, hãy tiếp tục đến [Trình hướng dẫn cài đặt](#trình-hướng-dẫn-cài-đặt)

*Lưu ý: Thông tin kết nối FTP/SFTP bị rò rỉ ra ngoài có thể dẫn đến rò rỉ thông tin thẻ tín dụng và các thông tin cá nhân khác. Hãy quản lý cẩn thận.*

**Bước tiếp theo**
- [Trình hướng dẫn cài đặt](#trình-hướng-dẫn-cài-đặt)

----

## Trình hướng dẫn cài đặt
EC-CUBE mã nguồn được giải nén sau đó, truy cập vào thư mục cài đặt để xem màn hình cài đặt.
Hãy làm theo hướng dẫn cài đặt để hoàn thành cài đặt.

*URL ví dụ của màn hình cài đặt: https://wwww.example.com/{EC-CUBE được tải lên thư mục/}/index.php/install/step1*

![install step1](/images/install/step1.png)
Nhấp vào *Tiếp tục* để tiếp tục.

### Kiểm tra quyền truy cập (quyền truy cập tệp)

![install step2](/images/install/step2.png)
Nhấp vào *Tiếp tục* để tiếp tục.

----

### Cấu hình trang web

![install step3](/images/install/step3.png)

#### Thông tin cơ bản của cửa hàng

- **Tên cửa hàng**
  - Nhập tên cửa hàng của bạn. Bạn có thể nhập bằng tiếng Nhật.
- **Email**
  - Email này sẽ nhận thông báo đặt hàng từ hệ thống.
- **ID đăng nhập trang quản lý**
  - ID đăng nhập để đăng nhập vào trang quản lý. Đây là người dùng có quyền cao nhất, vì vậy ID như "admin" hoặc các ID dễ đoán sẽ dẫn đến việc truy cập không hợp lệ và thông tin bị rò rỉ. Hãy tránh đặt ID này. Hãy đặt một chuỗi văn bản không có ý nghĩa.
- **Mật khẩu trang quản lý**
  - Nhập mật khẩu để người dùng có quyền truy cập vào trang quản lý. Nếu bạn quên mật khẩu này, **bạn sẽ không thể đăng nhập vào trang quản lý** vì EC-CUBE không có chức năng đặt lại mật khẩu cho người dùng. Hãy nhập mật khẩu phức tạp và không có ý nghĩa như "test1234" hoặc "password". **Đây là rất nguy hiểm, hãy tránh đặt mật khẩu này**.
- **Tên thư mục trang quản lý**
  - Nhập URL để truy cập vào trang quản lý. Trang quản lý sẽ truy cập vào
  https://www.example.com/{EC-CUBE được cài đặt thư mục}/{tên thư mục trang quản lý}/ 
  Hãy đặt tên thư mục này không giống như "admin" hoặc "dashboard" vì có thể bị đoán. Hãy đặt một chuỗi văn bản không có ý nghĩa.
- **Buộc trang web truy cập qua SSL**
  - Trang web chỉ có thể truy cập được qua https://〜
  Hãy đảm bảo thực hiện cấu hình SSL trên máy chủ trước khi bật chức năng này. **Nếu không thực hiện cấu hình SSL, trang web sẽ không thể truy cập được**.
- **Giới hạn truy cập trang quản lý đến IP sau đây**
  - Giới hạn truy cập trang quản lý đến địa chỉ IP cố định. Nếu bạn đặt IP ở đây, chỉ có IP đó mới có thể truy cập vào trang quản lý. Lưu ý, điều này có thể làm mất đi tính tiện lợi khi truy cập từ điện thoại di động của bạn.
  Nếu bạn không có IP cố định, hãy không đặt IP này.

*Lưu ý: Thông tin truy cập trang quản lý bị rò rỉ ra ngoài có thể dẫn đến rò rỉ thông tin cá nhân và các hành vi trốn tránh thanh toán. Hãy quản lý cẩn thận.*

#### Cấu hình email
Nhập thông tin tài khoản email đã chuẩn bị ở [Chuẩn bị tài khoản email](#chuẩn bị tài khoản email)

*Lưu ý: Nếu bạn muốn gửi email từ máy chủ cài đặt EC-CUBE bằng cách sử dụng sendmail, bạn cần thực hiện cấu hình khác.*

Nhấp vào *Tiếp tục* để tiếp tục.

**Bước tiếp theo**
- [Nhập thông tin cơ sở dữ liệu](#nhập-thông-tin-cơ-sở-dữ-liệu)

----

### Nhập thông tin cơ sở dữ liệu 
![install step 4](/images/install/step5.png)
Nhập thông tin cơ sở dữ liệu đã chuẩn bị ở [Chuẩn bị cơ sở dữ liệu](#chuẩn bị cơ sở dữ liệu)

- **Loại cơ sở dữ liệu**
  - Chọn loại cơ sở dữ liệu đã chuẩn bị ở [Chuẩn bị cơ sở dữ liệu](#chuẩn bị cơ sở dữ liệu). Đối với môi trường sản xuất, hãy sử dụng MySQL hoặc PostgreSQL.
- **Tên máy chủ cơ sở dữ liệu**
  - Nếu máy chủ cơ sở dữ liệu của bạn cũng chạy MySQL, nó có thể là localhost hoặc 127.0.0.1.
- **Cổng cơ sở dữ liệu**
  - Nếu máy chủ cơ sở dữ liệu của bạn không có đặc biệt, bạn không cần chỉ định nó.
- **Tên cơ sở dữ liệu**
  - Nhập tên cơ sở dữ liệu đã chuẩn bị ở [Chuẩn bị cơ sở dữ liệu](#chuẩn bị cơ sở dữ liệu). Đối với MySQL và PostgreSQL, đây không phải là tên cơ sở dữ liệu như "eccube_db".
- **Tên người dùng**
  - Đây không phải là ID người dùng trang quản lý như "eccube" mà là ID người dùng cơ sở dữ liệu đã chuẩn bị ở [Chuẩn bị cơ sở dữ liệu](#chuẩn bị cơ sở dữ liệu).
- **Mật khẩu**
  - Đây không phải là mật khẩu đăng nhập trang quản lý như "eccube" mà là mật khẩu của người dùng cơ sở dữ liệu đã chuẩn bị ở [Chuẩn bị cơ sở dữ liệu](#chuẩn bị cơ sở dữ liệu).

Nhấp vào *Tiếp tục* để tiếp tục.

**Bước tiếp theo**
- [Khởi tạo cơ sở dữ liệu](#khởi-tạo-cơ-sở-dữ-liệu)

----

### Khởi tạo cơ sở dữ liệu
![install step 6](/images/install/step6.png)

Đăng ký dữ liệu khởi tạo cơ sở dữ liệu.

Nhấp vào *Tiếp tục* để tiếp tục.

**Bước tiếp theo**
- [Hoàn thành cài đặt](#hoàn-thành-cài-đặt)

----

### Hoàn thành cài đặt
![install step 6](/images/install/step7.png)

**Chúc mừng bạn!** Nếu màn hình này xuất hiện, cài đặt đã hoàn thành. Hãy đăng nhập vào trang quản lý để thêm thông tin cửa hàng và đăng ký hàng hóa, chuẩn bị mở cửa hàng của bạn.

Cách sử dụng trang quản lý được hướng dẫn [ở đây](https://www.ec-cube.net/manual/ec-cube4/){:target="_blank"}.

Nhấp vào *Hiển thị trang quản lý* để chuyển hướng đến trang đăng nhập trang quản lý. Hãy đăng nhập vào trang quản lý bằng thông tin người quản lý đã nhập ở [Thông tin cơ bản của cửa hàng](#thông-tin-cơ-bản-của-cửa-hàng)

Nếu bạn không thể đăng nhập, có khả năng bạn đã quên mật khẩu hoặc ID đăng nhập, vì vậy hãy xóa .env của thư mục cài đặt và xóa cơ sở dữ liệu để thực hiện lại quy trình cài đặt.

----

### Lỗi thường gặp khi cài đặt

Dưới đây là những điểm mà người mới bắt đầu thường gặp phải, vì vậy hãy kiểm tra:

Nếu có lỗi khác, hãy tìm kiếm trên [Cộng đồng phát triển](https://xoops.ec-cube.net/){:target="_blank"} hoặc hỏi câu hỏi trên đó.

Ngoài ra, hãy đến các buổi học thực hành được tổ chức tại các nơi khác nhau [Nhóm người dùng](https://www.ec-cube.net/news/#events_information){:target="_blank"} để nghe.

#### Không thể kết nối đến cơ sở dữ liệu

- Máy chủ cơ sở dữ liệu không khởi động
  - Hãy khởi động lại máy chủ cơ sở dữ liệu.
- Thông tin cơ sở dữ liệu bị sai
  - Hãy kiểm tra lại tên máy chủ, tên người dùng, mật khẩu và tên cơ sở dữ liệu.
- Vấn đề mạng
  - Hãy kiểm tra xem máy chủ cài đặt EC-CUBE có thể kết nối đến máy chủ cơ sở dữ liệu hay không.

#### Lỗi quyền truy cập (quyền truy cập tệp)
Hãy xem [đây](/quickstart/permission/#quyền-truy-cập-của-tệp-về-quyền-truy-cập-chung) để kiểm tra quyền truy cập.

#### Khác

- PHP không phù hợp/PHP không có các module cần thiết
  - Hãy kiểm tra [yêu cầu hệ thống](/quickstart/requirement). EC-CUBE hoạt động cần PHP Ver.7.1 trở lên.
