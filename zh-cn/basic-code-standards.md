# 编码规范

> 文档内容主要来源于 [PSR-1](https://laravel-china.org/topics/2078/psr-specification-psr-1-basic-coding-specification) 和 [PSR-2](https://laravel-china.org/topics/2079/psr-specification-psr-2-coding-style-specification) ，并结合框架开发实践整理得出。

本文大部分内容直接复制 `PSR-4`，这么做的原因是因为使用的同学认真阅读本文内容，或者移步 `PSR-1` 和 `PST-4` 文档认真阅读并遵循编码规范。

## 编码

PHP代码 **必须** 且只可使用 `不带BOM的UTF-8` 编码。

## 命名方式

### namespace

命名空间以及类的命名必须遵循 [PSR-4](https://laravel-china.org/topics/2081/psr-specification-psr-4-automatic-loading-specification)。每个类为独立文件，且命名空间至少有一个层次：顶级的组织名称（vendor name）。

命名空间的声明应该紧挨 PHP 标签定义的下一行，声明后 **必须** 插入一个空白行。

示例（坏的）：
```php
<?php
/**
 * Created by PhpStorm.
 * User: xhb
 * Date: 2018-12-13
 * Time: 11:35
 */

namespace Vendor\Package;
```

示例（好的）：
```php
<?php
namespace Vendor\Package;
```

### use

所有 `use` 必须 在 `namespace` 后声明。每条 `use` 声明语句 必须 只有一个 `use` 关键词。并且 `use` 声明语句块后 **必须** 要有一个空白行。

示例：

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

// ... 更多的 PHP 代码在这里 ...
```

!> 在使用 `use` 引入各个类时，推荐根据类的用途给类加上对应的后缀，例如 `User` 命名为 `UserModel`，以增强代码可读性。

### 类命名

类的命名 **必须** 遵循 StudlyCaps 大写开头的驼峰命名规范。并且类名应当保持与文件相同的名称。

### 常量

所有的常量 **必须** 大写，词间以下划线分隔。

示例：

```php
<?php
namespace Vendor\Model;

class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
```

### 变量名

所有变量名 **必须** 遵循 properVar 小写开头的驼峰命名规范。

示例：

```php
<?php

$fooVar = '';
$ItemArrs = '';>
```

### 类、属性和方法

此处的「类」泛指所有的「class类」、「接口」以及「traits 可复用代码块」。

#### 扩展与继承

关键词 `extends` 和 `implements` **必须** 写在类名称的同一行。 类的开始花括号 **必须** 独占一行，结束花括号也 **必须** 在类主体后独占一行。

示例：

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements \ArrayAccess, \Countable
{
    // 这里面是常量、属性、类方法
}
```

implements 的继承列表也 **可以** 分成多行，这样的话，每个继承接口名称都 **必须** 分开独立成行，包括第一个。

示例：

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
    // 这里面是常量、属性、类方法
}
```

#### 属性

每个属性都 **必须** 添加访问修饰符。**一定不可** 使用关键字 `var` 声明一个属性。每条语句 **一定不可** 定义超过一个属性。**不该** 使用下划线作为前缀，来区分属性是 `protected` 或 `private`。

示例（坏的）：

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public $foo = null, $bar = null;

    private $_bar = null;
}
```

示例（好的）：

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public $foo = null;
    public $bar = null;

    private $bar = null;
}

```

#### 方法

所有方法都 **必须** 添加访问修饰符。**不该** 使用下划线作为前缀，来区分方法是 `protected` 或 `private`。方法名称后 **一定不可** 有空格符，其开始花括号 **必须** 独占一行，结束花括号也 **必须** 在方法主体后单独成一行。参数左括号后和右括号前 **一定不可** 有空格。一个标准的方法声明可参照以下范例，留意其括号、逗号、空格以及花括号的位置。

方法命名 **必须** 遵循 properVar 小写开头的驼峰命名规范。

示例：

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

##### 方法的参数

参数列表中，每个逗号后面 **必须** 要有一个空格，而逗号前面 **一定不可** 有空格。有默认值的参数，**必须** 放到参数列表的末尾。

示例：

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
        // 方法的内容
    }
}
```

##### abstract 、 final 、 以及 static

需要添加 `abstract` 或 `final` 声明时，**必须** 写在访问修饰符前，而 `static` 则 **必须** 写在其后。

示例：

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

#### 方法及函数调用

方法及函数调用时，方法名或函数名与参数左括号之间 **一定不可** 有空格，参数右括号前也 **一定不可** 有空格。每个参数前 **一定不可** 有空格，但其后 **必须** 有一个空格。

示例：

```php
<?php
bar();
$foo->bar($arg1);
Foo::bar($arg2, $arg3);
```

参数 **可以** 分列成多行，此时包括第一个参数在内的每个参数都 **必须** 单独成行。

示例：

```
<?php
$foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
);
```

#### 控制结构

控制结构的基本规范如下：

* 控制结构关键词后 **必须** 有一个空格。
* 左括号 ( 后 **一定不可** 有空格。
* 右括号 ) 前也 **一定不可** 有空格。
* 右括号 ) 与开始花括号 { 间 **必须** 有一个空格。
* 结构体主体 **必须** 要有一次缩进。
* 结束花括号 } **必须** 在结构体主体后单独成行。
* 每个结构体的主体都 **必须** 被包含在成对的花括号之中，
* 这能让结构体更加结构话，以及减少加入新行时，出错的可能性。

##### if 、elseif 和 else

标准的 `if` 结构如下代码所示，请留意「括号」、「空格」以及「花括号」的位置，注意 `else` 和 `elseif` 都与前面的结束花括号在同一行。

示例：

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

应该 使用关键词 `elseif` 代替所有 `else if` ，以使得所有的控制关键字都像是单独的一个词。

##### switch 和 case

标准的 `switch` 结构如下代码所示，留意括号、空格以及花括号的位置。`case` 语句 **必须** 相对 `switch` 进行一次缩进，而 `break` 语句以及 `case` 内的其它语句都 **必须** 相对 `case` 进行一次缩进。

如果存在非空的 `case` 直穿语句，主体里 **必须** 有类似 `// no break` 的注释。

示例：

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

##### while 和 do while

一个规范的 `while` 语句应该如下所示，注意其「括号」、「空格」以及「花括号」的位置。

示例：

```php
<?php
while ($expr) {
    // structure body
}
```

标准的 `do while` 语句如下所示，同样的，注意其「括号」、「空格」以及「花括号」的位置。

示例：

```php
<?php
do {
    // structure body;
} while ($expr);
```

##### for

标准的 `for` 语句如下所示，注意其「括号」、「空格」以及「花括号」的位置。

示例：

```php
<?php
for ($i = 0; $i < 10; $i++) {
    // for body
}
```

##### foreach

标准的 foreach 语句如下所示，注意其「括号」、「空格」以及「花括号」的位置。

示例：

```php
<?php
foreach ($iterable as $key => $value) {
    // foreach body
}
```

##### try, catch

标准的 `try catch` 语句如下所示，注意其「括号」、「空格」以及「花括号」的位置。

示例：

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

#### 闭包

闭包声明时，关键词 `function` 后以及关键词 `use` 的前后都 **必须** 要有一个空格。开始花括号 **必须** 写在声明的同一行，结束花括号 **必须** 紧跟主体结束的下一行。参数列表和变量列表的左括号后以及右括号前，**一定不可** 有空格。参数和变量列表中，逗号前 **一定不可** 有空格，而逗号后 **必须** 要有空格。闭包中有默认值的参数 **必须** 放到列表的后面。标准的闭包声明语句如下所示，注意其「括号」、「空格」以及「花括号」的位置。

示例：

```php
<?php
$closureWithArgs = function ($arg1, $arg2) {
    // body
};

$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // body
};
```
参数列表以及变量列表 **可以** 分成多行，这样，包括第一个在内的每个参数或变量都 **必须** 单独成行，而列表的右括号与闭包的开始花括号 **必须** 放在同一行。

示例：

```php
<?php
$longArgs_noVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) {
   // body
};

$noArgs_longVars = function () use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

$longArgs_longVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

$longArgs_shortVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use ($var1) {
   // body
};

$shortArgs_longVars = function ($arg) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};
```

注意，闭包被直接用作函数或方法调用的参数时，以上规则仍然适用。

示例：

```php
<?php
$foo->bar(
    $arg1,
    function ($arg2) use ($var1) {
        // body
    },
    $arg3
);
```
