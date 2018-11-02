PSR-3: [Logger Interface](https://github.com/php-fig/log)
=========================================================
Tài liệu này mô tả một khuôn mẫu chung cho các thư viện ghi log.

Mục đích chính là cho phép thư viện nhận một đối tượng `Psr\Log\LoggerInterface` và ghi log vào nó một cách dễ dàng và bao quát.

### 1. Specification
#### 1.1 Basics
* `LoggerInterface` trình bày 8 phương thức để ghi log, ứng với 8 level:
  * **emergency**: hệ thống không thể sử dụng.
  * **alert**: hành động phải giải quyết ngay lập tức: sập trang web, database không sẵn sàng. 
  * **critical**: điều kiện quan trọng: thành phần của ứng dụng không sẵn sàng, lỗi bất ngờ.
  * **error**: lỗi trong quá trình chạy, không đòi phải giải quyết ngay lập tức, nhưng nên ghi lại và theo dõi.
  * **warning**: những exception xảy ra nhưng không phải lỗi: những cảnh báo về sử dụng.
  * **notice**: những việc bình thường nhưng có ý nghĩa.
  * **info**: những sự việc đáng quan tâm: user đăng nhập, log của SQL.
  * **debug**: những thông tin debug.
* Một phương thức thứ 9 - `log` - chấp nhận `log level` với đối số thứ đầu tiên.
Gọi phương thức này với một hằng số `log level` **phải** tương ứng với một trong 8 level trên kia.
Nếu một `log level` không được định nghĩa thì **phải** bung ra lỗi `Psr\Log\InvalidArgumentException` nếu không biết level nào cả.

#### 1.2 Message
* Mỗi phương thức chấp nhận một string ứng với message, hoặc object với phương thức `__toString()`.
`Implementors` **có thể** có những xử lý đặc biệt cho những object. Trường hợp khác, `implementors` **phải** chuyển sang một string.
* Message **có thể** chứa `placeholder` (giống [sprintf](http://php.net/manual/en/function.sprintf.php)) mà `implementors` **có thể** thay thế bằng `value` từ mảng `context`.

Tên của `placeholder` **phải** tương ứng với tên key trong mảng `context`.

Nó **phải** phân cách bởi mở và đóng ngoặc nhọn, **không được** có whitespace nào liền kề bên trong ngoặc nhọn.

Và **nên** chỉ dùng các ký tự `A-Z`, `a-z`, `0-9`, gạch chân `_`, và dấu chấm `.`.

`Implementors` **có thể** dùng `placeholders` để phiên dịch khi ghi log.

Sau đây là ví dụ của việc sử dụng `placeholder`:
```php
/**
 * Interpolates context values into the message placeholders.
 */
function interpolate($message, array $context = array())
{
    // build a replacement array with braces around the context keys
    $replace = array();
    foreach ($context as $key => $val) {
        $replace['{' . $key . '}'] = $val;
    }
    // interpolate replacement values into the message and return
    return strtr($message, $replace);
}

// a message with brace-delimited placeholder names
$message = "User {username} created";

// a context array of placeholder names => replacement values
$context = array('username' => 'bolivar');

// echoes "User bolivar created"
echo interpolate($message, $context);
```

#### 1.3 Context
* Mỗi phương thức chấp nhận một mảng `context`. Nó có nghĩa là giữ bất kỳ thông tin không liên quan nào trong một String.
`value` trong `context` thì không bung ra `exception` và cũng không chứa bất kỳ `error`, `warning` hay `notice` của PHP.
* Nếu một đối tượng `Exception` được truyền trong mảng `context` thì nó **phải** thuộc key `exception`.
Việc ghi log `exception` là một mẫu chuẩn và nó cho phép `implementors` đưa ra một `stack trace` của `exception` khi log của `backend` hỗ trợ nó.
`Implementors` vẫn **phải** xác minh rằng key `exception` thì thực sự chứa một `Exception` trước khi sử dụng, vì nó **có thể** chứa bất kỳ thứ gì.

#### 1.4 Helper classes and interfaces
* Class `Psr\Log\AbstractLogger` cho phép bạn implement từ `LoggerInterface` một cách dễ dàng, bằng cách kế thừa nó và implement phương thức `log`.
* Tương tự như vậy, sử dụng `Psr\Log\LoggerTrait` chỉ yêu cầu bạn implement  phương thức `log`.
* `Psr\Log\LoggerAwareInterface` chỉ chứa phương thức `setLogger(LoggerInterface $logger)` dùng để thay đổi thể hiện của logger.
* Trait `Psr\Log\LoggerAwareTrait` implement từ `Psr\Log\LoggerAwareInterface` và cho phép bạn lấy được `$this->logger`.
* Class `Psr\Log\LogLevel` chứa 8 constant định nghĩa 8 level log. 

### 2. Package
Các interface và class mô tả cũng như thích hợp với các class ngoại lệ, và 1 dãy test để xác minh rằng `implementation` của bạn là một phần của gói `psr/log`.
