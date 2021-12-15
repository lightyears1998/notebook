# 用户界面

## 控件

- Label
- TextureReact
- TextureProgress
- NinePatchRect
- TextureButton

## 容器

- MarginContainer
- CenterContainer
- VboxContainer, HboxContainer
- GridContainer

经验法则：

- 将UI分解为嵌套的盒式结构：从包含所有内容的最大盒子，到包含一个像带有标签的进度条、面板或按钮这样的小部件的小盒子。所有一切都是盒子
- 如果一个区域周围有一些留白 `MarginContainer`
- 按行或列组织元素  `HBoxContainer` `VBoxContainer`

## UI

- Tween 过渡动画
