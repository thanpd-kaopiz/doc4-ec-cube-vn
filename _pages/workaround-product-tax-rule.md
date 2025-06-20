---
title: Về lỗi không áp dụng được thuế suất riêng cho từng sản phẩm
tags: [spec, getting_started]
permalink: workaround-product-tax-rule
summary: Nguyên nhân và cách khắc phục lỗi không áp dụng được thuế suất riêng cho từng sản phẩm trong một số điều kiện nhất định.
---

## Về lỗi không áp dụng được thuế suất riêng cho từng sản phẩm

Khi tăng thuế, thêm thiết lập thuế suất cơ bản 10% hoặc áp dụng thuế suất giảm nhẹ, nếu thực hiện thiết lập thuế suất riêng cho từng sản phẩm theo một trình tự thời gian nhất định, có thể xảy ra lỗi không áp dụng được thuế suất riêng khi mua hàng.

Vui lòng kiểm tra lại các trường hợp trong mục "Trường hợp bị ảnh hưởng" bên dưới để xác định xem bạn có gặp phải lỗi này không, và nếu có, hãy áp dụng các bước trong mục "Cách khắc phục lỗi".

## Nội dung và đối sách của lỗi

### Nội dung lỗi

Nếu bạn sử dụng EC-CUBE phiên bản 3 hoặc 4, khi thiết lập "Thời điểm áp dụng" cho thuế suất cơ bản, nếu thực hiện thiết lập thuế suất riêng cho từng sản phẩm trước thời điểm này, khi mua hàng sẽ áp dụng thuế suất cơ bản thay vì thuế suất riêng.

### Trường hợp bị ảnh hưởng

Lỗi này xảy ra khi đồng thời thoả mãn tất cả các điều kiện sau:

- Sử dụng EC-CUBE phiên bản 3 hoặc 4
- Đã thêm thiết lập thuế suất cơ bản
- Đã thực hiện thiết lập thuế suất riêng cho từng sản phẩm trước "Thời điểm áp dụng" của thuế suất cơ bản vừa thêm

Ví dụ, nếu thiết lập "Thời điểm áp dụng" thuế suất cơ bản 10% là `2019-10-01 00:00:00`, nhưng thực hiện thiết lập thuế suất riêng cho từng sản phẩm trước thời điểm này, lỗi sẽ xảy ra như hình dưới.

![](./images/tax_setting_time_series.png)

### Cách khắc phục lỗi

Khi mua hàng, hệ thống sẽ lấy thuế suất áp dụng cho sản phẩm dựa trên trường "apply_date (thời điểm áp dụng)" trong bảng "dtb_tax_rule".

Thuế suất có "apply_date" mới nhất và không vượt quá thời điểm hiện tại sẽ được ưu tiên.
Thuế suất riêng cho từng sản phẩm sẽ được đăng ký với "apply_date" là thời điểm thực hiện thiết lập.
Nếu "apply_date" của thuế suất riêng mới hơn "apply_date" của thuế suất cơ bản, lỗi sẽ được khắc phục.

Xem chi tiết về lỗi tại [đây](https://github.com/EC-CUBE/ec-cube/issues/4330){:target="_blank"}.

## Cách khắc phục lỗi

※ Nếu bạn đang sử dụng phiên bản không phải mới nhất, vui lòng nâng cấp lên phiên bản mới nhất trước.

### Cách khắc phục bằng thao tác trên giao diện quản trị

#### Cách thiết lập thời điểm áp dụng thuế suất cơ bản trước khi thiết lập thuế suất riêng cho từng sản phẩm

![](./images/workaround-product-tax-rule_1.png)

1. Mở màn hình quản trị "Cài đặt cửa hàng/Thiết lập thuế suất", nhấn nút "Chỉnh sửa" ở thuế suất cơ bản đã đăng ký.
1. Đổi "Thời điểm áp dụng" thành giá trị trước thời điểm thực hiện thiết lập thuế suất riêng cho từng sản phẩm.
1. Nhấn nút "Lưu" để lưu thiết lập.

#### Cách thiết lập thuế suất riêng cho từng sản phẩm sau thời điểm áp dụng thuế suất cơ bản

Nếu "Thời điểm áp dụng" của thuế suất cơ bản là `2019-10-01 00:00:00`, hãy thực hiện thiết lập thuế suất riêng cho từng sản phẩm sau thời điểm này theo các bước sau để tránh lỗi.

Khi đó, "apply_date" của thuế suất riêng sẽ mới hơn "apply_date" của thuế suất cơ bản, nên thuế suất riêng sẽ được ưu tiên áp dụng.

![](./images/workaround-product-tax-rule_2.png)

1. Nếu đã thiết lập thuế suất riêng cho từng sản phẩm, cần xoá thiết lập đó trước. Trên màn hình chỉnh sửa sản phẩm, xoá giá trị ở trường thuế suất.
1. Nhấn nút "Đăng ký" (lần 1) để lưu thiết lập.

![](./images/workaround-product-tax-rule_3.png)

3. Sau khi lưu, nhập lại giá trị thuế suất riêng cho từng sản phẩm.
1. Nhấn nút "Đăng ký" (lần 2) để lưu thiết lập.

**※ Trên EC-CUBE4.0.3, nếu có nhiều sản phẩm cần thiết lập thuế suất riêng, bạn cũng có thể thực hiện khởi tạo và đăng ký lại thuế suất riêng bằng chức năng "Đăng ký CSV sản phẩm". Tuy nhiên, mặc định trường thuế suất trong CSV sản phẩm bị ẩn, nên cần vào "Cài đặt cửa hàng/Cài đặt trường xuất CSV", chọn loại CSV là `CSV sản phẩm` và thêm trường `Thuế suất` vào mục "Trường xuất".**

### Cách khắc phục cho kỹ thuật viên

#### Cập nhật dữ liệu bằng SQL

Ví dụ dưới đây giả định "Thời điểm áp dụng" của thuế suất cơ bản là `2019-10-01 00:00:00`.
Khi cập nhật bằng SQL, hãy kiểm tra kỹ giá trị và điều kiện trước khi thực hiện.

Nếu dùng MySQL, hãy thiết lập `time_zone` phù hợp với môi trường trước khi cập nhật.

Ví dụ: Đổi time_zone sang JST trên MySQL

```SET time_zone = '+09:00';```

###### ・Cập nhật theo ID tuỳ ý

```UPDATE dtb_tax_rule SET apply_date = '2019-10-01 00:00:01' WHERE id = [id tuỳ ý];```

###### ・Cập nhật các bản ghi có "product_class_id" khác NULL

```UPDATE dtb_tax_rule SET apply_date = '2019-10-01 00:00:01' WHERE product_class_id IS NOT NULL;```

**※ Theo mặc định của EC-CUBE, các bản ghi thuế suất riêng cho từng sản phẩm sẽ có "product_class_id" là ID của phân loại sản phẩm.**

### Cách khắc phục cho EC-CUBE 3.0.x

Lỗi này cũng xảy ra trên EC-CUBE 3.x.
Ngoài các cách khắc phục trên, <u>cần sửa mã nguồn</u> (nếu không sửa mã nguồn thì thuế suất riêng sẽ không được áp dụng).

File cần sửa:  
src/Eccube/Repository/TaxRuleRepository.php
Diff code:  
[https://github.com/EC-CUBE/ec-cube/pull/4310/files#diff-9ebf9d0c89cef624ee2648733e557603](https://github.com/EC-CUBE/ec-cube/pull/4310/files#diff-9ebf9d0c89cef624ee2648733e557603)
Sau khi sửa, hãy xác nhận lại rằng thuế suất riêng đã được áp dụng đúng khi mua hàng.
