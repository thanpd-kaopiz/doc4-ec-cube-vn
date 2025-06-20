---
title: Cách thực hiện quét động
permalink: /penetration-testing/testing/active_scan
---
## Cơ bản về quét động

Quy trình cơ bản để thực hiện quét động như sau:

1. Từ lịch sử hoặc danh sách URL trong tab site, chọn URL cần quét
1. Chọn **Tấn công→Quét động** và thực thi

![Thao tác cơ bản quét động](/doc4-ec-cube-vn/images/penetration-testing/testing_active_scan.png)

**Lưu ý:** Hãy đảm bảo token CSRF được thiết lập trong tham số POST trùng khớp với token của Firefox khi truy cập qua Local Proxes.
![Xác nhận sự trùng khớp của token CSRF](/doc4-ec-cube-vn/images/penetration-testing/testing_active_scan_csrftoken.png)
Nếu token CSRF không trùng khớp, quét động sẽ bị lỗi và không thể kiểm thử đầy đủ.
{: .notice--warning}

**Lưu ý:** Các chức năng chỉnh sửa sau của màn hình quản trị có tham số ID trong token CSRF và được thiết lập động.
Cần đăng ký từng lần một trong OWASP ZAP tại Công cụ→Tùy chọn→Anti-CSRF Token.

 - Quản lý quy cách
 - Quản lý phân loại quy cách
 - Quản lý danh mục
 - Quản lý tag
{: .notice--warning}

## URL có thể truy cập bằng GET

Các URL có thể truy cập bằng GET không bị ảnh hưởng bởi token CSRF, do đó có thể chọn thư mục trong danh sách URL của tab site và thực hiện quét động cho toàn bộ các tầng con bên dưới.

![Có thể quét động toàn bộ tầng con](/doc4-ec-cube-vn/images/penetration-testing/testing_active_scan_get.png)

## Kiểm thử các pattern chuyển trang đặc biệt

**Lưu ý:** Phần này đang được viết tiếp
{: .notice}

### Kiểm thử chuyển trang nhiều màn hình

- Nếu bắt buộc nhập tiếng Nhật, nên lặp lại **Thăm dò thủ công→Quét động** từng màn hình một để đảm bảo
- Nếu không liên quan đến nhập tiếng Nhật, có thể sử dụng addon sequence
  - Tuy nhiên, cần kiểm tra kỹ xem đã quét đầy đủ chưa vì có thể không thành công

### Trường hợp nội dung bị xóa

- Áp dụng cho xóa ảnh, xóa khỏi giỏ hàng, v.v.
- Có thể kiểm thử bằng cách comment out logic xóa hoặc rollback DB
- Tuy nhiên, nếu có lỗ hổng SQL Injection trong logic xóa thì sẽ không phát hiện được

### Trường hợp điều khiển chuyển trang bằng tham số POST

Danh sách URL trong tab site sẽ không đăng ký các URL có giá trị tham số POST khác nhau.
(Ví dụ: chuyển trang với `mode=confirm`, `mode=complete`)
Cách làm không chính thống, nhưng có thể sử dụng chức năng gửi thủ công để thêm tham số giả và gửi request, từ đó thực hiện quét động.

*Giả định rằng URL với `mode=confirm` đã được đăng ký*

1. Tìm request tương ứng (`mode=complete`) trong lịch sử
2. Chuột phải → Gửi lại, thêm tham số giả và gửi lại (`mode=complete&mode2=dummy`, chỉnh sửa tham số bằng tay)
3. Lúc này, URL với `mode=complete` cũng sẽ được đăng ký vào danh sách URL của tab site, có thể thực hiện quét động với URL này

**Lưu ý:** Áp dụng cho các màn hình như liên hệ, đăng ký thành viên, v.v.
{: .notice--info}

### Trường hợp truyền dữ liệu qua session

- Nếu chuyển từ màn hình xác nhận sang hoàn tất mà dữ liệu được truyền qua session thì không thể kiểm thử
  - Có thể kiểm thử bằng cách viết ZAP Script

**Lưu ý:** Nếu có tuỳ biến hoặc plugin hiển thị thông tin nhập ở màn hình hoàn tất, cần chú ý có thể tiềm ẩn lỗ hổng
{: .notice--warning}

**Lưu ý:** Áp dụng cho màn hình hoàn tất mua hàng.
{: .notice--info}

### Kiểm thử upload file

Có thể kiểm thử upload file bằng cách **thăm dò thủ công rồi quét động**.
Nên sử dụng file có dung lượng nhỏ để kiểm thử vì upload file lớn sẽ tốn rất nhiều thời gian.

### Kiểm thử các chức năng xóa

Việc kiểm thử xóa đơn hàng, xóa thành viên là khó khăn vì không thể gửi lặp lại request xóa.

Có thể vô hiệu hóa chức năng xóa bằng cách rollback transaction hoặc comment out `EntityManager::flush()`, từ đó kiểm thử được phần nào.

Tuy nhiên, nếu vô hiệu hóa chức năng xóa thì việc kiểm thử SQL Injection sẽ khó khăn hơn, nên cần chú ý kiểm tra kỹ các tham số gửi khi xóa.
