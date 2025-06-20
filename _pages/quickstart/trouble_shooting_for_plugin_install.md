---
title: Giải pháp cho vấn đề không thể cài đặt plugin trên phiên bản 4.2
keywords: điểm yếu
tags: [quickstart, plugin]
permalink: quickstart/trouble-shooting-for-plugin-install
folder: security-guideline
---

## Hiện tượng
Không thể cài đặt plugin trên một số máy chủ cho thuê với EC-CUBE4.2.0.

## Đối tượng

### Phiên bản chính
EC-CUBE 4.2

### Plugin đối tượng
Tất cả

## Nguyên nhân

Hiện tượng xảy ra khi không có thư viện mở rộng PHP-sodium, được thêm vào mặc định từ PHP7.2 trở đi. Đây là hiện tượng xảy ra trên một số máy chủ cho thuê cụ thể. (Yêu cầu hệ thống của EC-CUBE4.2 là PHP7.4 trở lên.)

## Giải pháp gốc
Cài đặt thư viện mở rộng PHP-sodium.

→Nếu gặp khó khăn với giải pháp này, hãy thử **phương pháp tránh** dưới đây.

## Phương pháp tránh
Gỡ cài đặt plugin WebAPI

→Bằng cách gỡ cài đặt plugin WebAPI, có thể cài đặt plugin.

## Đặc điểm của EC-CUBE 4.2.1 trở lên

Từ EC-CUBE 4.2.1, nếu không có mở rộng sodium, plugin WebAPI sẽ được gỡ cài đặt trong trình cài đặt Web.

Xem chi tiết tại các liên kết dưới đây.

- [EC-CUBE#5912](https://github.com/EC-CUBE/ec-cube/issues/5912#issuecomment-1420335054)
- [EC-CUBE#5934](https://github.com/EC-CUBE/ec-cube/pull/5934)