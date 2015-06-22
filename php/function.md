
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

> 请说明 php 中传值与传引用的区别。什么时候传值什么时候传引用?

```php
Call by value (传值): 函数范围内对值的任何改变在函数外部都会被忽略。调用方式:函数名(参数 1,参数 2);
Call by address (传引用): 函数范围内对值的任何改变在函数外部也能反映出这些修改。调用方式:函数名(&参数 1,&参数 2);
优缺点: 按值传递时,php必须复制值。对于大型字符串和对象来说,这样做代价很大。按引用传递则不需要复制值,对于性能提高有好处。
```

> PHP中 error_reporting 这个函数有什么作用？

```php
error_reporting() 用来配置错误信息汇报的等级。

相关用法：
error_reporting(0);
ini_set('error_reporting', E_ALL);
```

> 检测一个变量是否有设置的函数是? 是否为空的函数是?

```php
isset($a)
empty($a)
```

> 下面哪个函数可以打开一个文件，以对文件进行读和写操作：
a) fget()  (b) file_open()  (c) fopen()  (d) open_file()

```php
(c) fopen 打开文件，供读写操作
```

> PHP中mysql_fetch_row() 和 mysql_fetch_array() 有什么区别?

```
mysql_fetch_row (resource $result) ：从结果集中取得一行作为枚举数组 
mysql_fetch_array(resource $result [, int $ result_type]) ：
从结果集中取一行作为关联数组(MYSQL_ASSOC),或数字数组(MYSQL_ASSOC),或二者兼有(MYSQL_BOTH)
```

> 取得查询结果集总数的函数是?

```php
mysql_num_rows($resource);
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


