PSR-2 Coding Style Guide
========================
Hướng dẫn này bao gồm phần mở rộng của [PSR-1](https://github.com/runsystem-hiennt2/PSR/blob/master/PSR-1.md).

Mục đích chính là tối thiểu sự phức tạp khi lướt qua code của nhiều tác giả khác nhau, bằng cách là liệt kê ra một tập hợp những quy tắc về chuẩn code PHP.

Quy tắc ở đây được bắt nguồn từ sự tương đồng của nhiều thành viên trong dự án. Khi nhiều tác giả cùng hợp tác trên nhiều dự án, nó sẽ giúp bạn có một tập hợp các nguyên tắc.

### 1. Overview
* Code **phải** tuân thủ [PSR-1](https://github.com/runsystem-hiennt2/PSR/blob/master/PSR-1.md)
* Code **phải** sử dụng 4 whitespaces cho thụt dòng, không sử dụng tab.
* **Không phải** là một giới hạn cứng về chiều dài của dòng; giới hạn mềm **phải** là 120 ký tự; dòng **nên** là 80 ký tự hoặc ít hơn.
* **Phải** có một dòng trống ở dưới `namespace` hoặc vùng code khai báo `use`.
* Mở ngoặc nhọn của Class và Method **phải** nằm ở dòng tiếp theo, và đóng ngoặc nhọn **phải** tại dòng cuối phía sau nội dung.
* Phạm vi (public, protected, private) **phải** được khai báo trong toàn bộ property và method; `abstract` và `final` **phải** được khai báo trước phạm vi; còn `static` thì **phải** khai báo ngay phía sau phạm vi.
* Từ khóa của cấu trúc điều khiển (if, else, for, foreach, while, switch, ...) **phải** có một whitespace phía sau, tuy nhiên việc gọi method hoặc function thì **không phải** như vậy.
* Mở ngoặc nhọn của cấu trúc điều khiển **phải** nằm cùng trong một dòng, và đóng ngoặc nhọn **phải** tại dòng cuối phía sau nội dung.
* Mở dấu ngoặc đơn cho cấu trúc điều khiển **không được** có một whitespace phía sau, và trước đóng ngoặc đơn cũng vậy.

#### 1.1 Example
Ví dụ này sẽ cho chúng ta một cái nhìn tổng quát về các quy ước:
```php
<?php
namespace Vendor\Package;

use FooInterface;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class Foo extends Bar implements FooInterface
{
    public function sampleFunction($a, $b = null)
    {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }
    }

    final public static function bar()
    {
        // method body
    }
}
```

### 2. General
#### 2.1 Basic Coding Standard
Code **phải** tuân theo tất cả quy ước được nêu trong [PSR-1](https://github.com/runsystem-hiennt2/PSR/blob/master/PSR-1.md).

#### 2.2 Files
Tất cả những file PHP **phải** sử dụng `end-of-line` là LF (linefeed).
Tất cả những file PHP **phải** kết thúc ở cuối với một dòng trống.
Tag đóng `?>` **phải** được bỏ qua ở tất cả những file chỉ chứa code PHP.

#### 2.3 Lines
**Không phải** là một giới hạn cứng về chiều dài của dòng.

Giới hạn mềm chiều dài của dòng **phải** là 120 ký tự.

#### 2.4 Indenting
Code **phải** sử dụng thụt dòng 4 spaces, **không phải** là tab.

#### 2.5 Keywords and True/False/Null
[Keywords](http://php.net/manual/en/reserved.keywords.php) của PHP **phải** viết thường.
Các hằng số PHP như `true`, `false`, `null` cũng **phải** viết thường.

### 3. Namespace and Use Declarations
**Phải** có một dòng trống phía sau khởi báo `namespace`.
Tất cả khởi báo `use` **phải** ở dưới `namespace`.
**Phải** chỉ có một từ khóa `use` ở một dòng khai báo.
**Phải** có một dòng trống phía sau vùng khai báo `use`.

Ví dụ:
```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

// ... additional PHP code ...
```

### 4. Classes, Properties, and Methods
Thuật ngữ *Class* đề cập đến toàn bộ các Class, Interface và Traits.

#### 4.1 Extends and Implements
Từ khóa `extends` và `implements` **phải** khởi tạo trên cùng một dòng với tên class.

Mở ngoặc nhọn của class **phải** nằm ở dòng tiếp theo, và đóng ngoặc nhọn **phải** tại dòng cuối phía sau nội dung.
```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements \ArrayAccess, \Countable
{
    // constants, properties, methods
}
```

Nếu một class có nhiều `implements` thì chúng ta **có thể** chia theo nhiều dòng.
Với interface đầu tiên **phải** nằm ở dòng tiếp theo, và mỗi interface **phải** nằm trên một dòng. 
```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // constants, properties, methods
}
```

#### 4.2. Properties
Phạm vi **phải** được khai báo ở toàn bộ các property.

Từ khóa `var` thì **không phải** được dùng để khai báo property.

**Không được** khai báo nhiều hơn một property ở mỗi câu lệnh khai báo.

Tên property **không nên** bắt đầu bằng một gạch dưới để thể hiện phạm vi `protected` hay `private`.
 
 Ví dụ:
 ```php
 <?php
 namespace Vendor\Package;
 
 class ClassName
 {
     public $foo = null;
 }
  ```

#### 4.3 Methods
Phạm vi **phải** được khai báo ở toàn bộ các method.

Tên method **không nên** bắt đầu bằng một gạch dưới để thể hiện phạm vi `protected` hay `private`.

Phía sau tên method **không được** có space nào cả.
Mở ngoặc nhọn **phải** nằm ở dòng tiếp theo và đóng ở dòng kết tiếp của nội dung.
**Không được** có khoảng trống nào ở sau mở ngoặc đơn và ở trước đóng ngoặc đơn cũng vậy.

Ví dụ:
```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function fooBarBaz($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```

#### 4.4 Method argument
Trong danh sách argument, **không được** có whitespace trước dấu phẩy, và **phải** có một whitespace sau dấu phẩy.

Argument có giá trị mặc định **phải** nằm ở cuối danh sách.
```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function foo($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```

Danh sách argument **có thể** chia làm nhiều dòng, với argument đầu tiên **phải** nằm ở dòng tiếp theo, mỗi dòng **phải** là một argument.

Và khi chia như vậy, thì đóng ngoặc đơn và mở ngoặc nhọn cũng **phải** nằm ở một dòng riêng biệt.
```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = []
    ) {
        // method body
    }
}
```

#### 4.5 `abstract`, `final`, and `static`
Từ khóa `abstract` và `final` **phải** nằm trước phạm vi, và `static` thì **phải** nằm sau phạm vi.
```php
<?php
namespace Vendor\Package;

abstract class ClassName
{
    protected static $foo;

    abstract protected function zim();

    final public static function bar()
    {
        // method body
    }
}
```

#### 4.6 Method and Function Calls
Khi gọi method hoặc function, **không được** có whitespace giữa tên và mở ngoặc đơn, phía sau mở ngoặc đơn và phía trước đóng ngoặc đơn.

Trong danh sách argument thì **không được** có whitespace phía trước dấu phẩy, và **phải** có một whitespace phía sau dấu phẩy.
```php
<?php
bar();
$foo->bar($arg1);
Foo::bar($arg2, $arg3);
```

Danh sách argument **có thể** chia làm nhiều dòng, mỗi mỗi dòng **phải** là một argument.
Đóng ngoặc nhọn **phải** nằm ở một dòng riêng biệt.
```php
<?php
$foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
);
```

### 5. Control Structures
* **Phải** có một whitespace phía sau từ khóa cấu trúc điều khiển.
* **Không được** có whitespace nào trước và sau đóng mở ngoặc đơn.
* **Phải** có một whitespace ở giữa đóng ngoặc đơn và mở ngoặc nhọn.
* Thân nội dung **phải** thụt vào một lần.
* Đóng ngoặc nhọn **phải** nằm ở dòng kế tiếp nội dung.

#### 5.1 `if`, `elseif`, `else`
```php
<?php
if ($expr1) {
    // if body
} elseif ($expr2) {
    // elseif body
} else {
    // else body;
}
```
Từ khóa `else if` **nên** được thay bằng `elseif`

#### 5.2 `switch`, `case`
```php
<?php
switch ($expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
```

#### 5.3 `while`, `do while`
```php
<?php
while ($expr) {
    // structure body
}
```
```php
<?php
do {
    // structure body;
} while ($expr);
```

#### 5.4 `for`
```php
<?php
for ($i = 0; $i < 10; $i++) {
    // for body
}
```

#### 5.5 `foreach`
```php
<?php
foreach ($iterable as $key => $value) {
    // foreach body
}
```

#### 5.6 `try`, `catch`
```php
<?php
try {
    // try body
} catch (FirstExceptionType $e) {
    // catch body
} catch (OtherExceptionType $e) {
    // catch body
}
```
