# Flex布局

* flex-direction: `row`(default) | `row-reverse` | `column` | `column-reverse`
* justify-content: `center` | `flex-start`(default) | `flex-end` | `space-between` | `space-around` | `space-evenly`(两侧留白与元素间留白等大)
* align-content: `center` | `flex-start` | `flex-end`
* align-items
* align-self 重写align-items
* flex-wrap: `nowrap`(default，将所有元素挤在一行（或列），即使设置了width可能不会生效) | `wrap`（换行，width生效） | `wrap-reverse`
* flex-shrink: 当空间不足时的`缩放权重`
* flex-grow: 空间富足时的`放大权重`
* flex-basis: 在缩放前的初始大小`px`, `em`...
* flex: `<flex-grow> <flex-shrink> <flex-basis>`

```plain
+----------------------------> 主轴方向 flex-flow
|       justify-content 主轴上元素的留白策略
|
|
|       align-content 单行无效，
|                     多个伸缩行之间的留白策略
|
|
|  align-items
|  交叉轴上元素的留白策略
|
v
交叉轴方向 flex-wrap
```

## 设置

```css
#flex-container {
    display: flex;
}
```
