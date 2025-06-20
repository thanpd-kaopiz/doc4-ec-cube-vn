---
title: Thiết lập thuế suất
keywords: tax 
tags: [spec, getting_started]
permalink: spec_tax
summary: Trong EC-CUBE, bạn có thể thiết lập thuế suất cơ bản và thuế suất riêng cho từng sản phẩm.

---

**Đã xác nhận có lỗi không áp dụng được thuế suất riêng cho từng sản phẩm trên EC-CUBE4.0.3.
Vui lòng xem chi tiết tại [đây](workaround-product-tax-rule).**

## Thiết lập thuế suất tiêu chuẩn

Tại `Cài đặt -> Cài đặt cửa hàng -> Thiết lập thuế suất`, bạn có thể thiết lập thuế suất tiêu chuẩn.
Thuế suất tiêu chuẩn sẽ được áp dụng chung cho tất cả sản phẩm.
Mặc định ban đầu là **8%**.

![Trạng thái mặc định của thuế suất tiêu chuẩn](./images/img-tax-01.png)

Bạn có thể thêm mới thuế suất tiêu chuẩn.
Có thể thiết lập thời điểm áp dụng và mức thuế suất.

![Thêm thuế suất tiêu chuẩn](./images/img-tax-02.png)

Khi thêm thuế suất tiêu chuẩn, sau thời điểm áp dụng hệ thống sẽ tự động chuyển sang thuế suất mới.
Thông tin đơn hàng trước thời điểm áp dụng sẽ giữ nguyên thuế suất/tổng thuế tại thời điểm đặt hàng, không bị thay đổi ngược lại.

## Thiết lập thuế suất riêng cho từng sản phẩm

**Đã xác nhận có lỗi không áp dụng được thuế suất riêng cho từng sản phẩm trên EC-CUBE4.0.3.
Vui lòng xem chi tiết tại [đây](workaround-product-tax-rule).**

Khi bật chức năng thuế suất riêng cho từng sản phẩm tại `Cài đặt -> Cài đặt cửa hàng -> Cài đặt cơ bản`, bạn có thể đăng ký thuế suất theo từng sản phẩm (chính xác là từng phân loại sản phẩm).

![Bật chức năng thuế suất riêng cho từng sản phẩm](./images/img-tax-03.png)

Ví dụ đăng ký sản phẩm không có phân loại
![Ví dụ đăng ký sản phẩm không có phân loại](./images/img-tax-04.png)

Ví dụ đăng ký sản phẩm có phân loại
![Ví dụ đăng ký sản phẩm có phân loại](./images/img-tax-05.png)

Khi chức năng thuế suất riêng cho từng sản phẩm được bật, sản phẩm có thiết lập thuế suất sẽ tính theo thuế suất đó, sản phẩm chưa thiết lập sẽ tính theo thuế suất tiêu chuẩn.

## Lưu ý khi áp dụng thuế suất giảm nhẹ

Từ tháng 10/2019, thuế tiêu thụ tăng lên 10% và bắt đầu áp dụng chế độ thuế suất giảm nhẹ.
Khi áp dụng chế độ này, các mặt hàng như "thực phẩm, đồ uống" sẽ áp dụng thuế suất khác với các mặt hàng thông thường.

Thông tin về chế độ thuế suất giảm nhẹ:
[https://www.nta.go.jp/taxes/shiraberu/zeimokubetsu/shohi/keigenzeiritsu/index.htm](https://www.nta.go.jp/taxes/shiraberu/zeimokubetsu/shohi/keigenzeiritsu/index.htm){:target="_blank"}

### Khuyến nghị thiết lập thuế suất tiêu chuẩn và thuế suất giảm nhẹ

Nên thiết lập thuế suất tiêu chuẩn tại `Cài đặt -> Cài đặt cửa hàng -> Thiết lập thuế suất` và thiết lập thuế suất giảm nhẹ bằng chức năng thuế suất riêng cho từng sản phẩm.
Ngay cả khi chỉ bán thực phẩm, phí xử lý và phí vận chuyển vẫn tính theo thuế suất tiêu chuẩn, nên khuyến nghị thiết lập như trên.

### Về giảm giá có thuế và không thuế

Có hai loại giảm giá: giảm giá có thuế và giảm giá không thuế.

Giảm giá có thuế dùng khi giảm giá trực tiếp trên sản phẩm. Số tiền giảm giá đã bao gồm thuế sẽ thay đổi theo thuế suất của sản phẩm, nên cần thiết lập thuế suất cho giảm giá.

![Giảm giá có thuế](./images/img-tax-06.png)

Giảm giá không thuế được coi như phiếu quà tặng, dùng để thanh toán một phần đơn hàng. Số tiền giảm giá này không tính vào thuế tiêu thụ.
Chức năng điểm thưởng mặc định của EC-CUBE và plugin coupon chính thức đều xử lý giảm giá không thuế.

![Giảm giá không thuế](./images/img-tax-07.png)

### Trường hợp vận hành theo giá đã bao gồm thuế

Nếu vận hành theo giá đã bao gồm thuế (thiết lập thuế suất 0% tại `Cài đặt -> Cài đặt cửa hàng -> Thiết lập thuế suất`), hệ thống sẽ hiển thị "Đối tượng thuế suất 0%: xxx yên". Nếu không cần hiển thị, bạn cần chỉnh sửa template.

# Vấn đề liên quan

Một số issue liên quan đến chức năng thuế suất đã được đăng ký. Vui lòng kiểm tra thêm:

- [https://github.com/EC-CUBE/ec-cube/issues/4183](https://github.com/EC-CUBE/ec-cube/issues/4183){:target="_blank"}
