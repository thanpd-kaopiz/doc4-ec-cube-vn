---
title: Kiểm thử xâm nhập EC-CUBE với OWASP ZAP
permalink: /penetration-testing
---
## Giới thiệu

**Chú ý!!**
Đây là công cụ thực hiện tấn công thực tế vào website để kiểm tra lỗ hổng bảo mật.
Chỉ sử dụng trên môi trường Docker local, tuyệt đối không sử dụng trên site đang hoạt động.
Có thể gây thay đổi hoặc xóa dữ liệu ngoài ý muốn.<br />
**Bạn tự chịu trách nhiệm khi thực hiện test, công ty EC-CUBE và cộng đồng phát triển liên quan không chịu bất kỳ trách nhiệm nào.**
{: .notice--danger}

Nếu bạn muốn tạo môi trường test nhanh, hãy xem [Bắt đầu nhanh](/penetration-testing/quick_start).
{: .notice--success}

Hiện tại, quá trình tự động hóa kiểm thử này đang được phát triển. Nếu muốn thử, hãy xem [README này](https://github.com/EC-CUBE/ec-cube/tree/4.1/zap/selenium/ci/TypeScript#automated-security-tests-with-owasp-zap){:target="_blank"}.
{: .notice--success}

Tài liệu này được tạo ra nhằm chia sẻ quy trình kiểm thử bảo mật trước khi phát hành EC-CUBE, giúp nhiều người dùng có thể áp dụng.
Không chỉ là hướng dẫn thao tác, tài liệu còn bao gồm tư duy kiểm thử, cách cải thiện quy trình, v.v.

OWASP ZAP sử dụng ở đây là một công cụ rất mạnh, nhưng để kiểm thử đầy đủ cần vượt qua một số vấn đề đặc thù của EC-CUBE.
Ngay cả khi không phát hiện lỗ hổng bảo mật, cũng có thể do kiểm thử chưa đủ.

Không nên chỉ tin vào kết quả kiểm thử, hãy kết hợp với việc nhờ chuyên gia kiểm tra để xây dựng môi trường bảo mật vững chắc hơn.

## Giới thiệu tổng quan

- [Đối tượng độc giả](/penetration-testing/introduction#%E5%AF%BE%E8%B1%A1%E3%81%AE%E8%AA%AD%E8%80%85)

### Về kiểm thử bảo mật

- [Các loại kiểm thử bảo mật](/penetration-testing/introduction/type)
- [Về kiểm thử xâm nhập ứng dụng web](/penetration-testing/introduction/penetration-test)
- [Cấu trúc kiểm thử xâm nhập ứng dụng web](/penetration-testing/introduction/layout)

### Về OWASP ZAP

- [Quy trình kiểm thử với OWASP ZAP](/penetration-testing/about_owaspzap#owasp-zap-%E3%81%A7%E3%81%AE%E3%83%86%E3%82%B9%E3%83%88%E3%81%AE%E6%B5%81%E3%82%8C)

## Lập kế hoạch kiểm thử

- [Bối cảnh, mục tiêu kiểm thử](/penetration-testing/planning/purpose)
- [Đối tượng kiểm thử](/penetration-testing/planning/target)
- [Chiến lược kiểm thử](/penetration-testing/planning/strategy)
- [Lập lịch kiểm thử](/penetration-testing/planning/scheduling)
- [Cách đánh giá kết quả kiểm thử](/penetration-testing/review)

## Thực hiện kiểm thử

- [Xây dựng môi trường](/penetration-testing/testing/settings)
- [Lưu ý khi thực hiện kiểm thử](/penetration-testing/testing/attention)
- [Cách sửa để kiểm thử không bị dừng](/penetration-testing/testing/apply_patch)
- [Phân loại context](/penetration-testing/testing/context)
- [Cách khám phá thủ công](/penetration-testing/testing/manual_explore)
- [Cách thực hiện dynamic scan](/penetration-testing/testing/active_scan)
- [Danh sách URL kiểm thử thủ công](/penetration-testing/testing/manual_inspection_urls)

## Đánh giá kiểm thử

- [Xuất báo cáo](/penetration-testing/review#%E3%83%AC%E3%83%9D%E3%83%BC%E3%83%88%E5%87%BA%E5%8A%9B)
- [Cách đánh giá cảnh báo bảo mật](/penetration-testing/review#%E3%82%BB%E3%82%AD%E3%83%A5%E3%83%AA%E3%83%86%E3%82%A3%E3%82%A2%E3%83%A9%E3%83%BC%E3%83%88%E3%81%AE%E8%A9%95%E4%BE%A1%E6%96%B9%E6%B3%95)
- [Cách xác định cảnh báo giả](/penetration-testing/review#%E8%AA%A4%E6%A4%9C%E7%9F%A5%E3%81%8B%E3%81%A9%E3%81%86%E3%81%8B%E3%81%AE%E5%88%A4%E5%AE%9A)

## Cải thiện bảo mật

- [Khi phát hiện lỗ hổng bảo mật](/penetration-testing/improvement#%E3%82%BB%E3%82%AD%E3%83%A5%E3%83%AA%E3%83%86%E3%82%A3%E3%83%9B%E3%83%BC%E3%83%AB%E3%82%92%E7%99%BA%E8%A6%8B%E3%81%97%E3%81%9F%E5%A0%B4%E5%90%88)
- [Cách báo cáo lỗ hổng](/penetration-testing/improvement#%E8%84%86%E5%BC%B1%E6%80%A7%E3%81%AE%E5%A0%B1%E5%91%8A%E6%96%B9%E6%B3%95)
- [Phản hồi vào core EC-CUBE](/penetration-testing/improvement#ec-cube%E6%9C%AC%E4%BD%93%E3%81%B8%E3%81%AE%E5%8F%8D%E6%98%A0)
- [Cải thiện phương pháp kiểm thử](/penetration-testing/improvement#%E3%83%86%E3%82%B9%E3%83%88%E6%96%B9%E6%B3%95%E3%81%AE%E6%94%B9%E5%96%84)
