# TCL 模块

## `proc`

`proc name arguments body`

- 返回值是 return 语句的返回值
- 当没有 return 时，返回值是最后一个命令的返回值

``` tcl
# 定义默认值的方法
proc justdoit {a {b 1} {c -1}} {
    ...
}
```

``` tcl
proc example {first {second ""} args} { #; 定义变长参数的方法：注意最后一个变量名必须为 args
    if {$second eq ""} {
        puts "There is only one argument and it is: $first"
        return 1
    } else {
        if {$args eq ""} {
            puts "There are two arguments - $first and $second"
            return 2
        } else {
            puts "There are many arguments:\n$first and $second and $args"
            return "many"
        }
    }
}
```
