Java 默认导入了以下三个包：

- **`java.lang`:** 包含 Java 语言的核心类，如基本数据类型的包装类、字符串、异常类、线程类等。
- **`java.io`:** 提供与设备无关的输入输出流支持、文件和目录操作、数据序列化等功能。
- **`java.util`:** 提供常用的数据结构和算法，如集合、日期、时间、随机数等功能。

**以下是这些包中一些常用类的示例:**

- **`java.lang`:** `String`、`Integer`、`Math`、`System`、`Thread`
- **`java.io`:** `InputStream`、`OutputStream`、`File`、`PrintWriter`
- **`java.util`:** `List`、`Map`、`Set`、`Date`、`Calendar`、`Random`

默认导入的包可以让我们在编写代码时更加简洁，无需显式导入这些常用的包。

但是，在某些情况下，我们可能需要显式导入特定的包，例如:

- 当我们需要使用该包中某个特定的类时。
- 当我们需要避免与其他包中的类发生冲突时。

**例如，如果我们想要使用 `java.util.concurrent` 包中的 `ExecutorService` 类，则需要显式导入该包:**
```Java
import java.util.concurrent.ExecutorService;

public class Main {

    public static void main(String[] args) {

        // 显式导入 java.util.concurrent 包

        ExecutorService executorService = Executors.newFixedThreadPool(10);

        // ...

    }

}
```
