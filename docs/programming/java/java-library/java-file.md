# Java 文件操作

## `java.io.BufferedReader`

```java
public static void main(String args[]) throws IOException {
    BufferedReader br = new BufferedReader(new FileReader("ReadFile.java"));
    for (String line = br.readLine(); line != null; line = br.readLine()) {
        System.out.println(line);
    }
    br.close();
}
```

## `java.io.FileInputStream` & `java.io.FileOutputStream`

```java
FileInputStream in = new FileInputStream("CopyFile.java");
FileOutputStream out = new FileOutputStream("CopyFile.java.tmp");

int read = in.read();
while (read != -1) {
    out.write(read);
    read = in.read();
}

in.close();
out.close();
```

## `java.io.File`

```java
File[] files = new File(".").listFiles();
for (File file : files) {
    if (file.isDirectory()) {
        System.out.println("<DIR>" + file.getName());
    } else {
        System.out.println(file.getName());
    }
}
```
