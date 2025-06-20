---
title: Liên quan đến đơn hàng
keywords: spec-order
tags: [spec, getting_started]
permalink: spec_order
summary: Giải thích về các chức năng liên quan đến đơn hàng.

---

## Quy trình xử lý trạng thái đơn hàng

![Sơ đồ trạng thái đơn hàng](./images/spec/order-statemachine.png)

[Tham khảo: Triển khai State Machine cho đơn hàng #3325](https://github.com/EC-CUBE/ec-cube/pull/3325)

### So sánh với phiên bản 3

| ID | 3.x<br> mtb_order_status<br>(Hiển thị phía quản trị) | 3.x<br> mtb_customer_order_status<br>(Hiển thị phía khách) | 4.x<br> mtb_order_status<br>(Hiển thị phía quản trị) | 4.x<br>mtb_customer_order_status<br>(Hiển thị phía khách) |
|----|----------------------------------------------|-------------------------------------------------------|----------------------------------------------|------------------------------------------------------|
|  1 | Tiếp nhận mới                                 | Đã nhận đơn hàng                                     | Tiếp nhận mới                                 | Đã nhận đơn hàng                                    |
|  2 | Chờ thanh toán                               | Chờ thanh toán                                       | (Bỏ qua)                                     | (Bỏ qua)                                            |
|  3 | Huỷ đơn                                      | Huỷ đơn                                              | Huỷ đơn hàng                                 | Huỷ đơn hàng                                        |
|  4 | Đang đặt hàng                                | Đã nhận đơn hàng                                     | Đang xử lý                                    | Đã nhận đơn hàng                                   |
|  5 | Đã giao hàng                                 | Đã giao hàng                                         | Đã giao hàng                                 | Đã giao hàng                                        |
|  6 | Đã thanh toán                                | Đã nhận đơn hàng                                     | Đã thanh toán                                | Đã nhận đơn hàng                                   |
|  7 | Đang xử lý thanh toán                        | Đơn chưa hoàn tất                                    | Đang xử lý thanh toán                        | Đã nhận đơn hàng                                   |
|  8 | Đang xử lý mua hàng                          | Đơn chưa hoàn tất                                    | Đang xử lý mua hàng                          | Đơn chưa hoàn tất                                  |
|  9 | (Không có)                                   | (Không có)                                           | Trả hàng                                     | Trả hàng                                            |

- Để thuận tiện cho việc di chuyển dữ liệu, hạn chế thay đổi ID.
- **4: Đang đặt hàng** được gộp thành **4: Đang xử lý**.
- **2: Chờ thanh toán** bị xoá. Trạng thái này trước đây dùng cho các phương thức thanh toán liên kết chờ xác nhận thanh toán. Trạng thái này sẽ được xử lý bằng **7: Đang xử lý thanh toán**. Đối với chuyển khoản ngân hàng hoặc chờ thanh toán trước khi giao hàng sẽ xử lý ở **1: Tiếp nhận mới**.
- **3: Huỷ đơn** đổi thành **3: Huỷ đơn hàng**. Dùng khi huỷ trước khi giao hàng (do có thêm trạng thái trả hàng nên đổi tên cho dễ hiểu).
- Thêm mới **9: Trả hàng**.

Luồng trạng thái chính:

"Đang xử lý mua hàng" → "Đang xử lý thanh toán" → "Tiếp nhận mới" → "Đã thanh toán" hoặc "Đang xử lý" → "Đã giao hàng" → Nếu có huỷ sau khi giao thì chuyển sang "Trả hàng"

#### Xử lý trạng thái khi huỷ đơn/ trả hàng

##### Huỷ đơn hàng

Nếu huỷ trước khi giao hàng, chọn huỷ đơn sẽ hoàn lại tồn kho và điểm thưởng.

Khi đã chọn "Đã giao hàng" thì không thể chọn "Huỷ đơn hàng" nữa.

##### Trả hàng

Sau khi giao hàng, nếu có trả hàng thì chọn trả hàng. Khi trả hàng sẽ không hoàn lại tồn kho và điểm thưởng.

## Quy tắc tính phí

### Sơ đồ ER các bảng liên quan đến đơn hàng

![Sơ đồ ER các bảng liên quan đến đơn hàng](./images/spec/order-erdiagram.png)

### Những thay đổi chính so với phiên bản 3

- dtb_shipment_item đổi thành dtb_order_item.
- dtb_order_detail bị loại bỏ.
- Quan hệ giữa các bảng đổi thành: dtb_order **1:N** dtb_order_item **N:1** dtb_shipping.
- Ngoài sản phẩm, các mục như phí vận chuyển, phí xử lý, giảm giá... cũng được quản lý như một dòng chi tiết trong dtb_order_item.

### Cách tính toán

Tính tổng số tiền thanh toán dựa trên thuộc tính của từng dòng chi tiết đơn hàng.
Lưu ý cách tính sẽ khác nhau tuỳ thuộc vào thuộc tính, như ví dụ dưới đây.

Dòng sản phẩm được đăng ký với **giá chưa thuế**, nên khi tính tổng sẽ **cộng thêm phần thuế**.

```
Tổng dòng = (Đơn giá sản phẩm x Thuế suất) x Số lượng
```

Dòng phí vận chuyển được đăng ký với **giá đã bao gồm thuế**, nên khi tính tổng **không cộng thêm thuế**.

```
Tổng dòng = Đơn giá vận chuyển x Số lượng
```

[Tham khảo: #3420 Kết quả tính toán theo loại dòng chi tiết](https://github.com/EC-CUBE/ec-cube/pull/3420)

### Thuộc tính dòng chi tiết đơn hàng

#### Phân loại dòng chi tiết

| ID | name           | Ghi chú                                         |
|----|----------------|------------------------------------------------|
|  1 | Sản phẩm       |                                                |
|  2 | Phí vận chuyển |                                                |
|  3 | Phí xử lý      |                                                |
|  4 | Giảm giá       | Chủ yếu dùng cho giảm giá sản phẩm. Có tính thuế. |
|  5 | Thuế           | Dùng khi đánh thuế cho toàn bộ đơn hàng.       |
|  6 | Giảm giá điểm  | Dùng cho giảm giá bằng điểm thưởng. Không tính thuế. |

#### Phân loại thuế

| ID | name   | Ghi chú           |
|----|--------|-------------------|
|  1 | Có thuế |                   |
|  2 | Không thuế | Giảm giá bằng điểm, v.v. |
|  3 | Miễn thuế | Chuyển nhượng phiếu quà tặng, v.v. |

#### Phân loại hiển thị thuế

| ID | name | Ghi chú                               |
|----|------|--------------------------------------|
|  1 | Chưa thuế | Đăng ký với giá chưa thuế (sản phẩm, v.v.) |
|  2 | Đã bao gồm thuế | Đăng ký với giá đã bao gồm thuế (phí vận chuyển, v.v.) |

### Tính điểm thưởng

#### Tính toán khi sử dụng điểm thưởng

```
Số tiền giảm giá bằng điểm = Số điểm sử dụng * Tỷ lệ quy đổi điểm
```

Làm tròn xuống phần lẻ. Phân loại thuế là không thuế.

#### Tính toán khi cộng điểm thưởng

Điểm thưởng được tính trên dòng sản phẩm.

```
Điểm cộng = Đơn giá sản phẩm (chưa thuế) * Tỷ lệ cộng điểm * Số lượng
```

Nếu có sử dụng điểm thưởng, số điểm giảm giá sẽ bị trừ đi.

```
Điểm trừ = Số tiền giảm giá bằng điểm * Tỷ lệ cộng điểm * Số lượng
```

Tổng điểm cộng và điểm trừ là tổng điểm cuối cùng được cộng cho đơn hàng đó.

### Tính điều kiện miễn phí vận chuyển

Khi thiết lập điều kiện miễn phí vận chuyển, hệ thống sẽ tính tổng giá trị sản phẩm (đã bao gồm thuế) cho từng địa chỉ nhận hàng để xác định điều kiện miễn phí vận chuyển.

Ví dụ: Điều kiện miễn phí vận chuyển: 3,000 yên

| Địa chỉ nhận hàng | Tổng giá trị sản phẩm | Được miễn phí vận chuyển |
|-------------------|----------------------|-------------------------|
| Địa chỉ A         | 2,900                | ×                       |
| Địa chỉ B         | 3,200                | ○                       |

### Thiết lập thuế tiêu thụ

### Về thiết lập thuế suất theo sản phẩm

Có thể thiết lập các tuỳ chọn sau:

- Thiết lập thuế suất trên màn hình đăng ký sản phẩm (sản phẩm không có phân loại)
- Thiết lập thuế suất trên màn hình đăng ký phân loại sản phẩm (sản phẩm có phân loại)
- Nếu để trống sẽ xoá thuế suất trong dtb_tax_rule

Một số lưu ý:

- Không lưu lịch sử như thuế suất chung.
- Khi đăng ký/chỉnh sửa sản phẩm, thuế suất riêng luôn được cập nhật.
- Khi chỉnh sửa đơn hàng:
   - Dòng chi tiết có thuế suất riêng luôn được cập nhật với giá trị mới nhất.
   - Nếu thuế suất trên sản phẩm bị xoá, sẽ áp dụng thuế suất cơ bản.

### Về loại hình bán hàng

Có thể thiết lập loại hình bán hàng để phân tách phương thức thanh toán theo từng loại hình.

Nếu thêm các sản phẩm thuộc loại hình bán hàng khác nhau vào giỏ cùng lúc, giỏ sẽ được tách riêng theo từng loại hình. Người dùng sẽ tiến hành đặt hàng cho từng giỏ riêng biệt.

