# PHP 工具

## 字符串工具

下标从0开始。

mbstring模块提供字符串函数的`mb_`版本

### 长度

- `strlen(字符串)` 返回字符串占用的*字节*数
- `mb_strlen(字符串, 'UTF8')`  返回字符串的长度，输出8

### 检索

找不到返回false，否则返回下标

- 区分大小写检索 `strpos()`, `strrpos()` 注意不是C风格的`strchr()`或`strstr()`
- insensitive 不区分大小写 `stripos()`, `strripos()`

### 截取

`substr(字符串string, 起始位置start [, 截取长度length])`

- start若为负数，则从字符串结尾位置向前倒数第Start个字符开始
- string长度小于start则返回`FALSE`
- length若为负数，则string结尾处的length个字符会被省略（与Python中Slicing的右开区间保持一致）；若start不在剩余的字符串中则返回`FALSE`

示例

- `substr('abcdef', -1)` 返回`f`
- `substr('abcdef', 1, -2)` 返回`bcd`，注意不是`bcdf`

### 替换

`str_replace(搜索字符串needle, 替换字符串replace, 被寻找字符串haystack [, 计数count])` Replace needle with replace in heystack.

- `str_replace(',', '', '1,000,000')` 删除逗号
- `str_replace('red', 'black', '<font style="red">')` 替换红色为黑色

`substr_replace(目标字符串string, 替换字符串replace, 起始位置start [, 替换长度])`

- 替换长度为0：相当于插入
- 负数：倒数

### 清理空格或其他字符

`trim(目标字符串, 以字符串形式提供需要删除的字符)`, `ltrim()`, `rtrim()`

- `trim('abc12a3cd', 'a..z')` 注意是两个点，输出`12a3`

### 切分和组合字符串

- `explode(分隔符glue, 字符串str)` 字符串打散为数组，注意参数的顺序（这样设置可能是想强调两个参数都需要吧）
- `implode(数组)`, `implode(分隔符glue, 数组arr)` 数组聚合成字符串，注意参数的顺序使得与`explode()`对应，注意可以不设置分割符

### 转义与反转义

- `addslashes()`, `addcslashes()`, `stripslashes()`, `stripcslashes()`
- `quotemeta()` 将`.\+*?[^]($)`前加反斜线转义，转义在正则表达式中有特殊意义的字符

`addslashes()`用于加反斜线转义单引号、双引号、反斜线和空字符，`addcslashes()`可以在自定义的字符集之前添加反斜线转义

### 进制转换

- `bin2hex()`, `hex2bin()` 将**数据串** *（不是字符串）*转换成对应格式

如果需要转化二进制字符，可以

```php
$binary = '11111001';
$hex = dechex(bindec($binary));
echo $hex;
```

### 分割

- `chunk_split()` 指定字串长度打断字符（插入换行符），在结合`base64_encode($data)`等函数时比较有用
- `wordwrap()` 含有避免单词被打断的选项
- `str_split()` 分割字符串，不需要指定分割符的`explode()`
- `split()` 支持正则表达式的字符串分割

### 哈希

- `md5()`, `crc32()`, `sha1()`, `hash()`

### 格式工具：处理csv

- `str_getcsv()` 解析csv为一个数组

## HTML表单处理

全局变量 `$_GET`, `$_POST`, `$_REQUEST`(GET，POST和COOKIE)

文本框和文本域

```php
if (isset($_GET['name'])) {
    // ...
}
```

### HTML接口

键名由name属性决定

- 文本域 键由name属性决定，值由value属性决定
- 单选按钮Radiobutton 值由value属性设定
- 复选框Checkbox，值由value属性设定，name属性应该以“[]”结尾（使得PHP以数组方式解析，避免值覆盖的问题；注意PHP中的标识符不包括“[]”）。
- 下拉列表，值由option的内容设定

## HTTP Cookie

`setcookie(name, value, expire, path, domain, secure);`

- `setcookie("user", "Chloe", time()+7200, '''', 'yourdomain.com', 1);` 启用安全传输
- `setcookie("user", "", time()-3600);` 删除Cookie

## PHP Session

可以通过设置`session.auto_start`为1来自动启用Session

- 创建session `session_start()`
- 终结session `session_destroy()`

## 日期和时间

> 格林尼治时间1970年1月1日0时0分0秒

### 设定时区

PHP默认时区为格林尼治时间 GMT+0

投入生产环境前注意检查日期和时间设定

1. php.ini date.timezone Asia/Shanghai
2. `date_default_timezone_set("Asia/Shanghai")`

### 用于日期和时间的工具函数

- `time()` 返回自Unix纪元到当前时间的秒数
- `date(format [, timestamp])`
- `mktime(hour, minute, second, month, day, year)`
- `strtotime(string, now当前时间戳)` 将字符串解析为Unix时间戳
- `getdate(timestamp)` 获取包含日期信息的**数组**，获取日期字符串可以使用`date()`
- `checkdate(month, day, year)` 确认日期是否有效
- `strftime(format [, timestamp])` 输出指定格式的日期和时间

示例

- `date('Y-m-d H:i:s')` 2018-08-04 15:32:16
- `date('D', mktime(0, 0, 0, 8, 8, 2018))`
- `strtotime('next Monday')`, `strtotime(+1 week)`, `strtotime('now')`, `strtotime(2008.8.8)`

### 工具对象

- DateTime 常量定义了国际标准中使用的时间格式，如DateTime::COOKIE等；附加许多有用的方法。
- DateTimeImmutable 多数方法返回一个新的DateTimeImmutable对象，本身不会改变。
- DateTimeZone 时区相关运算
- DateInterval 表示一段时间，主要用于DateTime的add/sub/diff方法。
- DatePeriod 表示一组相同时间间隔的时间

获得2018年1月1日至2018年12月31日的每个星期五

```php
$start_date = new DateTime('2018-1-1');
$start_date->modify('next Friday');
$end_date = new DateTime('2018-12-31');
$interval = new DateInterval('P7D');  // 相隔7天

$date_period = new DatePeriod($start_date, $interval, $end_date);
foreach ($date_period as $date)
{
    echo $date->format('Y-m-d')."<br>";
}
```

## 文件和目录

文件资源

- `fopen(filename, mode)` mode: r, w, a, x, c;
- `feof(handle)`
- `fread(handle, length)`
- `fclose(handle)`
- `file_get_contents(handle)` 读入string
- `file_put_contents(handle, string [, mode])` mode: FILE_USE_INCLUDE_PATH, FILE_APPEND, LOCX_EX
- `file(handle [, flags])` 将文件读入数组 flags: FILE_USE_INCLUDE_PATH, FILE_IGNORE_NEW_LINES, FILE_SKIP_EMPTY_LINES

文件名

- `copy(src, dst)` 复制文件
- `unlink(filename)` 删除文件
- `is_file(filename)` 检查文件是否存在及正常（具有x权限）
- `stat(filename)` 返回关于文件的信息数组

目录操作

- `opendir(path)` 打开目录，返回目录资源
- `closedir(handle)`
- `readdir(handle)` 返回目录下的所有文件名
- `mkdir(filename [, mode [, recursive]])`, `rmdir(path)`

文件和目录

- `rename()` 重命名文件或目录
- `file_exists()` 检查文件或目录是否存在

### 国际化

主要由mb_string和intl完成国际化

- `mb_detect_encoding()`, `mb_check_encoding(字符串, 编码)` 检查字符串是否在指定的编码内有效, `mb_convert_encoding(字符串, 编码 [, 原编码（字符串或数组）])`
- `mb_parse_str()` 解析GET字符串并转换为数组
- `mb_strcut()` 按字节数截取字符串

intl

- Collator 比较字符串
- NumberFormatter 中文数字大小写转换
- IntlDateFormatter 中文日期和时间

### 面向对象方法 Directory类

<http://php.net/manual/zh/class.directory.php>


## 正则表达式

- int `preg_match(pattern, subject)` 搜索subject，如果搜索到返回1，否则返回0
- string `preg_repalce(pattern, replacement, subject)` 搜索subject中的匹配串，并用replacemnet代替所有匹配串
- array `preg_split(pattern, subject)` 以字符串集合形式返回匹配结果

### 规则

元字符包括：`^$[]\.|?*+()`

- `^head`, `tail$` 定义头部和尾部
- `.` 匹配除`\n`外的任何单个字符
- `[]` 匹配指定范围内单个字符，匹配范围形如`aeiou`, `a-z`
- `|` 或操作 在多项之间选择一个进行操作 `(a|e|i|o|u|oo)`
- `\` 转义
- `()` 标记子表达式的开始位置和结束位置
- `*` 匹配左边的子表达式0次或多次
- `+` 匹配左边的子表达式至少1次
- `?` 匹配左边的子表达式0次或1次
- `{a,b}` 匹配左边的子表达式[a,b]次，如果b省略则是∞

### 修正符

PHP还有自己的一套修正符可以使用。

## 数据库

### Mysqli

- `new mysqli(host, usrname, pwd, dbname, port)`, `mysqli::close()`
- `select_db(dbname)`
- `query(sql)`
- `error` 错误信息

结果集

- 使用数字索引数组或关联索引数组均可访问
- `num_rows`
- `fetch_row()`

```php
while ($row = $result->fetch_row())
{
    // body
}
```

### RedBeanPHP

零配置ORM（对象关系管理）类库，兼容MySQL和SQLite等

CRUD：Create, retrieve, update, delete
