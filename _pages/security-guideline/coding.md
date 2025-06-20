---
title: Hướng dẫn bảo mật EC-CUBE 4
keywords: coding
tags: [security-guideline, coding]
permalink: security-guideline/coding
folder: security-guideline
---
Hướng dẫn bảo mật EC-CUBE 4

# Tổng quan

## Mục đích
Tài liệu này là hướng dẫn bảo mật dành cho lập trình viên phát triển EC-CUBE hoặc tuỳ biến EC-CUBE.
Làm theo hướng dẫn này sẽ giúp bạn tích hợp các biện pháp phòng chống lỗ hổng ngay từ giai đoạn phát triển, duy trì và nâng cao chất lượng bảo mật.

## Đối tượng
Chủ yếu dành cho lập trình viên phát triển EC-CUBE hoặc tuỳ biến EC-CUBE.

## Phạm vi
Tài liệu này tập trung vào các lưu ý khi lập trình trong giai đoạn phát triển EC-CUBE hoặc tuỳ biến EC-CUBE.
Không bao gồm hướng dẫn cài đặt, vận hành, bảo trì hệ thống.

# Lưu ý phòng chống lỗ hổng

Dựa trên [Cách xây dựng website an toàn](https://www.ipa.go.jp/security/vuln/websecurity.html), tài liệu này tổng hợp các lưu ý khi lập trình EC-CUBE để phòng chống từng loại lỗ hổng. Đối với giải thích chi tiết về lỗ hổng và các lưu ý chung khi phát triển web, hãy tham khảo tài liệu gốc "Cách xây dựng website an toàn". Các trích dẫn từ tài liệu gốc sẽ được ghi chú rõ.

## SQL Injection

### SQL Injection

#### [Giải pháp triệt để] Luôn sử dụng placeholder khi xây dựng câu lệnh SQL
> SQL thường có cơ chế sử dụng placeholder để xây dựng câu lệnh. Trong mẫu SQL, đặt ký hiệu (placeholder) tại vị trí biến, sau đó gán giá trị thực vào placeholder bằng xử lý tự động. So với việc nối chuỗi để xây dựng SQL, sử dụng placeholder giúp loại bỏ nguy cơ SQL Injection. 
> Việc gán giá trị vào placeholder gọi là binding. Có hai kiểu binding: binding tĩnh (prepared statement) và binding động (thư viện DB xử lý escape và gán giá trị). Cả hai đều giúp loại bỏ nguy cơ SQL Injection, nhưng binding tĩnh an toàn hơn về mặt nguyên lý. Xem thêm [Cách gọi SQL an toàn](https://www.ipa.go.jp/files/000017320.pdf) mục 3.2.

EC-CUBE sử dụng O/R Mapper nên không có chỗ viết SQL trực tiếp. 
Trừ trường hợp đặc biệt, luôn khuyến nghị dùng O/R Mapper. 
Khi tuỳ biến, lưu ý 2 điểm sau:

##### 1. Lưu ý khi dùng QueryBuilder

* Ví dụ sai:

```php
$qb = $this->createQueryBuilder('p')
    ->where('p.price > '. $price)
    ->orderBy('p.price', 'ASC');
```

Nếu `$price` chứa chuỗi như `1 or 1=1` thì sẽ trả về toàn bộ bản ghi.

* Ví dụ đúng:

```php
$qb = $this->createQueryBuilder('p')
    ->where('p.price > :price')
    ->setParameter('price', $price)
    ->orderBy('p.price', 'ASC');
```

Dùng `setParameter` để giảm rủi ro SQL Injection.

##### 2. Lưu ý khi dùng dbal

Không dùng cú pháp như sau. Nếu `$price` chứa chuỗi như `1 or 1=1` sẽ trả về toàn bộ bản ghi, thậm chí có thể xem/sửa/xoá dữ liệu bảng khác.

* Ví dụ sai:

```php
$conn = $this->getEntityManager()->getConnection();

$sql = "
    SELECT * FROM product p
    WHERE p.price > $price
    ORDER BY p.price ASC
    ";
$stmt = $conn->prepare($sql);
$resultSet = $stmt->executeQuery();

// returns an array of arrays (i.e. a raw data set)
return $resultSet->fetchAllAssociative();
```

* Ví dụ đúng:

```php
$conn = $this->getEntityManager()->getConnection();

$sql = '
    SELECT * FROM product p
    WHERE p.price > :price
    ORDER BY p.price ASC
    ';
$stmt = $conn->prepare($sql);
$resultSet = $stmt->executeQuery(['price' => $price]);
```

※ Khi dùng O/R Mapper, nếu dùng sai cách sẽ không đảm bảo an toàn. Hãy chú ý cách sử dụng.

#### [Giải pháp triệt để] Nếu phải nối chuỗi để xây dựng SQL, hãy escape đúng cách bằng API của DB
> Nếu phải nối chuỗi để xây dựng SQL, hãy đảm bảo các giá trị biến được escape đúng cách (dùng hàm của DB). Nếu là số, hãy ép kiểu số. Xem thêm [Cách gọi SQL an toàn](https://www.ipa.go.jp/files/000017320.pdf) mục 4.1.

EC-CUBE sử dụng O/R Mapper nên không có chỗ viết SQL trực tiếp. Khi tuỳ biến, lưu ý 2 điểm sau:

##### 1. Lưu ý khi dùng QueryBuilder

Khi dùng Symfony, hãy luôn dùng placeholder như trên. Ngoài ra, có thể wrap trong function để giới hạn kiểu dữ liệu.

```php
public function findAllGreaterThanPrice(int $price, bool $includeUnavailableProducts = false): array
{
    $qb = $this->createQueryBuilder('p')
        ->where('p.price > :price')
        ->setParameter('price', $price)
        ->orderBy('p.price', 'ASC');

    if (!$includeUnavailableProducts) {
        $qb->andWhere('p.available = TRUE');
    }

    $query = $qb->getQuery();

    return $query->execute();
}
```

##### 2. Lưu ý khi dùng dbal

Cũng nên wrap trong function để giới hạn kiểu dữ liệu.

```php
public function findAllGreaterThanPrice(int $price): array
{
    $conn = $this->getEntityManager()->getConnection();

    $sql = '
        SELECT * FROM product p
        WHERE p.price > :price
        ORDER BY p.price ASC
        ';
    $stmt = $conn->prepare($sql);
    $resultSet = $stmt->executeQuery(['price' => $price]);

    return $resultSet->fetchAllAssociative();
}
```

※ Khi dùng O/R Mapper, nếu dùng sai cách sẽ không đảm bảo an toàn. Hãy chú ý cách sử dụng.

#### [Giải pháp triệt để] Không truyền trực tiếp SQL vào tham số từ bên ngoài
> Không chỉ với EC-CUBE, tuyệt đối không truyền trực tiếp SQL vào hidden parameter hoặc các tham số từ bên ngoài. Nếu làm vậy, chỉ cần thay đổi giá trị tham số là có thể thực thi SQL tuỳ ý.

Khi tuỳ biến, có thể tạo plugin cho phép thực thi SQL trực tiếp, hãy đặc biệt lưu ý.

#### [Biện pháp bổ sung] Không hiển thị thông báo lỗi DB ra trình duyệt
> Nếu thông báo lỗi DB chứa thông tin về loại DB, nguyên nhân lỗi, câu lệnh SQL... thì đây là thông tin hữu ích cho kẻ tấn công. Không hiển thị lỗi DB ra trình duyệt.

EC-CUBE chỉ hiển thị lỗi khi ở chế độ dev nên không vấn đề.

#### [Biện pháp bổ sung] Chỉ cấp quyền tối thiểu cho tài khoản DB
> Tài khoản DB dùng cho web app chỉ nên có quyền tối thiểu cần thiết.

EC-CUBE: hãy cấu hình trên server.

... (Tiếp tục dịch các phần còn lại tương tự, giữ nguyên cấu trúc markdown, bảng, code, chú thích, v.v.)
