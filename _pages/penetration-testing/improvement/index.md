---
title: Cải thiện bảo mật
permalink: /penetration-testing/improvement
---
## Khi phát hiện lỗ hổng bảo mật trên website

Khi phát hiện lỗ hổng bảo mật trên website, thông tin về lỗ hổng có thể trở thành mối đe dọa đối với cả quản trị viên và người dùng website, do đó cần chú ý khi xử lý thông tin này.
Vui lòng quản lý nghiêm ngặt thông tin lỗ hổng, không để rò rỉ ra ngoài những người liên quan.

Quan trọng nhất là không để người khác bị thiệt hại.
Cho đến khi có biện pháp an toàn, người phát hiện và quản trị viên nên phối hợp và xử lý một cách thiện chí.

**Lưu ý:** [Tài liệu tham khảo về phát hiện và báo cáo lỗ hổng bảo mật](https://www.ipa.go.jp/security/vuln/report/notice/handling_20190926.html){:target="_blank"} sẽ hữu ích cho bạn.
{: .notice--info}

## Cách báo cáo lỗ hổng bảo mật

Vui lòng liên hệ với [Cửa sổ tiếp nhận thông tin liên quan đến lỗ hổng bảo mật của IPA](https://www.ipa.go.jp/security/vuln/report/){:target="_blank"} hoặc Công ty cổ phần EC-CUBE (support@ec-cube.net).

## Phản hồi cho EC-CUBE

Nếu phát hiện lỗ hổng bảo mật trong EC-CUBE, sẽ phối hợp với IPA và JPCERT/CC (tổ chức điều phối thông tin lỗ hổng bảo mật) để xử lý an toàn.

Thông tin lỗ hổng sẽ được quản lý nghiêm ngặt để không gây thiệt hại cho các cửa hàng và người dùng EC-CUBE.

Thông tin lỗ hổng phản hồi cho EC-CUBE sẽ được tổng hợp tại **[Danh sách lỗ hổng bảo mật EC-CUBE](https://www.ec-cube.net/info/weakness/){:target="_blank"}**.

**Lưu ý:** Tất cả các phiên bản mới nhất của EC-CUBE 2, 3, 4 đều đã được áp dụng các biện pháp khắc phục lỗ hổng bảo mật.
Nếu bạn đang sử dụng phiên bản cũ, vui lòng chú ý vì có thể còn tồn tại lỗ hổng chưa được vá.
{: .notice--info}

## Cải thiện phương pháp kiểm thử

Hiện tại, kiểm thử xâm nhập sử dụng OWASP ZAP vẫn còn nhiều thao tác thủ công, đòi hỏi kiến thức chuyên môn về EC-CUBE và bảo mật, cũng như tài nguyên máy tính lớn.

Trong tương lai, dự kiến sẽ tự động hóa bằng Selenium hoặc GitHub Actions.

Nếu bạn có đề xuất cải thiện kiểm thử, hãy gửi về [repository EC-CUBE trên GitHub](https://github.com/EC-CUBE/ec-cube){:target="_blank"}.


