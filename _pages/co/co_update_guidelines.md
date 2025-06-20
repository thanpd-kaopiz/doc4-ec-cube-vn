---
title: ec-cube.co Hướng dẫn cập nhật
keywords: co ec-cube.co Cloud version Hướng dẫn cập nhật
tags: [co, ec-cube.co]
permalink: co/co_update_guidelines
folder: co
---

---

## Mã nguồn được áp dụng

Mã nguồn EC-CUBE sử dụng trên ec-cube.co (4.0/4.1/4.2) được công khai tại các branch [co/master](https://github.com/EC-CUBE/ec-cube/tree/co/master){:target="_blank"}, [co/4.1](https://github.com/EC-CUBE/ec-cube/tree/co/4.1){:target="_blank"}, [co/4.2](https://github.com/EC-CUBE/ec-cube/tree/co/4.2){:target="_blank"}.
Branch [4.2](https://github.com/EC-CUBE/ec-cube/tree/4.2){:target="_blank"} sẽ được merge định kỳ vào branch [co/4.2](https://github.com/EC-CUBE/ec-cube/tree/co/4.2){:target="_blank"} trong các đợt bảo trì hàng tuần.

Mã nguồn EC-CUBE đang áp dụng cho ec-cube.co (bản 4.2) có thể kiểm tra tại [co/4.2-YYYYMMDD](https://github.com/EC-CUBE/ec-cube/tags){:target="_blank"}.
Mã nguồn EC-CUBE đang áp dụng cho ec-cube.co (bản 4.1) có thể kiểm tra tại [co/4.1-YYYYMMDD](https://github.com/EC-CUBE/ec-cube/tags){:target="_blank"}.
Mã nguồn EC-CUBE đang áp dụng cho ec-cube.co (bản 4.0) có thể kiểm tra tại [co/YYYYMMDD](https://github.com/EC-CUBE/ec-cube/tags){:target="_blank"}.

## Hướng dẫn cập nhật

Ưu tiên đảm bảo tính tương thích với tiêu chuẩn merge Pull Request của EC-CUBE.

Danh sách kiểm tra tương thích Pull Request:
- Thay đổi specification của chức năng hiện có
- Thay đổi timing gọi function hookpoint
- Xoá/thay đổi kiểu dữ liệu parameter của function hookpoint
- Xoá/thay đổi kiểu dữ liệu parameter truyền vào file twig
- Xoá/thay đổi kiểu dữ liệu parameter của function public trong Service class
- Thay đổi format file xuất/nhập (CSV, ...)

## Thời điểm phản ánh

Cập nhật sẽ được thực hiện theo lịch bảo trì hàng tuần.
- Bảo trì hàng tuần (mỗi thứ 5 từ 9:00~10:00, không dừng dịch vụ): cập nhật EC-CUBE
- Bảo trì hàng tháng (mỗi thứ 5 đầu tháng từ 9:00~10:00, có thể dừng dịch vụ): cập nhật GKE node, hạ tầng, middleware
