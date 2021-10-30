# TCL 工具

## 输入输出工具

### `puts`

``` tcl
puts What

puts -nonewline Hello,
puts World.
```

### `gets`

`gets ?channelId? ?varName?`

## 字符串工具

- `string length str`
- `string index str i`
- `string range str first last`

### Glob 风格匹配 `match`

``` tcl
# Matches
string match f* foo

# Matches
string match f?? foo

# Doesn't match
string match f foo

# Returns a big list of files on my Debian system.
set bins [glob /usr/bin/*]
```

### 字符串比较

- `string compare string1 string2`
  - -1 如果 string1 比 string2 小
  - 0
  - 1
- `string first string1 string2`
- `string last string1 string2`
- `string wordstart str i` 返回下标i这个字符所在的单词的开始位置的下标。
- `string wordend str i`
- `string match pattern str` glob 匹配

#### 字符串修改

- `string tolower str`
- `string toupper str`
- `string trim str ?trimChars?`
- `string trimleft str ?trimChars?`
- `string trimright str ?trimChars?`

#### 字符串格式化 `format`

与 C `printf` 类似。

``` tcl
set labels [format "%-20s %+10s " "Item" "Cost"]
set price1 [format "%-20s %10d Cents Each" "Tomatoes" "30"]
set price2 [format "%-20s %10d Cents Each" "Peppers" "20"]
set price3 [format "%-20s %10d Cents Each" "Onions" "10"]
set price4 [format "%-20s %10.2f per Lb." "Steak" "3.59997"]

puts "\nExample of format:\n"
puts "$labels"
puts "$price1"
puts "$price2"
puts "$price3"
puts "$price4"

# Item                       Cost
# Tomatoes                     30 Cents Each
# Peppers                      20 Cents Each
# Onions                       10 Cents Each
# Steak                      3.60 per Lb.
```

## 正则表达式

参考<https://wiki.tcl-lang.org/page/Tcl+Tutorial+Lesson+20>。

- `^` Matches the beginning of a string
- `$` Matches the end of a string
- `.` Matches any single character
- `*` Matches any count (0-n) of the previous character
- `+` Matches any count, but at least 1 of the previous character
- `[...]` Matches any character of a set of characters
- `[^...]` Matches any character *NOT* a member of the set of characters following - the ^.
- `(...)` groups a set of characer into a subSpec

- `regexp ?switches? exp string ?matchVar? ?subMatch1 ... subMatchN?` Searches string for the regular expression exp. If a parameter matchVar is given, then the substring that matches the regular expression is copied to matchVar. If subMatchN variables exist, then the parenthetical parts of the matching string are copied to the subMatch variables, working from left to right.
- `regsub ?switches? exp string subSpec varName` Searches string for substrings that match the regular expression exp and replaces them with subSpec. The resulting string is copied into varName.

``` tcl
set sample "Where there is a will, There is a way."

#
# Match the first substring with lowercase letters only
#
set result [regexp {[a-z]+} $sample match]
puts "Result: $result match: $match"
# Result: 1 match: here

#
# Match the first two words, the first one allows uppercase
set result [regexp {([A-Za-z]+) +([a-z]+)} $sample match sub1 sub2 ]
puts "Result: $result Match: $match 1: $sub1 2: $sub2"
# Result: 1 Match: Where there 1: Where 2: there

#
# Replace a word
#
regsub "way" $sample "lawsuit" sample2
puts "New: $sample2"
# New: Where there is a will, There is a lawsuit.

#
# Use the -all option to count the number of "words"
#
puts "Number of words: [regexp -all {[^ ]+} $sample]"
# Number of words: 9
```

## 进阶数据结构

## 操作系统接口

- `open`
- `exec`

## 解释器元信息

``` tcl
info exists varName
```
