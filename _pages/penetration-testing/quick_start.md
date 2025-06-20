---
title: Bắt đầu nhanh
permalink: /penetration-testing/quick_start
---

**Chú ý!** Để tránh tấn công ngoài ý muốn đến các site bên ngoài, hãy luôn sử dụng OWASP ZAP ở **chế độ bảo vệ (Protect Mode)**
![Sử dụng chế độ Protect Mode](/images/penetration-testing/quick_start_protect_mode.png)
{: .notice--danger}

1. [Cài đặt EC-CUBE bằng docker-compose](https://thanpd-ptit.github.io/doc4-ec-cube-vn/quickstart/docker_compose_install)
1. Tạo dữ liệu test
    ```shell
    ## Đặt APP_ENV: dev
    sed -i.bak -e 's/APP_ENV: "prod"/APP_ENV: "dev"/g' ./docker-compose.yml
    docker-compose up -d # Áp dụng thay đổi
    ## Tạo 1 customer
    docker-compose -f docker-compose.yml -f docker-compose.owaspzap.yml exec ec-cube bin/console eccube:fixtures:generate --products=0 --customers=1 --orders=0
    ## Đổi email thành zap_user@example.com
    docker-compose -f docker-compose.yml -f docker-compose.owaspzap.yml exec ec-cube bin/console doctrine:query:sql "UPDATE dtb_customer SET email = 'zap_user@example.com' WHERE id = 1;"
    ## Khi test với ZAP, đặt lại APP_ENV: prod
    sed -i.bak -e 's/APP_ENV: "dev"/APP_ENV: "prod"/g' ./docker-compose.yml
    docker-compose up -d # Áp dụng thay đổi
    ```
1. Khởi động container OWASP ZAP
    ```shell
    docker-compose -f docker-compose.yml -f docker-compose.owaspzap.yml up -d zap
    ```
    - *Sẽ mất một chút thời gian để cập nhật addon*
    - Sau khi khởi động, truy cập `http://localhost:8081/zap/` bằng trình duyệt (trừ Firefox) để mở giao diện quản lý OWASP ZAP

    **Lưu ý:** Sau khi khởi động OWASP ZAP, giao diện sẽ nhỏ và một số nút toolbar bị ẩn. Hãy chuyển sang chế độ toàn màn hình để dễ sử dụng.
    ![Toàn màn hình](/images/penetration-testing/quick_start_fullwindow.png)
    {: .notice--info}
1. Mở Firefox, vào Cài đặt → Cài đặt mạng → Cài đặt kết nối proxy
   - Chọn **Thiết lập proxy thủ công**
   - HTTP proxy: localhost, Port: 8090
   - Tick vào **Sử dụng proxy này cho cả FTP và HTTPS**
1. Import chứng chỉ gốc SSL CA vào Firefox
   - Chứng chỉ được tạo ở `path/to/ec-cube/zap/owasp_zap_root_ca.cer`
   - Vào Cài đặt → Quyền riêng tư & bảo mật → Chứng chỉ → Xem chứng chỉ để mở trình quản lý chứng chỉ
   - Chọn Chứng chỉ CA → Nhập, chọn file `path/to/ec-cube/zap/owasp_zap_root_ca.cer`
   - Tick vào **Tin tưởng CA này để xác thực website**, nhấn OK và đóng cài đặt
1. Truy cập `https://ec-cube/` bằng Firefox để kiểm tra đã truy cập EC-CUBE qua proxy thành công
1. Import context
    ```shell
    ## Cho admin
    docker-compose -f docker-compose.yml -f docker-compose.owaspzap.yml exec zap zap-cli -p 8090 context import /zap/wrk/admin.context
    ## Cho frontend (login)
    docker-compose -f docker-compose.yml -f docker-compose.owaspzap.yml exec zap zap-cli -p 8090 context import /zap/wrk/front_login.context
    ## Cho frontend (guest)
    docker-compose -f docker-compose.yml -f docker-compose.owaspzap.yml exec zap zap-cli -p 8090 context import /zap/wrk/front_guest.context
    ```
   **Lưu ý:** *Nếu import nhiều context cùng lúc, có thể bị xung đột session và không đăng nhập được*
   {: .notice--warning}
1. Bật nút [Forced User Mode On/Off](https://www.zaproxy.org/docs/desktop/ui/tltoolbar/#--forced-user-mode-on--off){:target="_blank"} trên toolbar của OWASP ZAP để kích hoạt tự động đăng nhập khi test
   ![Forced User Mode On/Off](/images/penetration-testing/quick_start_forceusermode.png)
1. Tiến hành test
   1. Duyệt các trang bằng Firefox (khám phá thủ công)
   1. Thực hiện dynamic scan với các URL đã phát hiện
   1. Kiểm tra các cảnh báo (alert) được phát hiện


## Tham khảo

- [Sử dụng OWASP ZAP với Docker](https://pc.atsuhiro-me.net/entry/2019/08/19/011324){:target="_blank"}
- [Chạy OWASP ZAP bản Docker](https://qiita.com/koujimatsuda11/items/83558cd62c20141ebdda){:target="_blank"}
- [Hướng dẫn testing](https://owasp.org/www-pdf-archive/OTGv3Japanese.pdf){:target="_blank"}
