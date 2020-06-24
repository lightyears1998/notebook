# Resource Management 资源管理笔记

## `res/`

- 在`res/`目录下存放资源文件，应用程序可通过`R`类自动为资源生成的Resource ID访问，如`R.id.text_view`。
- 在Android Studio中添加资源文件：`New > Android Resource File`。

### 布局 `res/layout/*.xml`

eg. `R.layout.main`, `R.id.textView`

### 图片 `res/drawable/*`

eg. `R.drawable.icon` `android:background="@drawable/icon"`

### 文字 `res/values/strings.xml`

`getResources().getText(R.string.name);` `android:text="@string/hello_world"`

支持替代值 `getString(int, Object...)`或其他格式化语句

```xml
<resources>
    <plurals name="child_count">
        <item name="one">One child</item>
        <item name="other">%s children</item>
    </plurals>
</resources>
```

### 颜色 `res/values/colors.xml`

`getResources().getColor(R.color.red);`

通常使用`AARRGGBB`格式

`Color.RED`

```xml
<resources>
    <color name="system_color">@android:color/black</color>
    <color name="primary_color">#FFF43336</color>
</resources>
```

### 数组 `res/values/array.xml`

```xml
<resources>
    <string-array name="sample">
        <item>One</item>
        <item>Two</item>
        <item>Three</item>
    </string-array>
</resources>
```

### 尺寸 `dimens.xml`

`getDimensions()`

```xml
<resources>
    <dimen name="default_padding">16dp</dimen>
<resources>
```

### ID

```xml
<resources>
    <item name="tag_view_holder" type="id" />
</resources>
```

### 菜单

```xml
<resources>
    <menu>
        <item></item>
        <item></item>
    <menu>
</resources>
```

## `assets/`

应用程序中通过AssetManager取得资源。

`getResources().getAssets().open({"filename"});`

AssetsManager引用项目内的Asset，路径不需要以`/`开头。

`getAssets()`

- `list()`
- `oepn()`
