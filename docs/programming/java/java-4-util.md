# Java工具

## 输入输出工具

### `java.util.Scanner`

```java
Scanner sc = new Scanner(System.in);
sc.hasNext(); // ...
sc.NextInt(); // ...
```

### `System.out.printf(format-string, var-list)`

类C语言的`printf`方法。

### 数字格式化工具

`java.text.NumberFormat`, `java.text.DecimalFormat`

每三位数字插入一个分隔符

```java
NumberFormat formatter = new DecimalFormat(",###");
formatter.format(number)
```

## 常用类

### `java.util.Random`

```java
Random rand = new Random(47);
rand.nextInt(100);  // 生成[0, 100)区间内的随机数
```

### `java.io.BufferedReader`

```java
public static void main(String args[]) throws IOException {
    BufferedReader br = new BufferedReader(new FileReader("ReadFile.java"));
    for (String line = br.readLine(); line != null; line = br.readLine()) {
        System.out.println(line);
    }
    br.close();
}
```

### `java.io.FileInputStream` & `java.io.FileOutputStream`

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

### `java.io.File`

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

### `java.util.StringTokenizer`

## 数据结构

### `java.util.Arrays`

- `Arrays.toString()` 打印数组

## `java.util.HashMap`

- `HashMap<String, Integer>`
- `size()`, `isEmpty()`
- `containsKey()`, `get()`
- `put()`
- `remove()`
