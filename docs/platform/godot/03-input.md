# Input 类

## 在 `_process` 时处理

- `is_action_just_pressed` 用于在 `_process` 时处理用户输入。

## 在输入事件时处理

第一个 Viewport 首先拿到用户输入，在一个 Viewport 中，Godot 输入事件处理顺序是 `_input(ev)` > `_gui_input(ev)` (`Control._input_event(ev)`) > `_unhandled_input(ev)` > `CollisionObject._input_event(ev)`。

`_input` 在 `_gui_input` 前，这就提供了先于 GUI 接触输入事件的机会。

调用 `SceneTree.set_input_as_handled()` 可以防止输入事件的进一步传播。

如果仍未处理，则传递到下一个 Viewport。

最终未处理的事件将被丢弃。
