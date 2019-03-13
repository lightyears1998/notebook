# Android笔记

## 基本知识

- Android应用运行在自己的安全沙箱内。（每个应用是操作系统的不同用户，每个应用在其自己的Linux进程内运行，每个进程具有自己的虚拟机）*最小权限原则*
- 默认情况下，同一个应用程序的所有应用程序组件都运行在相同的进程和线程中。

### 体系结构

1. 应用层 Applications
2. 应用框架层 Application Framework(Activity Manager, ...)
3. 库文件与Android运行时 Libraries and Android Runtime(SQLite, Dalvik Virtual Machine, ...)
4. Linux内核 Linux Kernel(drivers, ...)

### 基本组件

- *Activity* 具有用户界面的单一屏幕
- *Service* 服务后台长时间运行的操作，不提供用户界面
- *ContentProvider* 内容提供程序
- *BoardcastReceiver* 广播接收器
- *Intent* 消息传递者

详见[components](components)

### 资源管理

详见[resource-management.md](resource-management.md)

## 应用程序清单 AndroidManifest.xml

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

常用权限

- 网络 `<uses-permission android:name="android.permission.INTERNET" />`
- 储存 `<uses-permission android:name="android.permssion.MOUNT_UNMOUNT_FILESYSTEMS" />`, `<uses-permission android:name="android.permssion.READ_EXTERNAL_STORAGE" />`, `<uses-permission android:name="android.permssion.WRITE_EXTERNAL_STORAGE" />`

---

- [API Reference](https://developer.android.com/reference)
- [Manifest API Level](https://developer.android.com/guide/topics/manifest/uses-sdk-element)
