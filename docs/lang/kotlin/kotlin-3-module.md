# Kotlin 模块

## 函数

``` kotlin
fun functionName(arg0: ArgType): ReturnType {
    return something;
}
```

## 类

``` kotlin
class Customer                                  // 1

class Contact(val id: Int, var email: String)   // 2

fun main() {

    val customer = Customer()                   // 3

    val contact = Contact(1, "mary@gmail.com")  // 4

    println(contact.id)                         // 5
    contact.email = "jane@gmail.com"            // 6
}
```
