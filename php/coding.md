
# 编码


> 编写一个php函数计算两个文件的相对路径

```php
function getRelativePath($fileA, $fileB) {

    $arrA = explode("/", $fileA); 
    $arrB = explode("/", $fileB); 
    array_pop($arrA);
    array_pop($arrB);

    $offset = 0;
    foreach($arrB as $key => $value) {
        if(!isset($arrA[$key]) || ($arrA[$key] != $arrB[$key])) {
            $offset = $key;
            break;
        }
    }

    $relativePath = '';

    for($i = $offset; $i <count($arrB); $i++) {
        $relativePath .= '../'; 
    }

    for($i=$offset; $i<count($arrA); $i++) { 
        $relativePath .= $arrA[$i].'/';
    }

    return $relativePath; 
}
```


> 用 PHP 打印出前一天的时间,格式是 `2015-05-20 22:21:21`

```php
echo date('Y-m-d H:i:s', date('U')-86400);
echo date('Y-m-d H:i:s', time()-86400);
echo date('Y-m-d H:i:s', strtotime('-1 day'));
```


> 不使用第三个变量,交换变量 a、b 的值

```php
list($a, $b) = array($b, $a);
```


> 写出单例模式和工厂模式的程序片段,并列出其中的注意点

```php
class Single {

    static $instance;

    private function __construct() {
    }

    private function __clone() {
    }

    public static function getInstance() {
        if (! (self::$instance instanceof self)) {
            self::$instance = new self();
        }
        return self::$instance;
    }
}


class Factory {

    public static function create($className) {
        $classFile = "./library/{$className}.class.php";
        if (! class_exists($className) && file_exists($classFile)) {
            require $classFile;
        }
        return new $className();
    }
}
```


> 用代码写出获取 url 文件后缀的方法,如 `http://www.baidu.com/foo/bar.php?id=value` 中.php 的值

```php
$url = 'http://www.baidu.com/foo/bar.php?id=value';
$path = parse_url($url, PHP_URL_PATH);
$ext = pathinfo($path, PATHINFO_EXTENSION);
```


> 用 php 写出获取中位数的方法

```php
$numList = array(
    1, 
    4, 
    3, 
    2, 
    5, 
    8, 
    7, 
    6, 
    9
);
// 先排序
$numList = sort($numList);

$count = count($numList);
$mid = 0;

if ($count % 2 == 0) {
    // 个数是偶数则取中间两个数的和除以 2
    $key1 = intval($count / 2) - 1;
    $key2 = intval($count / 2);
    $mid = ($numList[$key1] + $numList[$key2]) / 2;
} else {
    // 个数是奇数则取中间那个数
    $key = intval($count / 2);
    $mid = $numList[$key];
}

echo $mid;
```


> 一遍找出一个数组中最大的 2 个值

```php
$itemList = array(
    2, 
    4, 
    6, 
    3, 
    5, 
    12, 
    9, 
    19, 
    7, 
    8, 
    56, 
    34, 
    25, 
    78, 
    93, 
    35, 
    56, 
    24, 
    89, 
    44
);
$big1 = $big2 = 0;
foreach ($itemList as $item) {
    if ($item > $big1) {
        $big2 = $big1;
        $big1 = $item;
    }
}
var_dump($big1);
var_dump($big2);
```


> 多维数组排序

```php
$data = array(
    
    array(
        'volume' => 67, 
        'edition' => 2
    ), 
    array(
        'volume' => 86, 
        'edition' => 1
    ), 
    array(
        'volume' => 85, 
        'edition' => 6
    ), 
    array(
        'volume' => 98, 
        'edition' => 2
    ), 
    array(
        'volume' => 86, 
        'edition' => 6
    ), 
    array(
        'volume' => 67, 
        'edition' => 7
    )
);
// 取得列的列表
foreach ($data as $key => $row) {
    $volume[$key] = $row['volume'];
    $edition[$key] = $row['edition'];
}

// 将数据根据 volume 降序排列,根据 edition 升序排列, $data 作为最后一个参数,以通用键排序
array_multisort($volume, SORT_DESC, $edition, SORT_ASC, $data);

var_dump($data);
```


> 写出一个能创建多级目录的 PHP 函数

```php
function mkdirs($dir) {
    if (! is_dir($dir)) {
        if (! mkdirs(dirname($dir))) {
            return false;
        }
        if (! mkdir($dir, 0777)) {
            return false;
        }
    }
    return true;
}

function mkdirs2($str) {
    $arr = explode('/', $str);
    $path = '';
    foreach ($arr as $v) {
        $path .= $v . '/';
        if (! is_dir($path)) {
            mkdir($path);
        }
    }
}

mkdirs('dir1/dir2/dir3');
mkdirs2('dir4/dir5/dir6');

```

> 如何实现字符串翻转?

```php

$str = 'abc';

// 使用php内置函数
echo strrev($str);

// 循环输出
$length = strlen($str);
$revStr = '';

for ($i = $length - 1; $i >= 0; $i --) {
    $revStr .= $str{$i};
}
echo $revStr;

```


> 实现中文字串截取无乱码的方法

```php

当用 substr 截取中文字符会出现乱码,如果装了 mb 扩展, 用 mb_substr 截取就不会乱码


```


> 用 PHP 编写显示客户端IP 与服务器IP 的代码

```php
// 客户端IP:
echo $_SERVER[REMOTE_ADDR];
echo getenv('REMOTE_ADDR');

// 服务器IP:
if (isset($_SERVER['SERVER_ADDR'])) {
    $ip = $_SERVER['SERVER_ADDR'];
} else {
    $ip = $_SERVER['LOCAL_ADDR'];
}
```

> 如何修改 SESSION 的生存时间

```php
1、将 php.ini 中 session.gc_maxlifetime 设置为 9999(默认 为 1440)重启 apache 即可
2、代码中修改：
$savePath = "./session_save_dir/";
$lifeTime = 24 * 3600;
session_save_path($savePath);
session_set_cookie_params($lifeTime);
session_start();

3、setcookie() 或 session_set_cookie_params($lifeTime)

```


> 有一个网页(如：http://www.baidu.com/index.html），如何得到它的内容?

```php
$url = 'http://www.baidu.com/index.html';
echo file_get_contents($url);

```


> 在HTTP1.0中，状态码401的含义是? 如果返回“找不到文件”的提示，其语句为?

```php
状态值为 401,代表未被授权;

header('HTTP/1.1 401 Unauthorized');
header('status: 401 Unauthorized');

// 找不到文件
header('HTTP/1.1 404 Not Found');
header("status: 404 Not Found");

header('HTTP/1.1 301 Moved Permanently');
header('Location: http://www.9qc.com/');

```

> PHP中 heredoc 的用法

```php
heredoc 的语法是用"<<<"加上自己定义成对的标签,在标签范围內的 文字视为一个字符串：

$str = <<<EOF
I saw a dog yesterday.
EOF;

需要注意:
1、"<<<"后面的 EOF 是自定义的标签名称,必须要成对,最后要加上分号表示结束。
2、结束的标签前面最好不要有空格,以免发生错误!

```

> 请写一个函数验证电子邮件的格式是否正确

```php
function is_email($email) {
    return preg_match("/^[\w\-\.]+@[\w\-\.]+(\.\w+)+$/", $email);
}
```

> $_SERVER数组中有哪些有用的值？

```php
Array
(
    [SCRIPT_FILENAME] => /var/www/test/server.php
    [QUERY_STRING] => id=1&name=test
    [REQUEST_METHOD] => GET
    [SCRIPT_NAME] => /server.php
    [REQUEST_URI] => /server.php?id=1&name=test
    [SERVER_PROTOCOL] => HTTP/1.1
    [SERVER_SOFTWARE] => nginx/1.6.0
    [REMOTE_ADDR] => 127.0.0.1
    [REMOTE_PORT] => 56442
    [SERVER_ADDR] => 127.0.0.1
    [SERVER_PORT] => 80
    [SERVER_NAME] => test.com
    [REDIRECT_STATUS] => 200
    [HTTP_HOST] => test.com
    [HTTP_CONNECTION] => keep-alive
    [HTTP_CACHE_CONTROL] => max-age=0
    [HTTP_ACCEPT] => text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
    [HTTP_USER_AGENT] => Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2272.104 Safari/537.36
    [HTTP_ACCEPT_ENCODING] => gzip, deflate, sdch
    [HTTP_ACCEPT_LANGUAGE] => zh-CN,zh;q=0.8,en;q=0.6,zh-TW;q=0.4
    [PHP_SELF] => /server.php
    [REQUEST_TIME_FLOAT] => 1434974920.5889
    [REQUEST_TIME] => 1434974920
)
```

> 写出一些在 PHP 输出一段 HTML代码的办法

```php
1、echo 或 print等直接输出
2、require 或 include 包含一个 HTML 代码文件
3、模板文件等中：<?php if($showHtml) { ?> <p>I am html code. </p> <?php } ?>
```

> $userList = array('james', 'tom', 'symfony'); 请打印出 第一个元素的值；将所有值合并成用','号分隔的字符串输出

```php
echo $userList[0];
echo implode(",", $userList);
```

> $a = 'abcdef'; 请打印出$a的第一个字母

```php
echo $a{0};
```

> 请写出 PHP5 权限控制修饰符

```php
public protected private
```

> 请写出 php5 的构造函数和析构函数

```php
__construct __destruct
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
