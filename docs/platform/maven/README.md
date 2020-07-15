# Maven

Maven：地表最强构建工具之一。

## 设置

```xml
<!-- $HOME/.m2/settings.xml -->
<settings>
  <mirrors>
    <mirror>
      <id>aliyunmaven</id>
      <mirrorOf>*</mirrorOf>
      <name>阿里云公共仓库</name>
      <url>https://maven.aliyun.com/repository/public</url>
    </mirror>
  </mirrors>
</settings>
```

## 快速上手

``` sh
mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.4 -DinteractiveMode=false
```

``` sh
mvn package
java -cp target/my-app-1.0-SNAPSHOT.jar com.mycompany.app.App

mvn compile
mvn test
mvn site

mvn install # Install .JAR to location repository.
```
