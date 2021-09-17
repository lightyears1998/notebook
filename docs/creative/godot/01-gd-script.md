# GD Script

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

``` gd
extends Node

# Declare the class name here
class_name ScriptName, "res://path/to/optional/icon.svg"

func _ready():
    var this = ScriptName           # reference to the script
    var cppNode = MyCppNode.new()   # new instance of a class named MyCppNode

    cppNode.queue_free()
```

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
