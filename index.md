---
layout: single
author_profile: false
title: Tài liệu dành cho nhà phát triển EC-CUBE 4
description: "Đây là trang tài liệu dành cho nhà phát triển EC-CUBE 4. Cung cấp thông tin về cách cài đặt EC-CUBE, tuỳ biến hệ thống và phát triển plugin."
keywords: Về trang này, QuickStart
sidebar:
  nav: "docs"
permalink: /
---

Đây là trang tài liệu dành cho nhà phát triển EC-CUBE 4.
Cung cấp thông tin về cách cài đặt EC-CUBE, hướng dẫn phát triển, các khái niệm kỹ thuật, hướng dẫn tuỳ biến hệ thống, phát triển plugin, Cookbook và nhiều thông tin hữu ích khác.

{: .notice--danger}
- 2021/05/10 [Thông báo cho nhà phát triển plugin: Vui lòng kiểm tra mã nguồn](https://drive.google.com/file/d/1kCHwoWrveHGPPkH2mu1cz6o2XfNv4Lsq/view?usp=sharing){:target="_blank"} đã được công bố.
- 2021/06/29 EC-CUBE 4.0.6 trở về trước có chứa [lỗ hổng bảo mật mức "Cao"](https://www.ec-cube.net/info/weakness/index.php?level=0&version=4.0){:target="_blank"}. Vui lòng nâng cấp lên EC-CUBE 4.0.6-p1 hoặc mới hơn.
- 2023/02/28 [Cách khắc phục lỗi không cài được plugin trên bản 4.2](/quickstart/trouble-shooting-for-plugin-install) đã được đăng tải. Đặc biệt dành cho **người dùng thuê server không cài được plugin bản 4.2**.
{: .notice--danger}

Nếu có thắc mắc về nội dung tài liệu hoặc tuỳ biến, vui lòng tham khảo các cách sau:
+ Đăng Issue lên [GitHub](https://github.com/EC-CUBE/doc4.ec-cube.net/){:target="_blank"} như với EC-CUBE chính thức. Xem chi tiết [tại đây](/documents/request)
+ Tham gia [các sự kiện, hội thảo UG sắp tới](https://www.ec-cube.net/event/){:target="_blank"}

Việc bổ sung hoặc chỉnh sửa tài liệu cũng được tiếp nhận qua [GitHub](https://github.com/EC-CUBE/doc4.ec-cube.net/){:target="_blank"}. Xem hướng dẫn [tại đây](/documents/writing-and-formatting)


# Về ec-cube.co

## ec-cube.co

Tổng hợp thông tin kỹ thuật về phiên bản cloud "ec-cube.co".

+ [ec-cube.co là gì](/co)
+ [Về bảo mật](/co/co_security)
+ [Chỉ dẫn cập nhật](/co/co_update_guidelines)
+ [Console](/co/co_console)
+ [Quy tắc đặt tên](/co/co_naming_rules)
+ [Chức năng quản lý Git](/co/co_git)
+ [Cách sử dụng thư mục tuỳ biến](/co/co_customize_dir_usage)
+ [Xây dựng môi trường test](/co/co_staging)
+ [Lấy log](/co/co_log)
+ [FAQ](/co/co_faq)

# Về EC-CUBE chính

## Giới thiệu

Tổng hợp thông tin cơ bản và những điều cần lưu ý về EC-CUBE.

+ [Phiên bản mới nhất ](/quickstart/latest_version)
+ [Yêu cầu hệ thống](/quickstart/requirement)
+ [Lưu ý khi dùng môi trường production](/quickstart/cautions_of_prod)

## Thông tin cho người mới bắt đầu

Tổng hợp thông tin học tập cho người mới sử dụng EC-CUBE.

+ [Các bước học tập](/learning/learning_step)

## Cài đặt

Tổng hợp các phương pháp cài đặt.

+ [Các phương pháp cài đặt](/quickstart/install)
+ [Giao diện dòng lệnh](/quickstart/cli)

## Nâng cấp phiên bản

Tổng hợp thông tin về nâng cấp và migration.

+ [Nâng cấp từ 4.2 lên 4.3](/update43)
+ [Migration từ 4.2 lên 4.3](/update-42-43)
+ [Migration từ 4.1 lên 4.2](/update-41-42)
+ [Nâng cấp từ 4.0 lên 4.1](/update41)
+ [Migration từ 4.0 lên 4.1](/update-40-41)
+ [Nâng cấp bản 4.2](/update42x)
+ [Nâng cấp bản 4.1](/update41x)
+ [Nâng cấp bản 4.0](/update)
+ [Lưu ý với bản 4.0.3](/update/4_0_3)
+ [Hỗ trợ SameSite Cookie](/hotfix_samesite_cookie)

## Đặc tả hệ thống

Tổng hợp đặc tả và chức năng hệ thống.

+ [ER Diagram](https://github.com/EC-CUBE/eccube-specification/tree/4.0/ER-D){:target="_blank"}
+ [Tài liệu kiểm thử tích hợp](https://github.com/EC-CUBE/eccube-specification/tree/4.0/IntegrationTest){:target="_blank"}
+ [Đặc tả WebAPI](https://github.com/EC-CUBE/eccube-api4){:target="_blank"}

### Đặc tả chức năng

+ [Danh sách chức năng](https://www.ec-cube.net/product/functions.php){:target="_blank"}
+ [Liên quan đến đơn hàng](/spec_order)
+ [Cài đặt thuế suất](/spec_tax)
+ [Cài đặt phương thức thanh toán](/spec_payment)

## Tuỳ biến hệ thống

Tổng hợp các phương pháp tuỳ biến hệ thống.

+ [Cấu trúc thư mục](/spec_directory-structure)
+ [Tuỳ biến Controller](/customize_controller)
+ [Tuỳ biến Entity](/customize_entity)
+ [Tuỳ biến Repository](/customize_repository)
+ [Tuỳ biến FormType](/customize_formtype)
+ [Tuỳ biến luồng mua hàng](/customize_service)
+ [Tuỳ biến trạng thái đơn hàng](/customize_order_state_machine)
+ [Tuỳ biến template](/customize_template)
+ [Tuỳ biến chức năng throttling](/customize_throttling)
+ [Quản lý whitelist trong Twig Sandbox](/customize_twig_sandbox)
+ [Mở rộng với chức năng của Symfony](/customize_symfony)
+ [Phát triển Command với Symfony](/customize_symfony#command)

## Tuỳ biến giao diện

Tổng hợp các phương pháp tuỳ biến giao diện.

+ [Cơ bản về template thiết kế](/design_template)
+ [Thay đổi layout form](/design_form)
+ [Sử dụng block](/design_block)
+ [Quản lý layout](/design_layout)
+ [Sử dụng CSS](/design_css)
+ [Sử dụng Sass(scss)](/design_sass)

+ [Tài liệu tham khảo thiết kế giao diện người dùng](http://eccube4-styleguide.herokuapp.com/){:target="_blank"}
+ [Tài liệu tham khảo thiết kế quản trị](https://thanpd-ptit.github.io/doc4-ec-cube-vn/pdf/ec-cube4_design-guide180930.pdf){:target="_blank"}

+ [Template giao diện người dùng cho Adobe XD](http://downloads.ec-cube.net/manual/documents/eccube4_xd_front_template.zip?argument=2qpV46CP&dmai=a5bf51b05bacc5){:target="_blank"}
+ [Template giao diện quản trị cho Adobe XD](http://downloads.ec-cube.net/manual/documents/eccube4_xd_admin_template.zip?argument=2qpV46CP&dmai=a5bf51b05bacc5){:target="_blank"}

## Phát triển plugin

Tổng hợp các phương pháp phát triển plugin.

+ [Đặc tả plugin](/plugin_spec)
+ [Cài đặt plugin](/plugin_install)
+ [Khắc phục sự cố plugin](/plugin_error)
+ [Plugin mẫu](/plugin_sample)
+ [Phát triển plugin](/plugin_development)
+ [Kiểm tra cài đặt qua Owners Store](/plugin_mock_package_api)
+ [Quy tắc đặt tên plugin](/plugin_naming_conventions)
+ [Mở rộng navigation quản trị](/plugin_admin_nav)

## Thay đổi cấu hình

Tổng hợp các phương pháp thay đổi cấu hình hệ thống.

+ [Đa ngôn ngữ](/i18n_multilingualization)
+ [Tiền tệ](/i18n_currency)
+ [Múi giờ](/i18n_timezone)
+ [Cài đặt môi trường](/environmental_setting)
+ [Chế độ debug](/debug_mode)
+ [Thay đổi phương thức lưu session](/session_handler_settings)

## Công cụ phát triển

Tổng hợp các công cụ hỗ trợ phát triển.

+ [MailCatcher](/development-tools/mail-catcher)

## Kiểm thử bảo mật

Tổng hợp thông tin về kiểm thử bảo mật.

+ [Giới thiệu](/penetration-testing)
+ [Quick Start](/penetration-testing/quick_start)
+ [Giới thiệu tổng quan](/penetration-testing/introduction)
+ [Về OWASP ZAP](/penetration-testing/about_owaspzap)
+ [Lập kế hoạch kiểm thử](/penetration-testing/planning)
+ [Thực hiện kiểm thử](/penetration-testing/testing)
+ [Đánh giá kiểm thử](/penetration-testing/review)
+ [Cải thiện bảo mật](/penetration-testing/improvement)

## Hướng dẫn bảo mật

Tổng hợp hướng dẫn bảo mật.

+ [Về coding](/security-guideline/coding)
+ [Tăng cường bảo mật khi phát triển plugin](/security-guideline/plugin)

## Tham khảo ngược

Tổng hợp các tips và ví dụ tuỳ biến hữu ích.

+ [Tips](/reverse-lookup/tips)
+ [Tổng hợp ví dụ tuỳ biến](/reverse-lookup/sample-code)

## Thông tin cho người vận hành

Xem hướng dẫn vận hành tại đây.

+ [Hướng dẫn quản trị, vận hành EC-CUBE 4](https://www.ec-cube.net/manual/ec-cube4/){:target="_blank"}

## Tham gia phát triển

Tổng hợp thông tin cho người muốn tham gia phát triển.

+ [Cách tham gia phát triển EC-CUBE (trang chính thức)](https://www.ec-cube.net/committer/){:target="_blank"}
+ [Tổng quan phát triển](/contribution-guide/overview)
+ [Cách tạo Pull Request](/contribution-guide/pull-request)

## Khi không tìm thấy tài liệu

Tổng hợp cách tham gia viết và bảo trì tài liệu.

+ [Yêu cầu tài liệu](/documents/request)
+ [Cách thêm, viết tài liệu](/documents/writing-and-formatting)
+ [Đăng tài liệu](/documents/contribute)

## Supporters

EC-CUBE nhận được sự hỗ trợ từ các đơn vị sau.

+ [SAKURA internet](https://www.sakura.ad.jp/){:target="_blank"}
[![SAKURA internet](./images/3-1-2line-rgb-whiteback.png)](https://www.sakura.ad.jp/){:target="_blank"}

+ [VAddy](https://vaddy.net/ja/){:target="_blank"}
[![VAddy](./images/VAddy_logo.png)](https://vaddy.net/ja/){:target="_blank"} 