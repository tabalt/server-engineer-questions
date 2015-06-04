
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

> 

```php

```


