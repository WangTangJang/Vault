`synchronized` 是 Java 中用于实现线程同步的关键字，它的**主要作用**是确保多个线程之间对共享资源的互斥访问，保证**同一时刻**只有一个线程访问代码块或方法。
## 用法：
### 同步方法：
   - 示例：
     ```java
     public synchronized void synchronizedMethod() {
         // 同步代码块
     }
     ```

### 同步块：
   - 示例：
     ```java
     public void someMethod() {
         // 非同步代码块

         synchronized (lockObject) {
             // 同步代码块
         }

         // 非同步代码块
     }
     ```
