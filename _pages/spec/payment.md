---
title: Thiết lập phương thức thanh toán
keywords: payment
tags: [spec, getting_started]
permalink: spec_payment
summary: Trong EC-CUBE, bạn có thể thiết lập phí và điều kiện sử dụng cho từng phương thức thanh toán.

---

Tại `Cài đặt -> Cài đặt cửa hàng -> Thiết lập phương thức thanh toán`, bạn có thể thiết lập phí và điều kiện sử dụng cho từng phương thức thanh toán.
Số tiền điều kiện sử dụng được xác định đã bao gồm phí thanh toán, nên cần thiết lập điều kiện bao gồm cả phí.

## Ví dụ thiết lập tăng phí theo từng mức tiền

![Ví dụ tăng phí theo từng mức tiền](./images/spec/payment-01.png)

Ví dụ:
Khi mua sản phẩm giá 10,000 yên, phí 330 yên ở mức 1 sẽ được áp dụng, tổng số tiền thanh toán là 10,330 yên.
Khi mua sản phẩm giá 10,001 yên, phí 440 yên ở mức 2 sẽ được áp dụng, tổng số tiền thanh toán là 10,441 yên.

## Ví dụ thiết lập giảm phí khi vượt quá một mức tiền nhất định

![Ví dụ giảm phí khi vượt quá một mức tiền nhất định](./images/spec/payment-02.png)

Ví dụ:
Khi mua sản phẩm giá 10,000 yên, phí 330 yên ở mức 1 sẽ được áp dụng, tổng số tiền thanh toán là 10,330 yên.
Khi mua sản phẩm giá 10,001 yên, phí 0 yên ở mức 2 sẽ được áp dụng, tổng số tiền thanh toán là 10,001 yên.
