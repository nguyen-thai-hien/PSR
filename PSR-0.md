PSR-0 Autoloading standard
==========================
_Kể từ 2014-10-21 [PSR-0](https://github.com/gr-hien/PSR/blob/master/PSR-0.md) bị phản đối (~~deprecated~~), [PSR-4](https://github.com/gr-hien/PSR/blob/master/PSR-4.md) đang được khuyến nghị như thay thế._

### Mandatory
* Một namespace đầy đủ **phải** tuân theo cấu trúc `\<Vendor Name>\(<Namespace>\)*<Class Name>`.
* Mỗi namespace **phải** có một top-level ("Vendor Name").
* Mỗi namespace **có thể** có nhiều sub-namespace.
* Mỗi phân cách namespace được chuyển sang `DIRECTORY_SEPARATOR` khi load lên.
* mỗi ký tự `_` trong CLASS NAME chuyển qua `DIRECTORY_SEPARATOR`. Ký tự `_` không có ý nghĩa đặc biệt trong namespace.
* Namespace đầy đủ và class là hậu tố với `.php` khi load lên.
* Chữ cái trong `vendor name`, `namespaces` và `class names` **có thể** là sự kết hợp của chữ viết thường và viết hoa.

### Examples
* `\Doctrine\Common\IsolatedClassLoader` => `/path/to/project/lib/vendor/Doctrine/Common/IsolatedClassLoader.php`
* `\Symfony\Core\Request` => `/path/to/project/lib/vendor/Symfony/Core/Request.php`
* `\Zend\Acl` => `/path/to/project/lib/vendor/Zend/Acl.php`
* `\Zend\Mail\Message` => `/path/to/project/lib/vendor/Zend/Mail/Message.php`

### Underscores in Namespaces and Class Names
* `\namespace\package\Class_Name` => `/path/to/project/lib/vendor/namespace/package/Class/Name.php`
* `\namespace\package_name\Class_Name` => `/path/to/project/lib/vendor/namespace/package_name/Class/Name.php`

### Example Implementation
Bên dưới là một ví dụ đơn giản về autoloading:
```php
<?php

function autoload($className)
{
	$className = ltrim($className, '\\');
	$fileName  = '';
	$namespace = '';
	if ($lastNsPos = strrpos($className, '\\')) {
		$namespace = substr($className, 0, $lastNsPos);
		$className = substr($className, $lastNsPos + 1);
		$fileName  = str_replace('\\', DIRECTORY_SEPARATOR, $namespace) . DIRECTORY_SEPARATOR;
	}
	$fileName .= str_replace('_', DIRECTORY_SEPARATOR, $className) . '.php';

	require $fileName;
}
spl_autoload_register('autoload');
```
### [SplClassLoader](https://gist.github.com/jwage/221634)
