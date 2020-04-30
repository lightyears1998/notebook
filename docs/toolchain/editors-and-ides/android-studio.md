# Android Studio

## Maven镜像

```groovy
repositories {
    maven {
        name 'google'
        url 'https://maven.aliyun.com/repository/google/'
    }

    maven {
        name 'jcenter'
        url 'https://maven.aliyun.com/repository/jcenter/'
    }
}
```

## ADB over tcp

```sh
adb devices
adb tcpip 5555
adb connect <IP-of-Device>:5555
adb devices
```
