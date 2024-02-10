[原文地址](https://www.graalvm.org/latest/reference-manual/native-image/basics/)
Native Image 使用 Java 编写，将 Java 字节码**编译成**独立的二进制文件（可执行文件或共享库）。编译过程中，Native Image 可以运行用户代码。最后，Native Image 将编译后的用户代码、Java 运行时的部分（例如，垃圾收集器、线程支持）以及代码执行结果==链接==到二进制文件中。
此二进制文件称为本机**可执行文件**（**native executable**)或**本机映像**(**native image**)。我们将生成二进制文件的实用程序称为 `native-image` 构建器或 `native-image` 生成器。
为了清楚区分本机映像**构建期间**执行的代码和本机映像**执行期间**执行的代码，我们将两者之间的差异称为构建时间和运行时间。
为了生成最小映像，Native Image 采用了称为[静态分析](https://www.graalvm.org/latest/reference-manual/native-image/basics/#static-analysis)的过程。
## 构建时与运行时 
在镜像构建过程中，Native Image 可能会执行用户代码。此代码可能会产生副作用，例如将值写入类的静态字段。我们说这段代码是在**构建时**执行的。此代码写入静态字段的值保存在图像堆中。**运行时**是指执行时(*executed*)二进制文件中的代码和状态。
了解这两个概念之间差异的最简单方法是通过[可配置的类初始化](https://www.graalvm.org/latest/reference-manual/native-image/optimizations-and-performance/ClassInitialization/)。*在Java中，类在第一次使用时被初始化。* ~~构建时使用的每个 Java 类都被认为是构建时初始化的。请注意，仅仅加载类并不一定会初始化它。构建时初始化类的静态类初始值设定项在运行映像构建的 JVM 上执行。如果类在构建时初始化，则其静态字段将保存在生成​​的二进制文件中。在运行时，第一次使用这样的类不会触发类初始化。~~

用户可以通过不同的方式在构建时触发类初始化：
	通过将 `--initialize-at-build-time=<class>` 传递给 `native-image` 构建器。
	通过在构建时初始化类的静态初始化器中使用类。
Native Image 将在映像构建时初始化**常用**的 JDK 类，例如 `java.lang.String` 、 `java.util.**` 等。请注意，构建时类初始化是一项专业功能。并非所有类都适合构建时初始化。
以下示例演示了构建时执行代码和运行时执行代码之间的区别：
```java
public class HelloWorld {
    static class Greeter {
        static {
            System.out.println("Greeter is getting ready!");
        }
        
        public static void greet() {
          System.out.println("Hello, World!");
        }
    }

  public static void main(String[] args) {
    Greeter.greet();
  }
}
```
在 JVM 上编译并运行该应用程序：
```bash
javac HelloWorld.java
java HelloWorld 
Greeter is getting ready!
Hello, World!
```
构建它的原生镜像：

```bash
native-image HelloWorld
========================================================================================================================
GraalVM Native Image: Generating 'helloworld' (executable)...
========================================================================================================================
...
Finished generating 'helloworld' in 14.9s.
```
运行：
```bash
./helloworld 
Greeter is getting ready!
Hello, World!
```
`HelloWorld` 启动并调用 `Greeter.greet` 。这导致 `Greeter` 初始化，并打印消息 `Greeter is getting ready!` 。这里我们说 `Greeter` 的类初始值设定项在映像运行时执行。

令`native-image` 在构建时初始化 `Greeter` ：
```bash
native-image HelloWorld --initialize-at-build-time=HelloWorld\$Greeter
=====================================================================================================================
GraalVM Native Image: Generating 'helloworld' (executable)...
========================================================================================================================
Greeter is getting ready!
[1/7] Initializing...                                                                                    (3.1s @ 0.15GB)
 Version info: 'GraalVM dev Java 11 EE'
 Java version info: '11.0.15+4-jvmci-22.1-b02'
 C compiler: gcc (linux, x86_64, 9.4.0)
 Garbage collector: Serial GC
...
Finished generating 'helloworld' in 13.6s.
./helloworld 
Hello, World!
```
## 本机映像堆
本机映像堆，也称为映像堆，包含：
- 在映像构建期间创建的可从应用程序代码访问的对象。
- `java.lang.Class` 本机映像中使用的类的对象。
- 嵌入方法代码中的对象常量。
当本机映像启动时，它会从二进制文件复制初始映像堆。
将对象包含在映像堆中的一种方法是在构建时初始化类：
```java
class Example {
    private static final String message;
    
    static {
        message = System.getProperty("message");
    }

    public static void main(String[] args) {
        System.out.println("Hello, World! My message is: " + message);
    }
}
```
在 JVM 上编译并运行该应用程序：
```bash
javac Example.java
java -Dmessage=hi Example
Hello, World! My message is: hi
```

```bash
java -Dmessage=hello Example 
Hello, World! My message is: hello
```

```bash
java Example
Hello, World! My message is: null
```
现在检查一下当我们构建一个本机映像（其中 `Example` 类在构建时初始化）时会发生什么：
```bash
native-image Example --initialize-at-build-time=Example -Dmessage=native
================================================================================
GraalVM Native Image: Generating 'example' (executable)...
================================================================================
...
Finished generating 'example' in 19.0s.
```

```bash
./example 
Hello, World! My message is: native
```

```bash
./example -Dmessage=aNewMessage
Hello, World! My message is: native
```

`Example` 类的类初始值设定项在映像构建时执行。这为 `message` 字段创建了一个 `String` 对象并将其存储在映像堆中。
## 静态分析
静态分析是确定应用程序使用哪些程序元素（类、方法和字段）的过程。这些元素也称为**可达代码**。分析本身有两个部分：
- 扫描方法的字节码以确定可以从该方法访问哪些其他元素。
- 扫描本机映像堆中的根对象（即静态字段）以确定可以从它们访问哪些类。它从应用程序的入口点（即 `main` 方法）开始。迭代扫描新发现的元素，直到进一步扫描不会对元素的可达性产生额外的变化。
最终映像中仅包含可到达的元素。一旦构建了本机映像，就无法在运行时添加新元素，例如通过类加载。我们将此约束称为封闭世界假设。