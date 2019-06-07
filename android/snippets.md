# Snippets 代码片段

## 通用代码

- `System.out.println()` 在Logcat中的级别为`Info`，tag为`System.out`

## 异步装载器Loader

通过系统的回调方法将数据异步装载到ListView、GridView等控件中。

1. 对Activity和Fragment均有效
2. 存在数据改变通知机制
3. 横竖屏切换时可以保证组件数据不丢失

## 电话与短信

- SMSManager
- TelephoneManager

## 媒体

MeidaPlayer

## Sensor

SensorManager

## 撤销软键盘

```java
InputMethodManager imm = (InputMethodManager) getSystemService(Context.INPUT_METHOD_SERVICE);
imm.hideSoftInputFromWindow(view.getWindowToken(), 0);
```

## 使用全屏模式

使用预定义的全屏幕主题或自定义全屏幕主题

```xml
<style name="FullScreen" parent="Theme.AppCompat.Light.NoActionBar">
    <item name="android:windowFullscreen">true</item>
    <item name="android:windowContentOverlay">true</item>
</style>
```

隐藏软导航键

```java
setSystemUiVisibility(View.SYSTEM_UI_FLAG_HIDE_NAVIGATION);
```

## 保持屏幕常亮

```java
getWindow().addFlags(WindowManager.LayoutParams.FLAG_KEEP_SCRENN_ON);
getWindow().clearFlags(WindowManager.LayoutParams.FLAG_KEEP_SCRENN_ON);
```

其他：WakeLock，需要额外权限

## 确定设备的物理尺寸

`getResources().getConfiguration().sreenLayout & Configuration.SCREENLAYOUT_SIZE_MASK`

## 确定设备的屏幕像素大小

```java
WindowsManager wm = (WindowManager) context.getSystemService(Context.WINDOWS_SERVICE);

Display display = wm.getDefaultDisplay();
Point size = new Point();
display.getSize(size);

int screenWidth = size.x;
int screenHeight = size.y;
```

## 确定设备的DPI

```java
final int density = getResources().getDisplayMetrics().densityDpi;
```

## 检查网络连接

```java
public static boolean isConnectedToNetwork(Context context) {
    boolean connected = false;
    ConnectivityManager cm = (ConnectivityManager) context.getSystemService(Context.CONNECTIVITY_SERVICE);
    if (cm != null) {
        NetworkInfo ni = cm.getActiveNetworkInfo();
        if (ni != null) {
            connected = ni.isConnected();
        }
    }
    return connected;
}
```

## 检查当前线程是否为UI线程

```java
if (Looper.myLooper() == Looper.getMainLooper()) {
    // UI线程
} else {
    // 其他线程
}
```
