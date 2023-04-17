# Blender

Under a viewport, press `N` to bring up property panel.
Hit `Ctrl + Space` to full screen on a panel.

- `~` or `z` to bring up pie menu.

## Object Mode

### 物体基本操作

- `左键` 选择；`右键` 上下文菜单
- `C` 滚动选择
- `Ctrl + Plus` 拓展选择
- `Ctrl + L` 选择与当前选中项目相连的部分

- 移动选中物体 `G`
- 旋转选中物体 `R`
- 缩放选中物体 `S`
- 按住 `Alt` + `G`, `R`, `S` 启用备用的移动、选择或缩放模式
  - `Alt` + `S` Shrink/Fatten 沿法线缩放
- 连按快捷键两次亦有其他编辑模式

- `右击` 取消操作
- `X`, `Y`, `Z` 或 `鼠标中键` 沿着指定的轴向移动

- `Ctrl` + `A`pply 应用（例如缩放等）

- `Shift + S` 操作 Cursor （例如将 Cursor 放置到世界原点）

- `SHIFT + D` 复制物体
- `X` 或 `Delete` 删除物体
- `H` (`Alt` + `H`) 隐藏物体

- `Ctrl + L` to link to shaders and others... to the last selected object.
- `Ctrl + P` to set parent to the last selected object.

### 视口基本操作

- `鼠标中键` 旋转视口
- `SHIFT + 鼠标中键` 移动视口
- `ALT + 鼠标中键` 正交地旋转视口
- 利用视口右上角的 Gizmoz 旋转和移动视口
- `` ` `` 召唤视图饼状菜单（三视图、摄像机视图、聚焦等）
- `数字键盘 .` 聚焦选中为物体

- `Ctrl + Alt + 0` View > Align View > Align Active Camera to View

### 视口组合

### 模式选择

- `Tab` 在当前模式和下一个模式（编辑模式）之间切换
- `Ctrl + Tab` 显示模式饼状选单

### 添加物体

- `SHIFT + A` 添加物体
- `F3` 召唤搜索框 搜索使用 Quick Smoke 快速烟雾
- 设置 Segment 的技巧：保持一个面是正方形会比较好。

### 添加修改器

扳手工具

- Subdivision Surface
- Solidify
- Shrinkwrap

## Edit View

- `Alt + Click` Select edge loop

- `Alt + N` 法线相关操作

- Toggle X-Ray `Alt + Z`
- Select Linked `L`
- Separate `P`
- Extrude `E`
- Add Face `F`

- `Ctrl + R` Loop cut
- `Ctrl + B` Add bevel

### Snapping

- Project individual elements

## Sculpting

Remember to apply modifiers in its order before starting sculpting.

`Ctrl` to reverse effects, `F` to set pen size and `Shift + F` to set strength.

- **Grab** `G`
- **Smooth** press `Shift` to temporary change to this tool
- **Inflate**

## Rendering

- 注意 Preferences > System 中的 Cycles Rendering Method 是否有硬件加速。
- Camera to View Or `Ctrl + Alt + NumPad 0` 将相机定位到当前视角。
- Scene > Performance > Persistent Data

If renders to animation, one can export all frames to OpenEXR and then export using blender as file editor.

## Shading

- `Ctrl + RMB` to cut connections. Use Node Wrangler plugin and `Ctrl Shift LMB` to preview the output of a node.
- `Ctrl + X` to delete node between keep the lines flow from left to right.

- Node Info (Random)
- Texture Coordinate
- Noise Texture
- ColorRamp
- Bump
- Image Texture
- Mix

## Texture Painting

Be patient.

## Geometry Nodes

`Ctrl + J` to add a frame around the node (to group nodes and write comments), and `F2` to rename the frame label.

- Distribute Points on Face
- Random Value
- Rotate Euler
- Set Position
- Joint Geometry
- Utility > Math
- Input > Value eg. `#frame`
- Combine XYZ

## Weight Mode

Paint on weigh mode will be saved as vertex group.

## Animation

- Select the object, and press `i` to add keyframe. (One can press `i` at almost everywhere.)
- Playback > Sync > Frame-dropping can be helpful.
- Use *Graph Editor* to view animation curve in details, and press `ctrl` to scroll the view in Graph Editor.
- Press `Home` to view the whole curve.
- Select the curve and hold `Ctrl + RMB` to add keyframe to the curve in Graph Editor.

## Lightning

Pay attention to the world lightning settings (Scene > World > Surface).

One can also change the color management settings (Scene > Color Management). Use "False Color" mode to check exposure settings. Use "High contrast" profile to achieve higher contrast.

In Scene > World > Film, background can be rendered as transparent.

## Compositor

In Blender post processing. `Ctrl + Shift + LMB` to preview the output of a node.

In Scene > ViewLayers > Passes, one can include more information for Compositor. It can be useful to include light information.

- Backdrop can be replaced by a view node and a split image editor that views the viewer node's content.
- RGB
- Alpha Over
- Ellipse Mask
- RGB Curve
- Blur
- Add
- Color Balance
- Lens Distortion (simulating lens effects.)
- Sharpen

## Filming

- Depth of Field of a camera (and F-stop)
- Motion Blur in Scene

---

## 控制杂项

- 模拟鼠标中键 开启 Preferences => Emulate 3 Button Mouse，按下 `ALT + 鼠标左键`模拟鼠标中键。
- 模拟 NumPad

---

## 参考资料

- [Guru制作 游戏叉叉兵翻译 的 blender 2.8 视频教程](https://www.bilibili.com/video/BV1az4y1X7Tr)
- [Tutorial: Blender MODELLING For Absolute Beginners - Simple Human](https://www.youtube.com/watch?v=9xAumJRKV6A)
