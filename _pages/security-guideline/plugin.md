---
layout: single
title: Tăng cường bảo mật khi phát triển plugin
keywords: plugin plugin bảo mật
tags: [security-guideline, plugin, security]
permalink: security-guideline/plugin
folder: security-guideline
---

## Về tăng cường bảo mật khi phát triển plugin

Tài liệu này giải thích các chức năng giúp tăng cường bảo mật khi phát triển plugin.

Khi phát triển plugin, khuyến nghị tích hợp các chức năng sau để tăng cường bảo mật.

- Throttling cho các thao tác quan trọng

## Throttling cho các thao tác quan trọng

Từ EC-CUBE 4.2.1, chức năng [throttling](https://thanpd-ptit.github.io/doc4-ec-cube-vn/customize_throttling){:target="_blank"} đã được tích hợp vào core EC-CUBE.

Chức năng này cũng có thể mở rộng từ plugin hoặc Customize.

Khi phát triển plugin có thao tác quan trọng, khuyến nghị tích hợp chức năng throttling.

### Cách triển khai

Ví dụ dưới đây minh hoạ cách thêm throttling vào chức năng thay đổi thông tin thẻ trong [plugin thanh toán mẫu](https://github.com/EC-CUBE/sample-payment-plugin){:target="_blank"}.

Thêm cấu hình vào services.yaml của plugin.

app/Plugin/SamplePayment42/Resource/config/services.yaml

```yaml
# Định nghĩa throttling
eccube:
  rate_limiter:
    sample_payment_mypage_card_info:
      # Chỉ định route thực thi
      route: sample_payment_mypage_card_info
      # Chỉ định method thực thi. Mặc định là POST.
      method: ['POST']
      # Kiểu kiểm soát throttling. Có thể là ip hoặc customer.
      type: ['ip', 'customer']
      # Số lần thử tối đa
      limit: 5
      # Khoảng thời gian
      interval: '60 minutes'
```

Như vậy là xong.

Hãy thử truy cập vượt quá số lần cho phép để xác nhận bị từ chối truy cập.

Tham khảo chi tiết tại [chức năng throttling](https://thanpd-ptit.github.io/doc4-ec-cube-vn/customize_throttling){:target="_blank"}.

