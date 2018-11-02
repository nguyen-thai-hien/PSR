PSR-4: Autoloader
=================

### 1. Overview
PSR này mô tả đặc điểm kỹ thuật cho những class `autoloading` từ những đường dẫn file.
Nó hoàn toàn tương thích và **có thể** dùng bổ sung cho bất kỳ những `autoloading` khác, bao gồm cả [PSR-0](https://github.com/runsystem-hiennt2/PSR/blob/master/PSR-0.md).
PSR này cũng mô tả nơi đặt những file mà **có thể** tự động load.

### 2. Specification
1. Định nghĩa `class` đề cập đến các Class, Interface, Trait và các cấu trúc tương tự khác.
2. Một `fully qualified class name` **phải** theo dạng sau:

  ```
  \<NamespaceName>(\<SubNamespaceNames>)*\<ClassName>
  ```
  1. `Fully qualified class name` **phải** có tên namespace cấp cao nhất, cũng **có thể** hiểu như một **vendor namespace**.
  2. `Fully qualified class name` **có thể** có một hay nhiều tên `sub-namespace`.
  3. `Fully qualified class name` **phải** kết thúc bằng một tên class.
  4. Dấu gạch dưới không có ý nghĩa gì đối với `fully qualified class name` cả.
  5. Các ký tự bảng chữ cái trong `fully qualified class name` **có thể** là sự kết hợp của cả viết hoa lẫn viết thường.
  6. Tất cả tên class thì được dẫn đến với một kiểu phân biệt dạng chữ (hoa hoặc thường).
3. Khi load một file mà nó tương ứng với `fully qualified class name`...
  1. Một chuỗi liên tiếp của một hay nhiều `namespace đầu tiên` và các `sub-namespace`, không bao gồm dấu ngăn cách của `namespace đầu tiên`, trong một `fully qualified class name` (`namespace prefix`) thì ứng với ít nhất một `base directory`.
  2. Một chuỗi liên tiếp các `sub-namespace` sau `namespace prefix` thì ứng với một `subdirectory` bên trong `base directory`, trong đó các dấu ngăn cách của namespace đại diện cho các dấu ngăn cách của directory.
  `Subdirectory` **phải** tương ứng với các trường hợp của các `sub-namespace`. 
  3. Tên class kết thúc thì ứng với một tên file kết thúc với `.php`.
  Tên phải **phải** tương ứng với các trường hợp của tên class kết thúc.
4. Các thực thi của `autoloader` **không được** bung ra exception, **không được** đưa ra lỗi của bất kỳ level, và **không nên** trả về bất kỳ giá trị nào.

### 3. Examples
Bảng bên dưới trình bày đường dẫn của file tương ứng cho một `fully qualified class name` đầy đủ, `namespace prefix`, và `base directory`:

| FULLY QUALIFIED CLASS NAME   | NAMESPACE PREFIX | BASE DIRECTORY         | RESULTING FILE PATH                       |
|------------------------------|------------------|------------------------|-------------------------------------------|
| \Acme\Log\Writer\File_Writer | Acme\Log\Writer  | ./acme-log-writer/lib/ | ./acme-log-writer/lib/File_Writer.php     |
| \Aura\Web\Response\Status    | Aura\Web         | /path/to/aura-web/src/ | /path/to/aura-web/src/Response/Status.php |
| \Symfony\Core\Request        | Symfony\Core     | ./vendor/Symfony/Core/ | ./vendor/Symfony/Core/Request.php         |
| \Zend\Acl                    | Zend             | /usr/includes/Zend/    | /usr/includes/Zend/Acl.php                |

Cho một ví dụ thực thi của `autoloaders` thích hợp với chi tiết, vui lòng xem [file ví dụ](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader-examples.md).
Ví dụ thực thi **không phải** là cái nhìn như một phần của chi tiết và **có thể** thay đổi bất cứ khi nào.
