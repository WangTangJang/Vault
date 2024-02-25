`Scanner` 类是 Java 中的一个实用工具类，位于 `java.util` 包中，用于从各种输入源获取基本数据类型和字符串。主要用于从键盘、文件等输入流中读取数据。以下是一些 `Scanner` 类的常用方法和用法：

1. **创建 Scanner 对象**：

   ```java
   import java.util.Scanner;

   Scanner scanner = new Scanner(System.in); // 从标准输入（键盘）读取数据
   ```

   也可以使用字符串作为输入源：

   ```java
   String inputString = "Hello World!";
   Scanner scanner = new Scanner(inputString);
   ```

   或者从文件中读取数据：

   ```java
   File file = new File("input.txt");
   Scanner scanner = new Scanner(file);
   ```

2. **读取不同类型的数据**：

   - 读取整数：

     ```java
     int num = scanner.nextInt();
     ```

   - 读取浮点数：

     ```java
     double num = scanner.nextDouble();
     ```

   - 读取字符串：

     ```java
     String text = scanner.next();
     ```

   - 读取一行文本：

     ```java
     String line = scanner.nextLine();
     ```

3. **判断输入是否存在**：

   ```java
   if (scanner.hasNextInt()) {
       int num = scanner.nextInt();
       System.out.println("You entered: " + num);
   } else {
       System.out.println("Invalid input");
   }
   ```

4. **关闭 Scanner 对象**：

   ```java
   scanner.close();
   ```

   使用完 `Scanner` 后，应该关闭它以释放相关的资源。

示例代码：

```java
import java.util.Scanner;

public class ScannerExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter an integer: ");
        int num = scanner.nextInt();
        System.out.println("You entered: " + num);

        System.out.print("Enter a double: ");
        double dbl = scanner.nextDouble();
        System.out.println("You entered: " + dbl);

        System.out.print("Enter a string: ");
        String text = scanner.next();
        System.out.println("You entered: " + text);

        scanner.close();
    }
}
```

在上述示例中，用户被要求输入一个整数、一个浮点数和一个字符串，`Scanner` 类分别读取并输出这些输入。