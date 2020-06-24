# Grid

## 创建布局

1. `grid-template-columns: 20% 20% 20% 20% 20%;`

    还可以使用百分比以外的数值来标定宽度，例如：`px`, `em`和Grid特有的单位`fr`（按比例分配格点时使用，每个`fr`为一份）

    使用fr作为单位时，fr的宽度将在最后计算，`grid-template-columns: 50px 1fr 1fr 1fr 50px;`。

2. `grid-template: <row> / <column>`是上述代码的简写

## 指定行与列

使用负数来标定行或列时，`-1`是指逆序第一条网格线。

1. `grid-column-start`, `grid-column-end`结合使用时，渲染结果是`[两者中较小值, 较大值)`（即夹在初始格线与停止格线之间的部分）
2. `span`可用于在给出了`start`或`end`时，指定格子拓展的长度
3. `grid-column: <start> / <end>;`是上述语法的简写

类似的还有`grid-row`的使用。

1. `grid-area: <row-start> / <column-start> / <row-end> / <column-end>;`是上述语法的简写

未指定`grid-column-start`等位置元素时，元素按源代码中出现的顺序占据一个格点，使用`order: <number>`来改变默认排序，类似于`z-index`。

## 辅助计算

1. `repeat(5, 20%)`展开为`20% 20% 20% 20% 20%`

这个参数顺序挺满足英语简单部分前置的风格的。
