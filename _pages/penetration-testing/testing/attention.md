---
title: Các lưu ý khi thực hiện kiểm thử
permalink: /penetration-testing/testing/attention
---
**Chú ý!!**
Công cụ này thực sự tấn công vào website để kiểm tra xem có lỗ hổng bảo mật hay không.
Chỉ sử dụng trên môi trường Docker cục bộ, tuyệt đối không sử dụng trên website đang hoạt động.
Có thể dữ liệu sẽ bị thay đổi hoặc xóa ngoài ý muốn.<br />
**Bạn tự chịu trách nhiệm khi kiểm thử, Công ty EC-CUBE và cộng đồng phát triển liên quan sẽ không chịu bất kỳ trách nhiệm nào, xin hãy lưu ý trước khi thực hiện.**
{: .notice--danger}

Khi thực hiện kiểm thử với OWASP ZAP, có một số điểm cần lưu ý.
Nếu không nắm rõ các điểm này, quét động của OWASP ZAP sẽ không đầy đủ và có thể không phát hiện được lỗ hổng.

## Sử dụng chế độ Protect Mode

Sau khi khởi động OWASP ZAP, hãy chuyển sang **Protect Mode**.
Chế độ này sẽ giới hạn kiểm tra lỗ hổng trong các URL được phép trong context.

![Sử dụng Protect Mode](/doc4-ec-cube-vn/images/penetration-testing/quick_start_protect_mode.png)

**Chú ý!** Nếu dùng chế độ Standard hoặc Attack, có thể vô tình tấn công ra ngoài website.
{: .notice--danger}

## Chức năng tự động sinh token Anti-CSRF

Chức năng tự động sinh token Anti-CSRF có thể không hoạt động tốt.
Ngay cả trên OWASP ZAP cũng chỉ là chức năng beta.
Lỗi liên quan đến không khớp token CSRF có thể tránh được bằng cách sử dụng cùng một session khi thăm dò thủ công qua Local Proxes và khi quét động.

## Thăm dò thủ công và quét động phải dùng cùng một session

Khi thăm dò thủ công qua Local Proxes và khi quét động, cần sử dụng cùng một session.
Khi thực hiện quét động, hãy đảm bảo token CSRF hợp lệ và xác nhận chắc chắn tấn công đã được thực hiện.

## Sử dụng Spider

Nếu sử dụng Spider, session sẽ không được giữ lại khi quét động, token CSRF sẽ thay đổi và kiểm thử sẽ thất bại.
Spider chỉ nên dùng để kiểm thử các request GET.

## Form POST

Do vấn đề về session và token CSRF, nên thăm dò thủ công tất cả các form submit bằng POST để đảm bảo.

## Pattern chuyển trang đặc biệt

Với các URL điều khiển chuyển trang bằng tham số POST như mode=confirm, mode=complete, không thể quét động toàn bộ từ tầng trên.
Cần quét động từng tham số riêng biệt từ lịch sử, v.v.

## Về addon sequence

Addon sequence cho phép kiểm thử chuyển trang nhiều màn hình.
Tuy nhiên, có vẻ chưa hỗ trợ tốt nhập tiếng Nhật. Chỉ nên dùng cho các chức năng không liên quan đến nhập tiếng Nhật và URL không thay đổi.

## Quét động màn hình quản trị

Màn hình quản trị có thể quét động liên tục vì token CSRF không thay đổi trừ khi logout.
Tuy nhiên, nếu quét động kéo dài, khả năng thất bại sẽ tăng lên.
Nên lặp lại thăm dò thủ công và quét động theo từng chức năng để đảm bảo.

## Addon beta, alpha

Nếu cài thêm các addon kiểm tra XSS, SQL Injection beta/alpha, số lượng kiểm tra sẽ tăng rất nhiều.
Kết quả là quét động kéo dài, session có thể bị thay đổi và kiểm thử thất bại.

## Không nên quá tin vào kết quả kiểm thử

OWASP ZAP cũng có giới hạn, vẫn có thể có lỗ hổng không phát hiện được.
Không nên chỉ tin vào một lần kiểm thử, hãy kiểm tra thường xuyên và liên tục.

