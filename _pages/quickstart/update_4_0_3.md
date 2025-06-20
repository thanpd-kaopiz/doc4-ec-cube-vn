---
title: Lưu ý khi cập nhật lên 4.0.3
keywords: cách cập nhật
permalink: update/4_0_3
summary : Mô tả về thay đổi hiển thị thông tin đơn hàng khi cập nhật lên EC-CUBE 4.0.3.
---


## Bối cảnh
- Trong các phiên bản trước 4.0.2 của EC-CUBE, có lỗi trong tính toán liên quan đến đơn hàng, nhưng đã được sửa trong 4.0.3.
- Do sửa lỗi này, sau khi cập nhật, cần sửa thông tin đơn hàng.

## Nội dung ảnh hưởng

### Về hiển thị tổng khi giảm giá

- Do giảm giá như sử dụng điểm là giảm giá không chịu thuế, nên đúng ra phải được trừ từ tổng số tiền, vì vậy vị trí hiển thị đã được sửa.
- Thay vì hiển thị giảm giá trong tổng số tiền như trước 4.0.2, đã sửa để hiển thị dưới tổng số tiền và tổng số tiền thanh toán.
- Ngoài ra, để hỗ trợ thuế suất giảm, đã thay đổi để hiển thị tổng số tiền theo từng thuế suất dưới tổng số tiền. Về thuế suất, xem chi tiết [tại đây](/spec_tax).

|Hiển thị tổng trên màn hình trước 4.0.2|Hiển thị tổng trên màn hình từ 4.0.3 trở đi|
|---|---|
|![Hiển thị tổng trước 4.0.2](/doc4-ec-cube-vn/images/price_notation_4_0_2.png)|![Hiển thị tổng từ 4.0.3 trở đi](/doc4-ec-cube-vn/images/price_notation_4_0_3.png)|

|Hiển thị tổng trên màn hình quản lý/chi tiết đơn hàng trước 4.0.2|Hiển thị tổng trên màn hình quản lý/chi tiết đơn hàng từ 4.0.3 trở đi|
|---|---|
|![Hiển thị tổng trên màn hình quản lý/chi tiết đơn hàng trước 4.0.2](/doc4-ec-cube-vn/images/admin_price_notation_4_0_2.png)|![Hiển thị tổng trên màn hình quản lý/chi tiết đơn hàng từ 4.0.3 trở đi](/doc4-ec-cube-vn/images/admin_price_notation_4_0_3.png)|

### Về giảm giá bằng plugin coupon

- Trong plugin coupon trước phiên bản 4.0.4, khi sử dụng coupon, có lỗi hiển thị giảm giá là "chịu thuế" với "0%".
- Nếu bạn đang sử dụng plugin coupon trước 4.0.4, hãy cập nhật từ "Màn hình quản lý/Plugin" của EC-CUBE.
- Đối với thông tin đơn hàng sử dụng plugin coupon trước 4.0.4, cần sửa dữ liệu sau khi cập nhật lên EC-CUBE 4.0.3.

|Hiển thị chi tiết đơn hàng với plugin coupon trước 4.0.4 trên màn hình quản lý|
|---|
|![Hiển thị chi tiết đơn hàng với plugin coupon trước 4.0.4 trên màn hình quản lý](/doc4-ec-cube-vn/images/coupon_order_detail.png)|


## Cách sửa chi tiết đơn hàng đã đăng ký với plugin coupon (trước 4.0.4)

- Để sửa chi tiết đã đăng ký với plugin coupon (trước 4.0.4) mà vẫn giữ là chịu thuế, có thể sửa bằng cách thiết lập "thuế suất" cho chi tiết.
- Trong EC-CUBE 4.0.3, khi thêm chi tiết từ nút "Thêm chi tiết khác" trong chi tiết đơn hàng, có thể đăng ký giảm giá chịu thuế và không chịu thuế.
- Để sửa thành giảm giá không chịu thuế, hãy xóa chi tiết đã đăng ký bằng coupon, sau đó thêm chi tiết mới từ "Thêm chi tiết khác".

|Thêm chi tiết khác trong chi tiết đơn hàng trên màn hình quản lý|
|---|
|![Thêm chi tiết khác trong chi tiết đơn hàng trên màn hình quản lý](/doc4-ec-cube-vn/images/coupon_order_detail_item.png)|
