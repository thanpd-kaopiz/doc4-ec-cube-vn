---
title: Cấu trúc kiểm thử xâm nhập ứng dụng web
permalink: /penetration-testing/introduction/layout
---
Sử dụng docker-compose để kết nối EC-CUBE và OWASP ZAP bản Docker.
Với OWASP ZAP bản Docker, bạn có thể truy cập giao diện quản lý của OWASP ZAP thông qua Webswing.

![Webswing](/images/penetration-testing/introduction_layout_webswing.png)

Ưu điểm là không phụ thuộc vào môi trường, có thể chuẩn bị cấu hình cơ bản bằng docker-compose, giúp bất kỳ ai cũng dễ dàng xây dựng môi trường giống nhau.

Nếu lưu lại session, bạn có thể mở lại session đã lưu bằng OWASP ZAP bản Windows, Mac hoặc Standalone để xác nhận kết quả quét.

## Cấu trúc docker-compose

![Cấu trúc docker-compose](https://www.plantuml.com/plantuml/proxy?fmt=svg&src=https://raw.githubusercontent.com/EC-CUBE/doc4.ec-cube.net/master/uml/introduction_layout.puml)

### Ưu điểm

- Có thể hoàn thành trong môi trường cục bộ, an toàn vì không gây ảnh hưởng ra bên ngoài
  - Ở chế độ quét động, sẽ thực hiện tấn công thực tế vào mục tiêu. Ở chế độ bảo vệ, không có tấn công ra bên ngoài
  - Tuy nhiên, khi sử dụng chế độ tiêu chuẩn hoặc tấn công, cần chú ý vì có thể gửi request ra dịch vụ bên ngoài
- Có thể tái hiện lỗ hổng và kiểm thử mà không lo rò rỉ ra ngoài
- Chỉ cần lệnh docker-compose là hoàn tất cấu hình ban đầu, dễ dàng xây dựng
- Ai cũng có thể xây dựng môi trường giống nhau

### Nhược điểm

- Không thể kiểm thử các thiết lập liên quan đến môi trường vận hành thực tế của server web
- Trong quá trình hoạt động, session có thể tiêu tốn hàng chục GB dung lượng đĩa, nên sẽ khó khăn với môi trường cục bộ ít tài nguyên
- Tốc độ chậm hơn so với OWASP ZAP bản Standalone

