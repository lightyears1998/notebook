# 应用程序清单 `AndroidManifest.xml`

XML头部具有版本和编码声明`<?xml version="1.0" encoding="utf-8"?>`。

XML使用Android命名空间：

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="net.qfstudio.primum">
    ...
</manifest>
```

一个典型的应用程序清单：

```xml
<manifest package="com.example.app">
    <uses-permission />
    <application
        icon="@mipmap/ic_launcher_round"
        label="@string/app_name"
        theme="@style/AppTheme">
        <activity
            name=".MainActivity"
            label="@string/app_name"
            theme="@style/AppTheme">
            <intent-filter>
                <action name="android.intent.action.MAIN" />
                <category name="android.intent.category.LAUNCHER" />
            </intent-fileter>
        </activity>
    </application>
</manifest>
```

注意权限声明的位置与`Application`标签同级。

## 应用程序权限

- 网络 `<uses-permission name="android.permission.INTERNET" />`
- 储存 `<uses-permission name="android.permssion.MOUNT_UNMOUNT_FILESYSTEMS" />`, `<uses-permission name="android.permssion.READ_EXTERNAL_STORAGE" />`, `<uses-permission name="android.permssion.WRITE_EXTERNAL_STORAGE" />`
