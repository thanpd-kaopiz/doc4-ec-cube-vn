---
title: Chức năng quản lý Git trên ec-cube.co
keywords: co ec-cube.co Cloud version Chức năng quản lý Git
tags: [co, ec-cube.co]
permalink: co/co_git
folder: co
---

---

Chức năng quản lý Git cho gói Standard như sau:

|                                               |Đối tượng quản lý Git|Ảnh hưởng khi dùng Plugin|Thao tác từ màn hình quản lý|
|-----------------------------------------------|--------------------|------------------------|----------------------------|
| \|\-\- app                                  |                    |                        |                            |
| \|  \|\-\- Customize                        | o                  |                        |                            |
| \|  \|\-\- DoctrineMigrations               | x                  |                        |                            |
| \|  \|\-\- Plugin                           | x                  | o                      |                            |
| \|  \|\-\- PluginData                       | x                  | o                      |                            |
| \|  \|\-\- config                           | x                  |                        |                            |
| \|  \|\-\- proxy                            | x                  |                        |                            |
| \|  `\-\- template                          | o                  | o                      | o                          |
| `\-\- html                                  |                    |                        |                            |
|  \|\-\- plugin                              | o                  | o                      |                            |
|  \|\-\- template                            | o                  | o                      | o                          |
|  \|\-\- upload                              | x                  |                        |                            |
|  \|  \|\-\- save_image                      | x                  |                        | o                          |
|  \|  `\-\- temp_image                       | x                  |                        | o                          |
|  `\-\- user_data                            | x                  |                        | o                          |
|    `-- assets                               | x                  |                        | o                          |

## Giải thích bảng

1. Đối tượng quản lý Git: Tài nguyên có thể phản ánh lên source code hoặc thư mục qua Git
1. Ảnh hưởng khi dùng Plugin: Khi cài đặt/gỡ cài đặt/bật/tắt plugin, source code có thể bị ghi đè
1. Thao tác từ màn hình quản lý: Có thể cập nhật từ màn hình quản lý (quản lý trang/template, v.v.)

Các thư mục dưới đây là code gốc của EC-CUBE nên không thuộc phạm vi quản lý:
- DoctrineMigrations
- config
- proxy

Về "Ảnh hưởng khi dùng Plugin" và "Thao tác từ màn hình quản lý":
- Ngoài việc phản ánh từ git, các file được tạo hoặc thay đổi bởi thao tác khác cũng sẽ được quản lý bởi git.
- Khi đó, thay đổi từ phía màn hình quản lý sẽ được commit là chính thức.
