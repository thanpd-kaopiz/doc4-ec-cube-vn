---
title: ec-cube.co FAQ
keywords: co ec-cube.co Cloud version FAQ
tags: [co, ec-cube.co]
permalink: co/co_faq
folder: co
---

---

Tổng hợp các câu hỏi thường gặp.

<style>
.page__content h2{ 
  font-size: 22px !important;
  padding-top: 2.5rem !important;
}
.page__content h2:nth-of-type(1){
  padding-top: 0 !important;
}
.page__content h3{
  font-size: 17px !important;
  padding: 1.5rem 1.5rem .5rem !important;
  border-bottom: 1px solid #f2f3f3!important;
  margin: 1rem 0 1rem!important;
  position: relative;
}
.page__content h3::before{
  content: "Q.";
  display: block;
  position: absolute;
  bottom: .4rem;
  left: 0;
  font-size: 22px;
  font-weight: bold;
  color: #40ACAC;
}
.page__content h3::after{
  content: "A.";
  display: block;
  position: absolute;
  bottom: -2.1rem;
  left: 5px;
  font-size: 16px;
  font-weight: bold;
}
.page__content > p{
  font-size: 14px !important;
  padding-left: 1.5rem !important;
}
.page__content > ul,
.page__content > ol{
  font-size: 14px !important;
  padding-left: 1.0rem !important;
  margin-left: 1.0rem !important;
}
.page__content li{
  font-size: 14px !important;
  margin-left: 1.0rem !important;
}
.toc__menu li{
  font-size: 14px !important;
  margin-left: 0 !important;
}
.toc__menu li ul li a{
  font-size: 12px !important;
  padding: .5rem 1rem !important;
}
</style>

## Cơ sở dữ liệu (DB)

### Có thể truy cập trực tiếp DB của ec-cube.co bằng công cụ client DB không?

Vì lý do bảo mật và vận hành, việc kết nối trực tiếp là không thể. Mong bạn thông cảm.

### Có thể thay đổi schema DB không?

Không thể trên môi trường trial. Sau khi đăng ký gói Standard, bạn có thể thực hiện thông qua vùng tuỳ biến. Xem thêm tại [Hướng dẫn mở rộng Entity](https://doc4.ec-cube.net/customize_entity#%E5%9F%BA%E6%9C%AC%E3%81%AE%E6%8B%A1%E5%BC%B5%E6%96%B9%E6%B3%95){:target="_blank"}.

### Chỉ hỗ trợ PostgreSQL phải không?

Đúng vậy, chỉ hỗ trợ PostgreSQL.

## Khác biệt với bản download

### ec-cube.co khác gì so với bản download?

Chức năng chính dựa trên EC-CUBE4 bản download, giống nhau. Bạn có thể sử dụng các plugin, template thiết kế tương tự bản download. Sau khi đăng ký gói Standard, bạn có thể mở rộng chức năng qua thư mục Customize.

## Google Analytics (Phân tích truy cập)

### Làm sao để cài đặt Google Analytics?

Bạn có thể sử dụng plugin trên [Owner's Store](https://www.ec-cube.net/owners/){:target="_blank"}:
- [Plugin Google Analytics eCommerce/Enhanced eCommerce cho EC-CUBE4](https://www.ec-cube.net/products/detail.php?product_id=1715){:target="_blank"}
- [Plugin Google Analytics E-Commerce/User-ID cho 4.0](https://www.ec-cube.net/products/detail.php?product_id=1722){:target="_blank"}

## Web API

### Có thể sử dụng Web API không? Có thể làm gì với WebAPI?

Bạn có thể sử dụng [Plugin EC-CUBE Web API](https://www.ec-cube.net/products/detail.php?product_id=2121){:target="_blank"}. Xem chi tiết tại [Tài liệu phát triển](https://doc.ec-cube.net/eccube-api4/){:target="_blank"}.

## Giới hạn truy cập

### Muốn giới hạn truy cập vào site thì làm thế nào?

Tùy mục đích mà cách thực hiện khác nhau:
- Vận hành site chỉ cho hội viên: dùng plugin trên Owner's Store, tìm với từ khóa "closed", "hội viên", "đăng ký hội viên".
- Giới hạn truy cập admin: vào Quản trị > Cài đặt > Cài đặt hệ thống > Quản lý bảo mật để cài đặt giới hạn IP.
- Giới hạn toàn site bằng .htaccess: không còn hỗ trợ cài đặt Basic Auth qua support. Để ẩn front khi xây dựng site, dùng chức năng bảo trì (Maintenance) từ bản 4.1.2 trở lên. Khi bật chế độ bảo trì, chỉ admin đã đăng nhập mới xem được front. Tuy nhiên, một số chức năng như thanh toán có thể không hoạt động khi bật maintenance.

## Giới hạn upload

### Có giới hạn upload file không?

Có. Mỗi file upload tối đa 10MB.

### Có thể yêu cầu tăng giới hạn upload hoặc tuỳ biến không?

Không thể. Mong bạn thông cảm.

## Lỗi/Hoạt động không ổn định

### Khi thao tác bị lỗi hoặc không ổn định thì làm gì?

Hãy liên hệ [Hỗ trợ ec-cube.co](https://www.ec-cube.net/product/co/support.php){:target="_blank"} và cung cấp các thông tin sau để được hỗ trợ nhanh:
- URL site cần kiểm tra
- Mô tả hiện tượng, thao tác gây ra lỗi
- Thời điểm xảy ra
- Đã khắc phục được chưa hay vẫn còn
- Có thay đổi gì trước khi xảy ra lỗi không

### Không làm gì nhưng menu admin bị ẩn đi?

Có thể do cache không đồng bộ. Hãy thử xóa cache trong quản trị. Nếu không được, liên hệ [Hỗ trợ ec-cube.co](https://www.ec-cube.net/product/co/support.php){:target="_blank"} và cung cấp các thông tin như trên.

## Tuỳ biến

### Làm sao miễn phí vận chuyển khi tổng tiền vượt mức?

Vào Quản trị > Cài đặt > Cài đặt cơ bản > Cài đặt phí vận chuyển để cài đặt điều kiện miễn phí.

### Muốn cài đặt phí vận chuyển, nơi gửi theo từng sản phẩm?

Sử dụng chức năng [Phân loại bán hàng](https://www.ec-cube.net/manual/ec-cube4/product/product_new.php){:target="_blank"}.

### Muốn cài đặt "Nhận tại cửa hàng" trong phương thức giao hàng?

Cần tuỳ biến code core. Tuy nhiên, có thể thực hiện như sau:
1. Tạo phương thức giao hàng "Nhận tại cửa hàng" trong Quản trị > Cài đặt > Cài đặt cửa hàng > Cài đặt phương thức giao hàng, nhập tên cửa hàng vào mục "Thời gian giao".
2. Tuỳ biến code trong Quản trị > Quản lý nội dung > Quản lý JavaScript để ẩn mục "Ngày giao" và đổi "Thời gian giao" thành "Cửa hàng nhận" khi chọn "Nhận tại cửa hàng".

Lưu ý: Trên quản lý đơn hàng, mục "Thời gian giao" sẽ hiển thị tên cửa hàng nhận, không thể tuỳ biến thêm.

### Muốn đổi favicon?

Vào Quản trị > Quản lý nội dung > Quản lý file, upload favicon.ico vào assets > img > common.

### Chỉ có thể tuỳ biến bằng plugin riêng hay có thể tuỳ biến core?

Sau khi đăng ký gói Standard, bạn có thể tuỳ biến qua thư mục Customize. Có thể dùng plugin riêng, nhưng các vấn đề phát sinh từ plugin riêng sẽ không được hỗ trợ. Việc tuỳ biến core đang được xem xét cho các gói mới.

### Muốn thêm trường tuỳ ý cho sản phẩm?

Có thể dùng plugin trên Owner's Store, ví dụ: [Plugin thêm trường thông tin sản phẩm](https://www.ec-cube.net/products/detail.php?product_id=1713){:target="_blank"}.

### Muốn tuỳ biến hoá đơn giao hàng?

Không thể trên môi trường trial. Sau khi đăng ký gói Standard, có thể thực hiện tuỳ vào cách triển khai.

### Có thể thêm trạng thái đơn hàng không?

Không thể, vì cần thay đổi cả chương trình. Xem thêm tại [Github Issue](https://github.com/EC-CUBE/ec-cube/issues/4299){:target="_blank"}.

### Cách thay đổi thiết kế front?

Vào Quản trị > Quản lý nội dung >
- Quản lý CSS
- Quản lý JavaScript

Bạn có thể cập nhật code để thay đổi thiết kế front. Ngoài ra, có thể upload template thiết kế riêng. Tuy nhiên, các vấn đề phát sinh từ template riêng sẽ không được hỗ trợ. Không thể chỉnh sửa trực tiếp file (default_frame.twig) từ quản trị.

### Có thể tích hợp Instagram Shopping không?

Có plugin trên Owner's Store:
[Plugin quản lý bài đăng Instagram cho EC-CUBE4](https://www.ec-cube.net/products/detail.php?product_id=2356){:target="_blank"}

Ngoài ra còn nhiều plugin khác, hãy tìm kiếm trên [Owner's Store](https://www.ec-cube.net/owners/){:target="_blank"}.
Lưu ý: Plugin Facebook hiện không sử dụng được.

### Có thể thêm chức năng thêm vào giỏ hàng nhanh, hiển thị sản phẩm đã xem gần đây trên header không?

Có thể thực hiện bằng tuỳ biến sau khi đăng ký gói Standard.

### Muốn cài đặt meta tag cho SEO?

Vào Quản trị > Quản lý nội dung > Quản lý trang, cài đặt meta ở cuối mỗi trang.

### Muốn đổi logo trên hoá đơn giao hàng?

Vào Quản trị > Quản lý nội dung > Quản lý file, upload logo mới.

### Có thể tuỳ biến gì?

- Tuỳ biến trong phạm vi quản trị
- Tuỳ biến bằng plugin, template thiết kế
- Tuỳ biến qua thư mục Customize
- Tuỳ biến bằng plugin/template riêng (không hỗ trợ lỗi phát sinh)

Không thể tuỳ biến core.

### Đã thay đổi code trong quản lý nội dung, muốn khôi phục về mặc định?

Mã nguồn EC-CUBE sử dụng trên ec-cube.co được công khai tại [co/master branch](https://github.com/EC-CUBE/ec-cube/tree/co/master){:target="_blank"}. Hãy tham khảo và copy code về môi trường của bạn.

### Có thể tuỳ biến plugin của các bên khác không?

Tuỳ vào license của từng plugin, EC-CUBE không thể trả lời. Hãy kiểm tra thông tin license trên trang chi tiết plugin và liên hệ nhà cung cấp.

### Muốn được hỗ trợ về thiết kế?

Liên hệ [Hỗ trợ ec-cube.co](https://www.ec-cube.net/product/co/support.php){:target="_blank"} hoặc [Đối tác tích hợp EC-CUBE](https://www.ec-cube.net/integrate/partner/){:target="_blank"}.

### Có cách nào tuỳ biến mà không sửa code core không?

Có thể override class hoặc parameter mà không sửa code core. Tham khảo:
- [Override class core trên EC-CUBE4](https://qiita.com/chihiro-adachi/items/b3bb70e6abbc0f824965){:target="_blank"}
- [Override parameter trên EC-CUBE4](https://qiita.com/chihiro-adachi/items/7edaf82845f9352d6500){:target="_blank"}

## Di chuyển site

### Hướng dẫn di chuyển từ bản download (2.x, 3.x) sang ec-cube.co?

Xem [Hướng dẫn di chuyển dữ liệu 2.x, 3.x](https://www.ec-cube.co/pdf/migration_manual_flow.pdf){:target="_blank"}. Nếu có vấn đề không có trong tài liệu, liên hệ [Hỗ trợ ec-cube.co](https://www.ec-cube.net/product/co/support.php){:target="_blank"}.

### Hướng dẫn di chuyển từ ec-cube.co sang bản download?

Có thể thực hiện có phí. Liên hệ [Hỗ trợ ec-cube.co](https://www.ec-cube.net/product/co/support.php){:target="_blank"} và cung cấp:
- URL site
- Thời gian mong muốn lấy dữ liệu

Thông tin cung cấp gồm:
- DB
- Mã nguồn
- Ảnh sản phẩm

Lưu ý: Sau 1 tuần kể từ khi dừng môi trường ec-cube.co, dữ liệu sẽ bị xoá và không thể cung cấp lại.

## Quy mô site

### Dịch vụ phù hợp quy mô nào?

Phù hợp từ site nhỏ đến vừa và lớn.

## Bảo mật

### Có hỗ trợ SSL không?

Đã hỗ trợ SSL toàn thời gian.

### Có đáp ứng PCI DSS không?

Không đáp ứng PCI DSS. Về không lưu trữ thông tin thẻ, hãy dùng plugin thanh toán trên Owner's Store.

### Trên môi trường 4.1, mục "Tên host tin cậy" trong quản lý bảo mật là gì? Có cần thay đổi không?

Không cần thay đổi, đã được cài đặt tự động. Khi đổi domain, EC-CUBE sẽ hỗ trợ cài đặt lại. Nếu lỡ thay đổi và không truy cập được site, liên hệ [Hỗ trợ ec-cube.co](https://www.ec-cube.net/product/co/support.php){:target="_blank"} để khôi phục.

## Bán hàng sản phẩm download

### Có thể bán sản phẩm download không?

Có, nhưng mỗi file upload tối đa 10MB. Nên dùng dịch vụ ngoài như CDN nếu cần.

## Dữ liệu/Nội dung

### Muốn xoá hàng loạt đơn hàng test trên production?

Dùng plugin trên Owner's Store:
- 4.2: [Plugin xoá đơn hàng hàng loạt cho EC-CUBE4.2](https://www.ec-cube.net/products/detail.php?product_id=2851){:target="_blank"}
- 4.0~4.1: [Plugin xoá đơn hàng hàng loạt cho EC-CUBE4](https://www.ec-cube.net/products/detail.php?product_id=2101){:target="_blank"}

### Muốn cập nhật DB production mới nhất?

Liên hệ [Hỗ trợ ec-cube.co](https://www.ec-cube.net/product/co/support.php){:target="_blank"} và cung cấp:
- URL site
- Nội dung yêu cầu (ví dụ: cập nhật DB)

## Template thiết kế

### Có thể dùng template thiết kế nào trên ec-cube.co?

Xem danh sách template tại [đây](https://www.ec-cube.net/products/list.php?category_id=7&ecversion=4.0){:target="_blank"}. Lưu ý: file trên 10MB sẽ bị lỗi khi upload.

## Domain

### Có thể dùng domain riêng không? Cài đặt SSL thế nào?

Có thể dùng domain riêng. SSL sẽ được cài đặt cùng lúc chuyển domain. Xem quy trình tại [PDF: Quy trình cài đặt domain riêng](https://www.ec-cube.net/user_data/packages/default/img/product/co/original_domain_setting.pdf){:target="_blank"}.
Chỉ hỗ trợ subdomain, không hỗ trợ root domain.

```
Không được: https://example.com
Được: https://www.example.com
Được: https://shop.example.com
```

## Plugin

### Muốn cài plugin thanh toán, có thể dùng plugin nào?

Xem danh sách plugin thanh toán tại [đây](https://www.ec-cube.net/products/list.php?ecversion=4.0&category_id=3){:target="_blank"}.
Lưu ý: Plugin "Repeat Cube" không thể cài đặt thông thường, liên hệ [Hỗ trợ ec-cube.co](https://www.ec-cube.net/product/co/support.php){:target="_blank"} nếu cần.
Nếu dùng plugin ngoài danh sách, site có thể bị dừng theo [Điều khoản sử dụng ec-cube.co](https://www.ec-cube.co/pdf/term.pdf){:target="_blank"}.

### Cài nhiều plugin có làm chậm site không?

Có site cài hơn 20 plugin vẫn hoạt động tốt. Tuy nhiên, tuỳ vào cách lập trình của từng plugin mà có thể ảnh hưởng hiệu năng.

### Cài nhiều plugin có thể gây xung đột không?

Có thể, tuỳ vào sự kết hợp plugin. Không thể cung cấp thông tin xung đột chi tiết do số lượng plugin lớn.

### Sau khi cài plugin bị lỗi server, không truy cập được site?

Có thể do cache. Nếu không đăng nhập được admin, liên hệ [Hỗ trợ ec-cube.co](https://www.ec-cube.net/product/co/support.php){:target="_blank"} và cung cấp:
- URL site
- Plugin gây lỗi
- Thời điểm xảy ra
- Thay đổi trước khi lỗi (nếu có)

Để tránh lỗi, hãy chuyển site sang chế độ bảo trì trước khi cài/upgrade plugin.

## Email

### Khách hàng không nhận được email mua hàng?

Kiểm tra xem email có bị chặn hoặc vào spam không. Nếu không phải, liên hệ [Hỗ trợ ec-cube.co](https://www.ec-cube.net/product/co/support.php){:target="_blank"} và cung cấp:
- URL site
- Đơn hàng bị lỗi
- Thời điểm xảy ra
- Các đơn hàng khác có bị không
- Thay đổi trước khi lỗi (nếu có)

## Email marketing

### Có thể gửi email marketing không?

Giới hạn 12.000 email/tháng. Nếu vượt, hãy dùng dịch vụ ngoài. Có thể dùng plugin trên Owner's Store:
- [Plugin quản lý email marketing](https://www.ec-cube.net/products/detail.php?product_id=1760){:target="_blank"}
- [Plugin gửi email marketing đơn giản x GreenForm (4.x)](https://www.ec-cube.net/products/detail.php?product_id=1859){:target="_blank"}
- [Plugin PostCarrier cho EC-CUBE4](https://www.ec-cube.net/products/detail.php?product_id=1940){:target="_blank"}

Có template email marketing:
- [HTML Email Magazine Template No.EM001](https://www.ec-cube.net/products/detail.php?product_id=2114){:target="_blank"}
- [HTML Email Magazine Template No.EM002](https://www.ec-cube.net/products/detail.php?product_id=2115){:target="_blank"}

## Vận hành

### Muốn đăng ký hàng loạt sản phẩm?

Có thể import file CSV sản phẩm từ quản trị. Không giới hạn số lượng (đã kiểm tra với 10.000 sản phẩm).

### Có giới hạn số lượng sản phẩm hoặc dung lượng dữ liệu không?

Không giới hạn. Tuy nhiên, mỗi lần upload dữ liệu tối đa 10MB. Nếu đăng ký quá nhiều sản phẩm, hiệu năng site có thể giảm.

### Muốn đăng ký hơn 1000 thuộc tính cho 1 sản phẩm?

Cần tăng php_value max_input_vars lên trên 1000, nhưng không thể thay đổi trên ec-cube.co vì lý do bảo mật và tài nguyên. Hãy chia nhỏ sản phẩm.

## Phát triển

### Muốn thuê phát triển site hoặc giới thiệu công ty phát triển?

Hãy liên hệ [EC-CUBE Advisor](https://www.ec-cube.net/advisor/){:target="_blank"} hoặc [Đối tác tích hợp EC-CUBE](https://www.ec-cube.net/integrate/partner/){:target="_blank"}.

## Kết nối dịch vụ ngoài

### Muốn dùng dịch vụ ngoài thì làm thế nào?

Có thể cài plugin tích hợp dịch vụ ngoài từ Owner's Store, hoặc tuỳ biến qua thư mục Customize/plugin riêng sau khi đăng ký gói Standard. Lưu ý:
- Chỉ dùng plugin thanh toán tải từ Owner's Store
- Không hỗ trợ lỗi phát sinh từ plugin/template riêng

Nếu dùng plugin thanh toán ngoài Owner's Store, site có thể bị dừng theo [Điều khoản sử dụng ec-cube.co](https://www.ec-cube.co/pdf/term.pdf){:target="_blank"}.

## Kết nối môi trường

### Có thể thao tác trực tiếp trên môi trường production không?

Chỉ giới hạn ở:
- Quản trị
- Console cung cấp sau khi đăng ký gói Standard

Nếu muốn upload ảnh hàng loạt, dùng [Plugin upload ảnh sản phẩm hàng loạt](https://www.ec-cube.net/products/detail.php?product_id=1957){:target="_blank"}.
Không thể kết nối trực tiếp qua SSH/telnet/SFTP/FTP.

## Giám sát

### Có giám sát tài nguyên không?

Có giám sát tài nguyên. Xem thêm tại [Giám sát & Monitoring](http://localhost:4000/co/co_security#%E7%9B%A3%E8%A6%96%E3%83%A2%E3%83%8B%E3%82%BF%E3%83%AA%E3%83%B3%E3%82%B0){:target="_blank"}.

## Chức năng

### EC-CUBE có những chức năng gì?

Xem tại:
- [Danh sách chức năng EC-CUBE4](https://www.ec-cube.net/product/functions.php){:target="_blank"}
- [Hướng dẫn quản trị EC-CUBE4](https://www.ec-cube.net/manual/ec-cube4/){:target="_blank"}

## Thanh toán

### Muốn cho phép thanh toán toàn bộ bằng điểm thì làm thế nào?

Nếu cổng thanh toán không hỗ trợ thanh toán 0 đồng, hãy đăng ký phương thức thanh toán "0 đồng" hoặc "Thanh toán toàn bộ bằng điểm".

## Xử lý sự cố

### Khi có sự cố, EC-CUBE sẽ hỗ trợ thế nào?

Sau khi nhận được liên hệ hoặc phát hiện cảnh báo, EC-CUBE sẽ kiểm tra và phản hồi.

### Khi phát hiện sự cố, có gửi email cho khách hàng không?

Có thể cài đặt gửi email cho 1 địa chỉ email/site khi có yêu cầu. Không hỗ trợ nhiều email.

## Upload video giới thiệu sản phẩm

### Muốn upload video giới thiệu sản phẩm lên site thì làm thế nào?

Có thể upload, nhưng mỗi file tối đa 10MB. Nên dùng dịch vụ ngoài như CDN nếu cần.

## Cài đặt

### Địa chỉ IP gửi đi có cố định không?

Có, là IP cố định. Sau khi đăng ký gói Standard, có thể xem IP trên màn hình Console. Nếu cần biết IP sau khi đăng ký trial, liên hệ [Hỗ trợ ec-cube.co](https://www.ec-cube.net/product/co/support.php){:target="_blank"} và cung cấp:
- URL site
- Nội dung yêu cầu: Muốn biết IP

## Plugin/Template riêng

### Có thể tự làm plugin/template riêng không?

Có thể, nhưng các lỗi phát sinh sẽ không được hỗ trợ. Hãy cân nhắc sử dụng plugin/template trên Owner's Store.

#### Liên hệ

Ngoài [Hỗ trợ ec-cube.co](https://www.ec-cube.net/product/co/support.php){:target="_blank"}, bạn có thể tham khảo:
- Muốn hỏi đáp nhanh về lỗi nhỏ: [Cộng đồng phát triển EC-CUBE](https://xoops.ec-cube.net/){:target="_blank"}
- Muốn tìm hiểu kỹ thuật về ec-cube.co/EC-CUBE: [Tài liệu phát triển EC-CUBE 4](https://doc4.ec-cube.net/){:target="_blank"}
- Muốn hỏi trực tiếp chuyên gia: Tham gia các nhóm người dùng, sự kiện, seminar tại [Tin tức & Sự kiện & Cộng đồng](https://www.ec-cube.net/news/#events_information){:target="_blank"}
- Muốn thuê xây dựng site: [Đối tác tích hợp EC-CUBE](https://www.ec-cube.net/integrate/partner/){:target="_blank"}
- Không biết chọn đối tác nào: [EC-CUBE Advisor](https://www.ec-cube.net/advisor/){:target="_blank"}
