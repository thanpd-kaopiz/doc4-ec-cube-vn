---
title: Về kiểm thử xâm nhập ứng dụng web
permalink: /penetration-testing/introduction/penetration-test
---
Kiểm thử xâm nhập ứng dụng web (Penetration Test) là quá trình thực hiện tấn công thực tế vào hệ thống kết nối Internet để xác nhận xem có tồn tại lỗ hổng bảo mật hay không.

Do thực hiện tấn công thực tế để xác nhận khả năng tái hiện, có thể xảy ra trường hợp dữ liệu bị thay đổi hoặc xóa ngoài ý muốn.
Khi thực hiện kiểm thử, **nhất định phải chuẩn bị môi trường kiểm thử riêng biệt với môi trường thật và chỉ thực hiện trên môi trường kiểm thử**

Ngoài ra, việc kiểm thử có thể gây tải lớn lên hệ thống, một số dịch vụ hosting có thể giới hạn kiểm thử, hãy xác nhận kỹ quy định sử dụng dịch vụ hosting trước khi thực hiện kiểm thử.

Tham khảo các dịch vụ cloud tiêu biểu:

- [Amazon Web Service](https://aws.amazon.com/jp/security/penetration-testing/)
- [Microsoft Azure](https://docs.microsoft.com/ja-jp/azure/security/fundamentals/pen-testing)
- [Google Cloud Platform](https://support.google.com/cloud/answer/6262505?hl=ja)

## Ưu điểm

Có thể thiết kế kiểm thử phù hợp với môi trường hệ thống, thực hiện kiểm thử xâm nhập trên môi trường kiểm thử nên **có thể điều tra an toàn và cụ thể**.

Nhiều trường hợp phát hiện lỗ hổng mà khi phát triển không nhận ra, giúp vận hành hệ thống vững chắc hơn.

## Nhược điểm

Khi thực hiện kiểm thử, cần có kiến thức chuyên sâu về hệ thống mục tiêu và bảo mật.

Có một số công cụ kiểm thử tự động như OWASP ZAP, nhưng phạm vi kiểm thử tự động vẫn còn hạn chế, cần kết hợp kiểm thử thủ công.

Do đó, chi phí kiểm thử thường cao và mất nhiều thời gian.
