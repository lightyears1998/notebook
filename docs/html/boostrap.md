# BootStrap

- 十二栏栅格布局。
- 五种屏幕大小：
    1. `xs` Extra samll
    2. `sm` Small
    3. `md` Medium
    4. `lg` Large
    5. `xl` Extra Large
- 通过`class`来取得样式，而不是重置标签的样式，以便结合其他预定义的框架。

## Layout

## Containers

- `container` 在每个断点处设置不同的宽度。
- `container-fluid` 总是拓展到所有可用的宽度。

## Grid System

- 行之间存在`gutter`，可以在`.row`中使用`no-gutter`取消。
- `col-<数字>` 占据一定列的
- `col-<尺寸>`, `col-<尺寸>-<数字>`, `col-<尺寸>-auto` 针对一定的屏幕尺寸布局，注意针对尺寸的定义向上兼容。
