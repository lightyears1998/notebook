# Gradle笔记

基于Ant和Maven的项目自动化构建工具，使用Groovy来声明项目设置。

## 配置

- 仓库 `repositories {}`
- 依赖 `dependencies {}`

Android平台特定配置 `android {}`

- applicationId 应用程序package名 应用程序商店中的唯一id
- minSdkVersion 最小Android版本
- targetSdkVersion 目标Android版本
- versionCode 用于代表版本信息的整数
- versionName 用于代表版本信息的字符串

### 等价配置

以下语句等价：

1. `implementation group: 'org.apache.httpcomponents' , name: 'httpclient-android' , version: '4.3.5.1'`
2. `implementation 'org.apache.httpcomponents:httpclient-android:4.3.5.1'`
