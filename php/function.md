
# 函数


> echo(),print(),print_r(),var_dump()函数的区别

```php
echo：是PHP语句,语句是没有返回值的,而 print 和 print_r 是函数,函数可以有返回值。
print：只能打印出简单类型变量的值(如 int,string)
print_r：可以打印出复杂类型变量的值(如数组,对象)
echo：输出一个或者多个字符串
var_dump：可以打印出复杂类型变量的值和类型
```

> include 和 require 的区别是什么? 如何避免多次包含同一文件？

```php
1、PHP 程序执行到 require()时,只会读取一次档案,故常放在程序开头,档案引入后 PHP 会将网页档重新编译,让引入档成为原先网页 的一部分。
2、PHP 程序执行到 include()时,每次皆会读取档案,故常用于流 程控制的区段,如条件判断或循环中。
3、require() :如果文件不存在,会报出一个 fatal error.脚本停 止执行
4、include() : 如果文件不存在,会给出一个 warning,但脚本会 继续执行 
5、推荐使用require_once()和include_once(),可以检测文件是 否有重复包含。
```

> 

```php

```

> 

```php

```

> 

```php

```

> 

```php

```

> 

```php

```

> 

```php

```

> 

```php

```

> 

```php

```


