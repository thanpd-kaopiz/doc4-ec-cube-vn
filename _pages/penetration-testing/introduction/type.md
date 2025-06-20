---
title: Các loại kiểm thử bảo mật
permalink: /penetration-testing/introduction/type
---
Kiểm thử bảo mật có nhiều loại khác nhau.
Trong mục này, chúng tôi sẽ giải thích sơ lược về các loại kiểm thử bảo mật chính.

**Lưu ý:** Vui lòng tham khảo thêm [OWASP Testing guide - Testing Techniques Explained](https://owasp.org/www-project-web-security-testing-guide/v41/2-Introduction/README.html#testing-techniques-explained)
{: .notice--info}

## Kiểm tra thủ công và review

Kiểm tra thủ công là quá trình kiểm tra bảo mật do con người thực hiện, không sử dụng công cụ tự động.
Có những trường hợp kiểm tra cả quy định nội bộ, quy trình, thiết kế kiến trúc hệ thống, v.v.

Chủ yếu thực hiện bằng cách phân tích tài liệu, phỏng vấn nhà thiết kế hoặc quản trị viên hệ thống.

## Mô hình hóa mối đe dọa (Threat Modeling)

Đây là phương pháp phân tích sơ đồ cấu trúc hệ thống, sơ đồ luồng dữ liệu để xác định các mối đe dọa.
Thông thường thực hiện theo các bước sau:

1. Nắm bắt tổng thể hệ thống
1. Lần theo luồng dữ liệu
1. Liệt kê các mối đe dọa
1. Lặp lại các bước trên cho từng hoạt động

Các bước này thường được thực hiện ở giai đoạn đầu thiết kế. Cụ thể, sẽ thực hiện khi đã xác định được phương pháp nhập/xuất dữ liệu, phương pháp lưu trữ lâu dài, v.v.

## Review mã nguồn

Đây là quá trình kiểm tra mã nguồn để phát hiện các vấn đề bảo mật bằng cách quan sát trực tiếp.

Đặc biệt, với các phần mềm mã nguồn mở như EC-CUBE, nhiều lỗ hổng đã được cải thiện thông qua review mã nguồn.

Việc thực hiện review mã nguồn giúp xây dựng hệ thống vững chắc hơn so với chỉ kiểm thử bằng hộp đen.

## Kiểm thử xâm nhập

Kiểm thử xâm nhập (Penetration Test) là quá trình sử dụng các công cụ như OWASP ZAP để thực hiện tấn công thực tế, xác nhận xem có tồn tại lỗ hổng bảo mật hay không.

Đây là phương pháp kiểm thử được đề cập trong tài liệu này.
