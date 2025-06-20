---
title: Cách sử dụng Sass (scss)
keywords: thiết kế 
tags: [thiết kế]
permalink: design_sass

summary: Cách chỉnh sửa Sass (scss)
---

CSS của EC-CUBE được viết bằng [Sass(scss)](http://sass-lang.com){:target="_blank"}.

1. [Vị trí lưu source scss](#vị-trí-lưu-source-scss)
1. [Cấu trúc thư mục và file scss](#cấu-trúc-thư-mục-và-file-scss)
1. [Cách build Sass(scss)](#sass_build)


## Vị trí lưu source Sass(scss)
- Source Sass được lưu tại thư mục sau:

```
[html]
 └─ [template]
     └─ [default] # admin là cho trang quản trị
         └─ [assets]
             ├─ [css]
             └─ [scss]
```

## Cấu trúc thư mục và file scss

Thư mục scss được cấu trúc để dễ bảo trì.<br>
Về thiết kế component và quy tắc viết CSS, EC-CUBE áp dụng quy tắc FLOCSS.<br>
Tham khảo thêm [Style Guide](https://eccube4-styleguide.herokuapp.com/){:target="_blank"}.

```
[assets]
 ├─ [css]
 │    ├─ style.css     # CSS được build ra từ scss
 │    └─ style.min.css # CSS rút gọn được build ra từ scss
 └─ [sass]
      ├─ [component]   # Chứa các module nhỏ (component) cơ bản
      ├─ [project]     # Chứa các module lớn như header, footer, trang chủ
      ├─ [mixins]      # Chứa các thiết lập style tái sử dụng
      ├─ [sections]    # Dùng để ghi đè
      └─ style.scss    # File import các scss khác
```

- component<br>
  Chứa các module nhỏ như tiêu đề, nút bấm, v.v...<br>
  Tham khảo Style Guide mục 1-9

- project<br>
  Chứa các module lớn như header, footer, trang chủ, v.v...<br>
  Tham khảo Style Guide mục 11-22

- mixins <br>
  Chứa các thiết lập style tái sử dụng hoặc dùng nhiều nơi.

- sections<br>
  Dùng để ghi đè các class CSS của component hoặc project.<br>
  Khi sử dụng, hãy thêm vào style.scss như sau:

```css
@import "sections/components";
@import "sections/projects";
```

- style.scss<br>
  File này import các file scss khác.<br>
  style.scss sẽ được build thành style.css và style.min.css.
  
  
### Về Style Guide

EC-CUBE cung cấp 'Style Guide' để bạn có thể kiểm tra các nguyên tắc thiết kế và quy tắc code cho CSS và HTML.
Tham khảo thêm tại các link sau:

- [Style Guide cho giao diện người dùng](https://github.com/EC-CUBE/Eccube-Styleguide){:target="_blank"}
- [Style Guide cho trang quản trị](https://github.com/EC-CUBE/Eccube-Styleguide-Admin){:target="_blank"}



## Cách build Sass(scss) {#sass_build}

1. [Chuẩn bị môi trường build](#chuẩn-bị-môi-trường-build)
1. [Cách build cho EC-CUBE 4.0.3 trở về trước](#build_eccube403)
1. [Cách build cho EC-CUBE 4.0.4 trở lên](#build_eccube404)


## Chuẩn bị môi trường build

EC-CUBE sử dụng [Gulp](https://gulpjs.com/){:target="_blank"} để build Sass.<br>
Yêu cầu cài đặt [Node.js](https://nodejs.org/ja/){:target="_blank"} trước.

- Node.js<br>
  Gulp chạy trên nền Node.js.<br>
  ※ Một số phiên bản Node.js mới có thể gây lỗi khi chạy Gulp, tham khảo [tại đây](https://qiita.com/KKKarin/items/bbb424fd93ef523a741a).

- Gulp<br>
  Dùng để chuyển đổi file Sass thành CSS.<br>
  EC-CUBE 4.0.3 trở về trước dùng Gulp3, từ 4.0.4 dùng Gulp4

**1. Cài Node.js vào máy tính**<br>

Tải Node.js từ [trang chủ Node.js](https://nodejs.org/ja/){:target="_blank"} và cài đặt.<br>
Kiểm tra Node.js đã cài bằng lệnh sau:
```shell
node -v
```

**2. Di chuyển vào thư mục gốc của ec-cube**<br>
Di chuyển vào thư mục chứa package.json, gulpfile.js.

```shell
cd path/to/eccube_root # thay path/to/eccube_root bằng đường dẫn thư mục EC-CUBE
```

**3. Tạo thư mục node_modules**<br>

Chạy lệnh sau để tạo thư mục node_modules:

```shell
npm install # tạo thư mục node_modules
```


## Cách build cho EC-CUBE 4.0.3 trở về trước {#build_eccube403}

Chạy lệnh sau để chuyển scss thành CSS:

```shell
npm run build # build scss thành style.css và style.min.css
```

CSS sau khi build sẽ được xuất ra `html/template/{admin,default}/assets/css/`.<br>
Sẽ có file style.css và style.min.css (phiên bản rút gọn).


### Lưu ý khi sử dụng template khác default ở EC-CUBE 4.0.3 trở về trước

Nếu bạn đổi template sang tên khác ngoài default, cần sửa giá trị trong gulpfile.js:<br>
Sửa phần default trong srcPattern tại `eccube_root/gulpfile.js`:
```
[ec-cube_root]
 └─ gulpfile.js # sửa thiết lập srcPattern
```

```js
const srcPattern = [
    'admin',
    'default' // đổi 'default' thành tên template đang dùng
];
```
※ Từ EC-CUBE 4.0.4 trở lên không cần thiết lập này.<br>
※ Một số template có thể có vị trí/lưu trữ Sass khác, hãy tham khảo tài liệu của template bạn mua.


## Cách build cho EC-CUBE 4.0.4 trở lên {#build_eccube404}

Từ 4.0.4, đã bổ sung chức năng tự động build (watch).<br>
[Lưu ý cho Windows](#win_sass)

File cấu hình nằm ở `gulp/config.js`, hãy thiết lập trước khi build.

```shell
npm run build # build scss thành style.css và style.min.css
```
```shell
npm run watch # theo dõi thay đổi scss, tự động build style.css và style.min.css
```
```shell
npm run start # theo dõi, tự động build & tự động reload trình duyệt
```

**Dừng watch hoặc start: nhấn tổ hợp phím "Ctrl" + "C"**


CSS sau khi build sẽ được xuất ra `html/template/{admin,default}/assets/css/`.<br>
Sẽ có file style.css và style.min.css (phiên bản rút gọn).



### 【Lưu ý】Với Windows cần sửa một số đoạn mã {#win_sass}

Ở bản đóng gói 4.0.4 trên Windows, có lỗi không build đúng file style.css, hãy sửa 2 chỗ sau trong gulpfile.js (dòng 90 và 115):
```js
path.dirname = path.dirname.replace('/scss', '/css') # trước khi sửa
```

```js
path.dirname = path.dirname.replace(/scss$/, 'css') # sau khi sửa
```