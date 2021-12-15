# GD Script

调用顺序：

- `_init` 实例化
- `_enter_tree()` 当前节点进入场景树（当前结点的子节点尚未进入）
- `_ready` 当前节点和子节点进入场景
- `_process` 图像帧
- `_physical_process` 恒定速率的物理帧
- `_on_NodeName_signalName`

``` gd
func ready():
    add_to_group("enemies")
    $Button # 相当于 get_node("Button")
    get_node("Button").connect("pressed", self, "_on_Button_pressed")
    get_node("Label").text = "Hello!"

    get_viewport_rect()
```

## 类型

``` gd
var a = 1
var a = "123"

var typed_var: int = 3

var inferred_type := 4

enum { UNIT_ONE, UNIT_TWO, UNIT_THREE}
enum Named { ONE, TWO, THREE }
```

## `for`

``` gd
for i in 3:
    # `for i in range(3)`

for i in 2.2:
    # `for i in range(ceil(2.2))`
```

可以[自定义迭代器](https://docs.godotengine.org/en/stable/getting_started/scripting/gdscript/gdscript_advanced.html#custom-iterators)。

## `match`

- 相当于 `switch`，但是默认 break。
- `continue` 指定 fallthrough。
- `_` 相当于 default。

``` gd
match [expression]:
    [pattern](s):
        [block]
    [pattern](s):
        [block]
    [pattern](s):
        [block]
```

``` gd
# Constant pattern
match x:
    1:
        print("We are number one!")
    2:
        print("Two are better than one!")
    "test":
        print("Oh snap! It's a string!")

# Variable pattern
match typeof(x):
    TYPE_REAL:
        print("float")
    TYPE_STRING:
        print("text")
    TYPE_ARRAY:
        print("array")

# Wildcard pattern
match x:
    1:
        print("It's one!")
    2:
        print("It's one times two!")
    _:
        print("It's not 1 or 2. I don't care to be honest.")

# Binding pattern
match x:
    1:
        print("It's one!")
    2:
        print("It's one times two!")
    var new_var:
        print("It's not 1 or 2, it's ", new_var)

# Array pattern
match x:
    []:
        print("Empty array")
    [1, 3, "test", null]:
        print("Very specific array")
    [var start, _, "test"]:
        print("First element is ", start, ", and the last is \"test\"")
    [42, ..]:
        print("Open ended array")

# Dictionary pattern
match x:
    {}:
        print("Empty dict")
    {"name": "Dennis"}:
        print("The name is Dennis")
    {"name": "Dennis", "age": var age}:
        print("Dennis is ", age, " years old.")
    {"name", "age"}:
        print("Has a name and an age, but it's not Dennis :(")
    {"key": "godotisawesome", ..}:
        print("I only checked for one entry and ignored the rest")

# Multiple patterns
# 注意使用 Multiple patterns 时不允许使用 binding
match x:
    1, 2, 3:
        print("It's 1 - 3")
    "Sword", "Splash potion", "Fist":
        print("Yep, you've taken damage")
```

## 模板字符串

实现了类似于 C 的[功能](https://docs.godotengine.org/en/stable/getting_started/scripting/gdscript/gdscript_format_string.html)。

``` gd
"We are waiting for %s." % "Godot"

"We are waiting for {whom}.".format({ "whom": "Godot" })
```

## 信号

观察者模式。

可以声明和使用自定义信号

``` gd
signal my_signal
signal my_arg_signal(v1, v2)

func _ready():
    emit_signal("my_signal")
    emit_signal("my_arg_signal", true, 42)
```

## 分组

订阅模式。

``` gd
extends Panel

func ui_group_callback():
   var ui_group_members = get_tree().get_nodes_in_group("ui")
    get_node("Button").text = "Called"

func _ready():
    add_to_group("ui")
    get_node("Button").connect("pressed", self, "_on_Button_pressed")

func _on_Button_pressed():
    get_node("Label").text = "Hello!"
    get_tree().call_group("ui", "ui_group_callback")
```

## 通知

底层的 `Object._notification`

``` gd
func _notification(what):
    match what:
        NOTIFICATION_READY:
            print("This is the same as overriding _ready()...")
        NOTIFICATION_PROCESS:
            print("This is the same as overriding _process()...")
```

## 实例化节点

``` gd
var s
func _ready():
    s = Sprite.new() # Create a new sprite!
    add_child(s) # Add it as a child of this node.
```

``` gd
func _someaction():
    s.free() # Immediately removes the node from the scene and frees it.
```

节点在释放时会自动释放子节点。

释放处于“阻塞”状态（正在发出信号或正在调用函数）的节点会导致崩溃。

``` gd
func _someaction():
    s.queue_free() # Removes the node from the scene and frees it when it becomes safe to do so.
```

## 实例化场景

``` gd
var scene = load("res://myscene.tscn") # Will load when the script is instanced.
# or
var scene = preload("res://myscene.tscn") # Will load when parsing the script.

var node = scene.instance()
add_child(node)
```

## 脚本类

可以将脚本以类的形式注册到场景编辑器中。

若没有 `extends` 则默认继承 `Reference`。

``` gd
extends Node

# Declare the class name here
class_name ScriptName, "res://path/to/optional/icon.svg"

func _ready():
    var this = ScriptName           # reference to the script
    var cppNode = MyCppNode.new()   # new instance of a class named MyCppNode

    cppNode.queue_free()
```

- 使用 `is` 检查是否继承自某个类。
- `_init(args).(parent_args)` 可以向父类构造器传参。
- `class InnerClassName` 声明内部类。
- `var var_name = value setget setter_func getter_func` 提供 setter / getter
- 使用 `as` 进行类型转换。

## 资源

``` gd
func _ready():
    var res = load("res://robi.png") # Godot loads the Resource when it reads the line.
    get_node("sprite").texture = res

func _ready():
    var res = preload("res://robi.png") # Godot loads the resource at compile-time
    get_node("sprite").texture = res

func _on_shoot():
    var bullet = preload("res://bullet.tscn").instance()
    add_child(bullet)
```

## SceneTree

`get_tree` `change_scene`

## 工具

GD Script 最强大的功能之一。

``` gd
tool

export(int) var size = 10

func _ready():
    if Engine.editor_hint:
        # 在编辑器中的专用代码
```

## 协程 `yield`

``` gd
func a():
    printraw("Greetings to ")
    yield()
    printraw(".")

func b():
    var r = a()
    printraw("Godot")
    r.resume()

# Greetings to Godot.
```

``` gd
func generator():
    for i in 5:
        yield(i)

func _ready():
    y = generator()
    while y is GDScriptFunctionState && y.is_valid():
        y = y.resume()
```

可以与信号结合在一起使用，收到来自对象的信息后恢复执行。

``` gd
# 在下一帧执行
yield(get_tree(), "idle_frame")

# 动画播放完成之后执行
yield(get_node("AnimationPlayer"), "animation_finished")

# 5秒后执行
yield(get_tree().create_timer(5.0), "timeout")
```

``` gd
func my_func():
    yield(button_func(), "completed")
    print("嗯 ，终 于 按 下 了 所 有 按 钮 !")
func button_func():
    yield($Button0, "pressed")
    yield($Button1, "pressed")
```
