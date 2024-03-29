# C++ 模块

## 函数

### 函数参数与临时变量、引用参数和const

仅当参数为const引用时，才不生成临时变量。

## 函数模板

```cpp
template <typename T>
void swap(T &a, T &b) { };
```

实例化是编译器为函数模板生成具体代码的过程，具体化是编写函数模板的过程。

显式实例化在函数原型声明中以`template`修饰，显示具体化在函数原型中以`template<>`修饰。

显式具体化和显式实例化

```cpp
// 非模板形式
void swap(job &a, job &b) { };

// 模板形式
template <typename T>
void swap(T &a, T &b) { };

// 显式具体化形式
template <> void swap(job &a, job &b) { };
template <> void swap<job>(job &a, job &b) { };

// 显式实例化声明
template void swap<int> (int, int);
```

编译器确认可行函数的过程：完全匹配和最佳匹配、提升转换、标准转换、用户定义转换。“最具体”指找到可行函数需要的转换最少。

### `decltype`

用于确认变量的类型：

```cpp

template <typename T1, typename T2>
void ft(T1 x, T2 y)
{
    decltype(x+y) xpy = x + y;
}
```

结合后置返回类型声明函数的返回类型：

```cpp

template <typename T1, typename T2>
auto h(T1 x, T2 y) -> decltype(x + y)
{
    /* 函数体 */
};

```

### `decltype`确认类型的顺序

1. 对于没有使用括号的标识符，与标识符的类型相同
2. 对于函数调用，与函数的返回值类型相同
3. 对于左值，为指向其类型的引用
4. 对于表达式，与表达式的类型相同

```cpp
double xx;
decltype((xx)) w; // double &
decltype(xx)   u; // dooble
```

## 储存类

### 存储持续性

- 自动储存持续性
- 静态存储持续性 自动默认初始化为0（零初始化）
- 线程存储持续性 thread_local
- 动态存储持续性 new/delete

编译期间执行常量表达式初始化，运行期间执行动态初始化。

### 作用域与链接性

内部链接性在翻译单元内共享，外部链接性在翻译单元之间共享，无链接性为局部变量

- 文件作用域
- 函数原型作用域

### `register`

显式地指明变量的储存性是自动的。

### `extern`

单定义规则 在多个文件中使用到外部变量的情况下，只需在一个文件中包含该变量的定义，但在其他文件中要使用extern关键字来声明它。

### `static`

修饰变量时，在文件作用域中表示内部链接性，在局部声明中表示静态储存持续性。

修饰函数时，可将函数的链接性设置为内部；静态函数将覆盖外部定义。

### `const`

在全局变量中，用const修饰，等同于用const static进行修饰，表示内部连续性。

使用extern关键字修饰const表示外部连续性，此时所有用到该变量的翻译单元都必须使用extern关键字标记，同时只有一个文件可对其初始化。

### 其他关键字

- *cv-限定符* const和volatile
- *mutable* 即使一个结构或类是const的，某个成员也可以被修改

`mutable`的示例

```cpp
struct K
{
    mutable int i = 12;
    int x = 12;
};

int main()
{
    const K k;
    k.i = 32;  // 可行
    k.x = 43;  // 不可行
}
```

### 语言链接性

C语言链接性

```cpp
extern "C" void spaff(int);
```

C++语言链接性

```cpp
extern void spaff(int);
extern "C++" void spaff(int);
```

## 类

### 类的内联函数

注意到定义于类声明中的函数都成为内联函数，也可以在类声明之外定义成员函数，使之成为内联函数，只需要有一处`inline`标记。

```cpp
class Stock
{
private:
    void set_tot();
}

inline void Stock::set_tot()
{
    ...
}
```

### 构造函数和析构函数

- **explicit** 禁用构造器形参的隐式类型转换

```cpp
Stock stock("Nano Element", 2, 3);
Stock stock = ("Nano Element", 2, 3);  // 可能会创建临时变量
Stock stock {"Nano Element", 2, 3};
```

可以使用列表初始化；

可以利用`std::initialize_list`实现任意长度的初始化列表。

### 类作用域

像下面这样定义常量是不可行的，因为类的定义只是描述了对象的形式，并没有创建对象，也就没有存放值的空间。

```cpp
class Backery
{
private:
    const int Months = 12;
    double cost[Months];
}
```

做法是为类声明一个枚举类型，或者使用static来修饰

```cpp
class Backery
{
private:
    enum {Month = 12}; // 并不会创建类数据成员，即对象实例中不包含枚举
    double cost[Months];
}
```

```cpp
class Backery
{
private:
    static const int Months = 12;
    double cost[Months];
}
```

利用**作用域内枚举**，或称**强类型枚举**可以防止名称冲突

```cpp
// 可能产生名称冲突
enum egg {Small, Medium, Large, Jumbo};
enum t_shirt { Small, Medium, Large, Jumbo};

// 下列枚举的作用域为类
enum class egg {Small, Medium, Large, Jumbo};
enum struct t_shirt {Small, Medium, Large, Jumbo};  // 此处class关键子与struct关键字是等效的

egg choice = egg::Small;
```

传统枚举值可以隐式转换为整型，而作用域类枚举不能隐式转换为整型，亦无法与整数比较，可指定底层枚举类型。

```cpp
enum class : short pizza { Small, Medium, Large, XLarge };
```

### 运算符重载

```cpp
class Time
{
public:
    Time opearator +(const Time&) const;
}


Time opearator +(double, const Time&) const;
```

1. 重载后的运算符至少有一个是用户定义的操作类型
2. 重载运算符不会改变结合性和优先级
3. 只能重载现有运算符
4. 不能重载sizeof运算符、成员运算符、成员指针运算符、作用域解析运算符、三元条件运算符、RTTI运算符以及强制类型转换运算符
5. 下列运算符只能通过成员函数重载：赋值运算符、函数调用运算符、下标运算符、通过指针访问类成员的运算符（->）

重载运算符需要小心二义性。

注意重载自增操作符时，默认重载的是前缀自增操作符，重载后缀自增操作符需要使用`Type& operator ++(int)`形式的声明。

### 友元

友元函数、友元类、友元成员函数

重载二元运算符常常需要友元

### 创建友元函数

1. 将函数放置在类声明中，并使用*friend*修饰
2. 定义函数时，不使用*friend*修饰

即使友元函数在类中声明，但它不是类成员函数，不能通过成员运算符来调用。即使友元函数不是成员函数，但它与成员函数的访问权限相同。

只要在类外访问类的私有数据，就需要友元。

### 类的自动转换和强制类型转换

自动转换在不兼容的类型中不发生。

1. **由其他类型转换**：接受一个参数的构造函数可以作为转换函数。*explicit*可以用于指定显式强制类型转换。
2. **转换成其他类型**：`operator int()` `operator double()` *explicit*可以用于指定显式强制类型转换。

### 类成员静态函数

this指针无效，可以使用类名访问，也可以使用对象访问。

### 类和动态内存分配

> “开始时还是正常的，但逐渐变得异常，最终导致了灾难性的后果。”

不能在类中初始化静态成员变量（声明只是描述如何分配内存，但不分配内存）；静态数据成员为const整型或枚举型除外。

### 特殊成员函数

1. 默认构造函数 `Time() = default;`
2. 默认析构函数
3. 复制构造函数 `Time(const Time &);` 逐个复制数据成员
4. 赋值运算符
5. 地址运算符

静态类成员函数，不能通过对象进行调用。

### 在构造函数中使用new

如果使用new来初始化指针成员，则应该在析构函数中使用delete；new和delete必须相互兼容

### 返回对象

编程陷阱预防：返回const对象

```cpp
// 如果为force的类型定义了operator +()
net = force1 + force2;
force1 + force2 = net;
```

### 定位`new`运算符

定位new运算符不能与常规delete运算符配合使用，
从而删除对象时需要显式调用对象的析构函数。

### 嵌套声明

在类中嵌套结构或类声明，可以使作用域仅限于类中。

### 成员初始化列表和类内初始化

类中定义的const常量，可以初始化，但不能给它赋值。

只有构造函数可以使用成员初始化列表语法。

使用成员初始化列表的例子：

```cpp
Queue::Queue(int qs) : qsize(qs) {
    front = rear = NULL;
    items = 0;
}
```

成员初始化列表初始化的对象不仅仅限于常量；但常量和被声明为引用的类成员也必须使用成员初始化语法。

C++11的类内初始化允许初始化以更直观的形式初始化：

```cpp
class Classy
{
    int mem1 = 10;
    const int mem2 = 20;
}
```

## 类继承

### 派生

派生类需要添加自己的构造函数。

创建派生类对象之前，首先创建基类对象。创建的过程如同烙饼需要从里层开始。在派生类的构造函数中，如果不调用基类的构造函数，程序使用基类默认构造函数。派生类构造函数中通过成员初始化列表将必要参数传递给基类构造函数。

析构对象的顺序与创建对象的顺序相反，先析构派生类对象，再析构基类对象，如同吃烙饼从外层吃起。析构函数的调用是自动的。

派生类对象可以使用基类的非私有方法。可以使用作用域解析运算符指定执行的方法。

基类指针或引用可以不进行显式类型转换而指向或是引用派生类对象。也就是说可以利用基类指针数组方便地管理基类和派生类。将派生类指针或引用转换为基类指针或引用称为**向上强制转换（upcasting）**，在共有继承关系中无需显式类型转换，相反的过程称为**向下强制转换**，需要显式类型转换。

### 虚方法

如果不使用`virtual`，程序根据引用类型或者指针类型选择方法；如果使用`virtual`，根据引用或指针指向的对象的具体类型来选择方法。

方法在基类中被声明为`virtual`，在派生类中自动生成为虚方法。

`virtual`只用于类声明的定义中，而没有用于方法定义中。

`virtual`方法和基类指针/引用的特性，使得创建一个基类指针数组来管理基类和派生类对象十分方便。

建议析构函数声明为虚函数：除非类不用于基类。如果析构函数不是虚函数，则只调用对应于指针类型的析构函数。如果析构函数是虚的，将调用对应类型的析构函数，并自动调用基类对象的析构函数。

有关虚函数的注意事项：

1. **构造函数** 不能是虚函数，定义为虚函数没有任何意义。
2. **析构函数** 工程上必须是虚函数。通常应该给基类提供一个虚析构函数，即使它不需要析构函数。
3. **友元不会是虚函数** 因为友元不是成员函数。只有成员函数可以成为虚函数。
4. **如果没有重新定义** 如果在派生类中没有重新定义虚函数，则使用该函数的基类版本。
5. **重新定义将隐藏同名的所有基类函数** 重新定义继承的方法不是重载，无论参数列表是否相同，该操作将隐藏所有同名的基类方法。经验方法：一、如果重新定义继承的方法，则应确保与原函数的类型相同；如果返回类型是基类引用或者指针，则可以修改为指向派生类的引用或指针，称为“返回类型协变”。此例外仅适用于返回值，不适用于参数。二、如果基类声明被重载了，则应该在派生类中重新定义所有基类版本。

### 静态联编和动态联编

- **函数名联编（binding）** 将源代码中的函数调用解析为具体的函数代码块。
- **静态联编/早期联编（static binding / early binding）** 在编译期间进行的联编。
- **动态联编/晚期联编（dynamic binding / late binding）** 在运行时选择正确的虚方法。

### 抽象基类

纯虚函数：未实现的函数。

```cpp
class BaseEllipse
{
public:
    virtual double Area() const = 0; // 纯虚函数定义
}
```

当类的生命包含纯虚函数时，不能创建该类的对象。纯虚函数可以有定义，因为所有派生类的方法可以与基类一致，则可以在基类中统一定义。

### 继承和动态内存分配

派生类不使用new，不需要为派生类定义构造函数、析构函数或复制构造函数。

派生类中使用new，需要为派生类定义构造函数、析构函数和赋值构造函数。在复制构造函数中，可以使用语法`Base::operator =(hs)`

### 派生类型

- **公有继承** 基类的公有成员成为派生类的公有成员，保护成员成为派生类的保护成员，只能通过基类接口访问私有成员，能够隐式向上转换。
- **保护继承** 基类的公有成员和私有成员成为派生类的保护成员，只能通过基类接口访问基类私有成员。只能在派生类中隐式向上转换。
- **私有继承** 基类的公有成员和保护成员成为派生类中的私有成员，只能通过基类接口访问基类私有成员，不能隐式向上转换。

### using重新定义访问权限

使用保护继承和私有继承时，若要让基类的方法在派生类外可用，可以在派生类的公有部分添加声明：

```cpp
class  MyClass : private BaseClass {
public:
    using BaseClass::min;
    ...
}
```

## 多重继承

注意需要使用public修饰符限定每一个基类。

多重继承带来的问题是：从不同的基类中继承同名方法，从相关基类中继承同一个类的多个实例。

### 有多个实例

使用类型转换来指定要使用的对象。

```cpp
Worker * pw1 = (Waiter *) &ed; // the Worker in the Waiter
Worker * pw2 = (Singer *) &ed; // the Worker in the Singer
```

### 虚基类

使用Virtual关键字使从多个基类相同的类中派生时，只继承一个基类对象。

```cpp
class Singer : virtual public Worker {... };
class Waiter : virtual public Worker {... };

class SingerWaiter : public Singer, public Waiter {... };

```

使用虚基类要求在必要时显式地调用公有基类的构造函数，自动信息传递不起作用。因为自动传递信息时从两条路径传递到基类。这样的语法对于非虚基类是非法的，但对于虚基类则必须这样做。

```cpp
// 不合法的
SingerWaiter(const Worker &wk, int p = 0, int v = Singer::other)
                : Waiter(wk, p), Singer(wk, v) { };

// 合法的
SingerWaiter(const Worker &wk, int p = 0, int v = Singer::other)
                : Worker(wk), Waiter(wk, p), Singer(wk, v) { };
```

### 有多个方法

使用作用域解析操作符澄清名称引用。

```cpp
newhire.Worker::show();
```

## 类模板

```cpp
template <class T>
class Stack
{
    // details omitted
}

template <class T>
Stack<T>::Stack() {
    // details omitted
}

template <class T>
Stack<T>::function(int arg1) {  // 在类外需要使用完整的类型声明
    // details omitted
}
```

注意模板必须与特定的模板实例化请求一起使用，
最通用的办法是将模板的信息放置在一个头文件`hpp`中（定义与实现不要分离）。

在工程实践中也可以分离定义，前提是要求将使用到的模板显式实例化。

### 非类型参数

非类型参数（或称表达式参数）可以是整型、枚举、引用或者指针。

```cpp
template <class T, int n>
class Array {
private:
    T ar[n];

    // ...
};

template <class T, int n>
T& Array<T,n>::function() {
    // ...
}
```

### 模板多功能性

#### 递归使用模板

`Array<ArrayK<int, 5>, 10> twodee;`

#### 使用多个类型参数

`template <class T1, class T2> ...`

#### 默认类型模板参数

`template <class T, class T2 = int> class Typo {..};`

### 模板的具体化

1. **隐式实例化**
2. **显式实例化**
3. **显式具体化**

## 名称空间

区分声明区域，潜在作用域和作用域。

命名空间可以是全局的，也可以从属于另一个命名空间。

命名空间是开放的。任何人都可以往名称空间中加入新的内容。

区分未限定的名称和限定的名称。

### `using`

```cpp
using Jill::fetch;     // using声明
using namespace std;   // using编译指令
```

若使用using声明，局部名称将隐藏全局名称，但仍可使用作用域解析操作符。

using编译指令是可传递的。

可以**通过使用未命名的名称空间**来实现链接性为内部的静态变量。未命名的名称空间于全局变量类似，但不能使用using声明或using编译指令使它在其他位置可用。

例如，

```cpp
static int counts;
int other();

int main() {};
int other() {};
```

它采用命名空间的实现如下

```cpp
namespace
{
    int counts;
}
int other();

int main() {};
int other() {};
```

### 内联名称空间

自动将内层的标识符放至外层作用域

```cpp
namespace X
{
    inline namespace Y
    {
        void foo();
    }  // namespace Y
}  // namespace X
```

一个利用内联名称空间实现的实用的功能如下

```cpp
// V98.h
namespace V98
{
    void f();  // 实现基本功能
}

// V99.h
inline namespace V99
{
    void f();  // 改良实现
}

// Mine.h
namespace Mine
{
#include "V98.h"
#include "V99.h"
}

// main.cpp
#include "Mine.h"
using namespace Mine;

int main()
{
    f();  // 默认版本，V99版
    V98::f();  // V98版
    V99::f();  // 可以通过完整方式访问
}
```
