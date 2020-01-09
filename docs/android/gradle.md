# Gradle Build Script笔记

基于Ant和Maven的项目自动化构建工具，使用Groovy语言来声明项目设置。

## `build.gradle (project)`配置

顶层配置文件，可以定义`buildscript`等。

```groovy
// Top-level build file where you can add configuration options common to all sub-projects/modules.

buildscript {
    repositories {
        google()
        jcenter()
    }

    dependencies {
        classpath 'com.android.tools.build:gradle:3.1.3'

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

allprojects {
    repositories {
        google()
        jcenter()
    }
}

task clean(type: Delete) {
    delete rootProject.buildDir
}

```

## `build.gradle (module)`配置

`android {}`字段

- applicationId 应用程序package名 应用程序商店中的唯一id
- minSdkVersion 最小Android版本
- targetSdkVersion 目标Android版本
- versionCode 用于代表版本信息的整数
- versionName 用于代表版本信息的字符串

```groovy
apply plugin: 'com.android.application'

android {
    compileSdkVersion 26
    defaultConfig {
        applicationId "net.qfstudio.primum"
        minSdkVersion 26
        targetSdkVersion 26
        versionCode 1
        versionName "0.0.1"
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
}

dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    implementation 'com.android.support.constraint:constraint-layout:1.1.2'
    testImplementation 'junit:junit:4.12'
    androidTestImplementation 'com.android.support.test:runner:1.0.2'
    androidTestImplementation 'com.android.support.test.espresso:espresso-core:3.0.2'
}

```

### 等价语法

以下语句等价：

1. `implementation group: 'org.apache.httpcomponents', name: 'httpclient-android', version: '4.3.5.1'`
2. `implementation 'org.apache.httpcomponents:httpclient-android:4.3.5.1'`
