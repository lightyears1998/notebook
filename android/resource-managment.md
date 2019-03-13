# Resource Management 资源管理笔记

## 度量单位

1. dp, Divice independent pixel，基于MDPI，一个dp即一个MDPI屏幕上的一个像素
2. sp，字体尺寸

## Assets

- `getResources().getAssets().open({"filename"});`

## 字符串

支持替代值 `getString(int, Object...)`或其他格式化语句

```xml
<resources>
    <plurals name="child_count">
        <item name="one">One child</item>
        <item name="other">%s children</item>
    </plurals>
</resources>
```

## 数组

```xml
<resources>
    <string-array name="sample">
        <item>One</item>
        <item>Two</item>
        <item>Three</item>
    </string-array>
</resources>
```

## 颜色

通常使用`AARRGGBB`格式

`Color.RED`

```xml
<resources>
    <color name="system_color">@android:color/black</color>
    <color name="primary_color">#FFF43336</color>
</resources>
```

## 尺寸

`getDimensions()`

```xml
<resources>
    <dimen name="default_padding">16dp</dimen>
<resources>
```

## ID

```xml
<resources>
    <item name="tag_view_holder" type="id" />
</resources>
```

## 菜单

```xml
<resources>
    <menu>
        <item></item>
        <item></item>
    <menu>
</resources>
```
