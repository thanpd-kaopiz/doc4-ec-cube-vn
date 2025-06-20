---
title: Tổng quan phát triển
description: Giới thiệu về workflow phát triển và các công cụ sử dụng trong phát triển EC-CUBE.
keywords: contribution-guide workflow
tags: [contribution-guide, guideline]
permalink: contribution-guide/overview
folder: contribution-guide
---

Giới thiệu về workflow phát triển và các công cụ sử dụng trong phát triển EC-CUBE.

## Quy trình phát triển

Việc phát triển EC-CUBE core được thực hiện dựa trên GitHub Flow.

Xem chi tiết tại các trang tham khảo dưới đây:

- [Giới thiệu về GitHub Flow](https://gist.github.com/Gab-km/3705015){:target="_blank"}
- [Sơ đồ khái niệm GitHub Flow](http://qiita.com/tbpgr/items/4ff76ef35c4ff0ec8314){:target="_blank"}

## Trao đổi thông tin & giao tiếp

- <a href="https://qiita.com/tags/ec-cube4/" target="_blank">Qiita</a>
    - Chia sẻ các tips khi phát triển.
- <a href="https://ec-cube.slack.com/messages/" target="_blank">Slack</a>
    - Công cụ giao tiếp giữa các lập trình viên.
- <a href="https://github.com/EC-CUBE/ec-cube/issues/" target="_blank">GitHub Issues</a>
    - Nơi tập trung các thông tin quan trọng như "Yêu cầu cải tiến, ý tưởng, báo cáo bug".

## Công cụ

### Quản lý phiên bản

- <a href="https://github.com/EC-CUBE/ec-cube/" target="_blank">GitHub</a>
    - Ngoài việc chia sẻ thông tin qua Issues, còn quản lý version và so sánh mã nguồn.

### Test & Phân tích mã nguồn

- <a href="https://travis-ci.org/" target="_blank">Travis</a>
    - Chạy unit test trên môi trường chỉ định.

- <a href="https://ci.appveyor.com/login" target="_blank">AppVeyor</a>
    - CI dùng để test trên môi trường Windows.

- <a href="https://scrutinizer-ci.com/" target="_blank">Scrutinizer</a>
    - Phân tích mã nguồn tĩnh.
