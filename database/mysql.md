
# MySQL


> MySQL 数据库的优化方法

```
1. 选取最适用的字段属性,应该尽量把字段设置为 NOT NULL,在执行查询的时候不用比较 NULL 值。 
2. 使用连接(JOIN)来代替子查询(Sub-Queries) 
3 .使用联合(UNION)来代替手动创建的临时表
4 .尽量少使用 LIKE 关键字和通配符
5 .使用事务和外键

```

> MYSQL取得当前时间的函数和格式化日期的函数是？

```
now()
date_format( date, format )
```

> 数据表members有这些字段：id,username,posts,pass,email，写出发帖数最多的十个人的名字：

```sql
SELECT `username` FROM `members` ORDER BY `posts` DESC LIMIT 0,10;

```

> 请写出数据类型(int char varchar datetime text)的意思; 其中 varchar 和 char 有什么区别？

```
int 整数类型 
char 固定长度字符串 
varchar 可变长字符串 
datetime 日期时间型 
text 字符字符串

char 列的长度固定为创建表时声明的长度, varchar 列中的值为可变长字符串.
```

> MySQL自增类型(通常为表ID字段)必需将其设为(?)字段

```
AUTO_INCREMENT
```

> 有一个用户表(User)结构如下，使用 php 查出所有姓名为“张三”的内容并打印出来：

| Name | Tel | Content | Date |
|:-----:|:--------|:-------|:-------|
| 张三 | 13333663366 | 大专毕业 | 2006-10-11 |
| 张三 | 13612312331 | 本科毕业 | 2007-01-15 |
| 李四 | 02155665566 | 中专毕业 | 2008-02-16 |

```php
$link = mysql_connect("localhost", "root", "") or die('Could not connect: ' . mysql_error());
mysql_select_db("db_name", $link) or die ('Can\'t use db_name : ' . mysql_error());

$result = mysql_query("SELECT * FROM `User` WHERE `Name` = '张三'; ", $link);
while ( $row = mysql_fetch_array($result, MYSQL_ASSOC) ) {
    echo "{$row['Name']},{$row['Tel']},{$row['Content']},{$row['Date']}\n";
}

mysql_close($link);
```

> 针对上述用户表，写出实现以下功能的SQL语句：

1、添加用户(王五 13254748547 高中毕业 2009-03-17)：

```
INSERT INTO `User`(`Name`,`Tel`,`Content`,`Date`) VALUES ('小王','13254748547','高中毕业','2007-05-06');
```

2、 修改张三的时间为当前系统时间：
```
UPDATE `User` SET `Date` = DATE_FORMAT(NOW(),'%Y-%m-%d') WHERE `Name` = '张三';
```

3、 写出删除名为李四的全部记录：

```
DELETE FROM `User` WHERE `Name` = '李四';
```

> 新闻发布系统相关数据库操作

1、名为 article 的表有这些字段：（id：文章id，title：文章标题，content：文章内容，category_id：文章分类id，hits：点击量 ）；写出建表语句：

```
CREATE TABLE `article`(
    'id' int(11) NOT NULL AUTO_INCREMENT,
    'title' varchar(200) NOT NULL DEFAULT '',
    'content' TEXT(500),
    'category_id' int(11) NOT NULL,
    'hits' int(11) NOT NULL DEFAULT 0,
    PRIMARY KEY('id')
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

2、表comment记录用户评论内容，字段有：（id：评论id，article_id：文章id 关联article表中的id，content ：评论内容）；编写SQL语句：查询字段列表（文章 id 文章标题 点击量 回复数量）, 按照回复数量排序，最高的排在最前，没有回复则显示为0。

```
SELECT article.id as id, article.title as title, IF(article.`hits` IS NULL,0,article.`hits`) as hits,IF(comment.`id` is NULL,0,count(*)) number FROM article 
LEFT JOIN comment ON article.id=comment.article_id GROUP BY article.`id` ORDER BY number DESC;
```

3、表 category 保存分类信息,字段如下 id int(4) not null auto_increment; name varchar(40) not null; 用户输入文章时,通过选择下拉菜单选定文章分类，写出如何实现这个下拉菜单

```
$result = mysql_query("select id, name from category") or die("Invalid query: " . mysql_error());

echo '<select name="category_id">';
while ( $row = mysql_fetch_array($result) ) {
    echo ("<option value=\"{$row['id']}\">{$row['name']}</option>");
}
echo '</select>';
```

> 

```

```

> 

```

```

> 

```

```


