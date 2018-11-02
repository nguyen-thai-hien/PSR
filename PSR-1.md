PSR-1 Basic Coding Standard
===========================
Những tiêu chuẩn của phần này bao gồm những gì được coi là chuẩn code.
Việc này đảm bảo một mức độ cao về khả năng tương tác của code PHP được chia sẻ.

### 1. Overview
* Files **phải** sử dụng thẻ `<?php` và `<?=`.
* Files **phải** dùng *UTF-8 without BOM* cho code PHP.
* Files chỉ **nên** khai báo các biểu tượng (như Class, Function, Constant, ...), hoặc để làm các việc phụ (như xuất ra màn hình, cấu hình, ...). Nhưng không được làm một lúc cả 2 việc.
* Namespaces và các class **phải** tuân theo `autoloading` PSR: [[PSR-0](https://github.com/runsystem-hiennt2/PSR/blob/master/PSR-0.md),[PSR-4](https://github.com/runsystem-hiennt2/PSR/blob/master/PSR-4.md)].
* Tên class **phải** khai báo theo kiểu `StudlyCaps`.
* Tên constant **phải** khai báo tất cả viết hoa và ngăn cách bằng dấu gạch dưới.
* Tên method (function) **phải** khai báo theo kiểu`camelCase`.

### 2. Files
#### 2.1 PHP tags
Code PHP **phải** dùng tag dài `<?php ?>` hoặc tag echo ngắn `<?= ?>`, KHÔNG ĐƯỢC dùng những tag với từ khóa khác.

#### 2.2 Character Encoding
Code PHP **phải** chỉ dùng `UTF-8 without BOM`.

#### 2.3 Side effects
Một file chỉ **nên** khai báo các biểu tượng (như Class, Function, Constant, ...) và không có những `side effects` khác, hoặc chỉ **nên** thực thi các logic với `side effects`, nhưng **không nên** làm cả 2 việc.

Cụm từ `side effects` nghĩa là thực thi các logic không liên quan trực tiếp đến việc xây dựng Class, Function, Constant, ...

`Side effects` bao gồm: xuất ra màn hình, sử dụng `require` hoặc `include`, kết nối với services ngoài, chỉnh sửa file ini, bung ra các lỗi hoặc ngoại lệ, chỉnh sửa các biến toàn cục hoặc tĩnh, đọc hoặc viết ra file, và hơn nữa.

Ví dụ sau đây là một ví dụ của việc sử dụng cả `declarations` và `side effects`, đây là ví dụ mà chúng ta cần phải tránh:
```php
<?php
// side effect: change ini settings
ini_set('error_reporting', E_ALL);

// side effect: loads a file
include "file.php";

// side effect: generates output
echo "<html>\n";

// declaration
function foo()
{
    // function body
}
```

Và ví dụ sau là chỉ sử dụng `declarations` mà không có `side effects`, đây là ví dụ mà chúng ta cần phải bắt chước:
```php
<?php
// declaration
function foo()
{
    // function body
}

// conditional declaration is *not* a side effect
if (! function_exists('bar')) {
    function bar()
    {
        // function body
    }
}
```

### 3. Namespace and Class Names
Namespaces và các tên class **phải** tuân theo `autoloading` PSR: [[PSR-0](https://github.com/runsystem-hiennt2/PSR/blob/master/PSR-0.md),[PSR-4](https://github.com/runsystem-hiennt2/PSR/blob/master/PSR-4.md)].

Điều này có nghĩa là mỗi class chỉ ở trong một file của chính nó, và chỉ trong một namespace của một cấp cao nhất là `vendor`.

Tên class **phải** khai báo theo kiểu `StudlyCaps`.

Code viết bởi PHP 5.3 và về sau **phải** sử dụng một hình thức namespace.

Sau đây là ví dụ:
```php
<?php
// PHP 5.3 and later:
namespace Vendor\Model;

class Foo
{
}
```

Tuy nhiên, code viết cho PHP 5.2 và trở về trước **nên** sử dụng quy ước giả của với tiền tố là `Vendor_` ở tên class:
```php
<?php
// PHP 5.2.x and earlier:
class Vendor_Model_Foo
{
}
```

### 4. Class Constants, Properties, and Methods
Thuật ngữ *Class* đề cập đến toàn bộ các Class, Interface và Traits.

#### 4.1 Constants
Tên các constant **phải** khai báo với toàn bộ từ viết hoa và cách nhau bằng dấu gạch dưới. Ví dụ:
```php
<?php
namespace Vendor\Model;

class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
```

#### 4.2 Properties
Việc sử dụng tên của property **có thể** tuân theo `$StudlyCaps`, `$camelCase` hay `$under_score`.
Tuy nhiên, việc sử dụng này **nên** được áp dụng thống nhất trong phạm vi hợp lý. Những phạm vi như: vendor-level, package-level, class-level hoặc method-level.

#### 4.3 Methods
Tên method cần **phải** khởi tạo tuân theo `camelCase()`. 
