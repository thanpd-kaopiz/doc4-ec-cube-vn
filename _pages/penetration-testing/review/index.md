---
title: Đánh giá kiểm thử
permalink: /penetration-testing/review
---
## Xuất báo cáo

Từ menu báo cáo, có thể xuất nhiều loại báo cáo khác nhau.
Cơ bản sẽ xuất dưới dạng HTML.

Bạn cũng có thể nhập vào các công cụ quản lý lỗ hổng như [Faraday](https://faradaysec.com){:target="_blank"} để xác nhận.

## Phương pháp đánh giá lỗ hổng bảo mật

Khi phát hiện lỗ hổng bảo mật, quan trọng hơn việc chỉ đánh giá mức độ nguy hiểm là đánh giá mức độ ảnh hưởng đến hoạt động kinh doanh.

Về phương pháp đánh giá cụ thể, chủ yếu sử dụng **[Hệ thống đánh giá lỗ hổng chung CVSS](https://www.ipa.go.jp/security/vuln/CVSS.html){:target="_blank"}**.

**Lưu ý:** Có thể sử dụng [Công cụ tính điểm CVSS](https://www.first.org/cvss/calculator/3.0){:target="_blank"} đã được công khai.<br />
[https://www.first.org/cvss/calculator/3.0](https://www.first.org/cvss/calculator/3.0){:target="_blank"}
{: .notice--info}

Chi tiết, vui lòng tham khảo trang [Hệ thống đánh giá lỗ hổng chung CVSS](https://www.ipa.go.jp/security/vuln/CVSS.html){:target="_blank"} của IPA.

## Phân biệt cảnh báo sai (false positive)

Ngay cả khi phát hiện alert, không phải lúc nào cũng là lỗ hổng bảo mật thực sự, có thể là cảnh báo sai.

Nguyên nhân cảnh báo sai có nhiều, nhưng thường do đặc thù của ứng dụng.

- Thử gửi lại request ghi trong báo cáo để xác nhận có tái hiện được không
- Nếu tái hiện, xác nhận xem có thực sự gây nguy hiểm không

Đây là các điểm cần lưu ý.

Đặc biệt, nếu phát hiện alert **High**, cần xác nhận cẩn thận.
Nếu phân vân, nên hỏi ý kiến chuyên gia.

Ví dụ cảnh báo XSS được phát hiện, gửi lại request cũng tái hiện nhưng thực tế không thực thi mã độc (cảnh báo sai):
![XSS positive false](/doc4-ec-cube-vn/images/penetration-testing/review_positive_false.png)
{: .notice}
