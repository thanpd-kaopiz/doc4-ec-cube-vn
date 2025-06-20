---
title: Cách thăm dò thủ công
permalink: /penetration-testing/testing/manual_explore
---
Khám phá tất cả các trang bằng Firefox đã thiết lập Local Proxes.
Các trang có thể truy cập bằng GET có thể phát hiện bằng chức năng import `containing urls` hoặc Spider, nên hãy tập trung thăm dò các form chuyển trang bằng POST.

**Lưu ý:** Khi thăm dò thủ công, hãy chú ý không logout giữa chừng.
Nếu logout, token CSRF sẽ thay đổi và quét động có thể thất bại.
{: .notice--danger}

Để token CSRF không bị thay đổi trong quá trình kiểm thử, bí quyết là lặp lại **thăm dò thủ công → quét động** theo từng chức năng.

### Form nhập tiếng Nhật

Với các form bắt buộc nhập tiếng Nhật như tên Kana, hãy chắc chắn nhập tiếng Nhật khi thăm dò thủ công.
Việc này giúp quét động cũng kiểm thử với dữ liệu tiếng Nhật.

### Pattern chuyển trang đặc biệt

#### Trường hợp điều khiển chuyển trang bằng tham số mode trong POST

Với các chức năng có pattern chuyển trang như **Nhập form → Màn hình xác nhận → Màn hình hoàn tất**, có 2 loại pattern lớn:

**1. Trường hợp màn hình nhập, xác nhận, hoàn tất được phân biệt bằng URL**

| Màn hình | Nhập         | Xác nhận             | Hoàn tất                |
|----------|--------------|----------------------|-------------------------|
| URL      | `/shopping`  | `/shopping/confirm`  | `/shopping/complete`    |

**2. Trường hợp chuyển trang nhập, xác nhận được phân biệt bằng tham số mode trong POST**

| Màn hình | Nhập        | Xác nhận         | Hoàn tất                |
|----------|-------------|------------------|-------------------------|
| URL      | `/contact`  | `/contact`       | `/contact/complete`     |
| POST     |             | `mode=confirm`   | `mode=complete`         |

Trường hợp 1 thì không có gì khó, nhưng với trường hợp 2, khi quét động cần có thêm thao tác đặc biệt.

**Lưu ý:** Áp dụng cho các màn hình như liên hệ, đăng ký hội viên, v.v.
{: .notice--info}

#### Trường hợp truyền dữ liệu qua session

Với các chức năng có pattern **Nhập form → Xác nhận → Hoàn tất**, nếu dữ liệu nhập ở màn hình nhập được lưu vào session và khi chuyển từ xác nhận sang hoàn tất không có input (không truyền qua hidden), thì chỉ có thể quét động từ nhập → xác nhận, không thể quét động từ xác nhận → hoàn tất.

**Lưu ý:** Có thể kiểm thử chuyển trang nhiều màn hình bằng addon sequence hoặc ZAP Script, nhưng phần này xin phép không đề cập chi tiết.
{: .notice--info}

Nếu có tuỳ biến hoặc plugin hiển thị lại nội dung nhập ở màn hình hoàn tất, có thể sẽ không kiểm thử đầy đủ, hãy chú ý.

**Lưu ý:** Áp dụng cho màn hình hoàn tất mua hàng.
{: .notice--info}
