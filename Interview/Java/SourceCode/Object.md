在Java中，`Object`类是所有类的根类。每个类都直接或间接地继承自`Object`类，因此`Object`类中的方法对于所有Java对象都是可用的。以下是`Object`类的一些重要方法：

1. **`toString()`方法：** 返回对象的字符串表示。默认实现返回类名，后跟 "@" 符号和对象的散列码。通常应该被子类重写以提供更有意义的字符串表示。

    ```java
    public String toString() {
        return getClass().getName() + "@" + Integer.toHexString(hashCode());
    }
    ```

2. **`equals(Object obj)`方法：** 用于比较两个对象是否相等。默认实现使用的是对象的[[什么是对象引用？|引用]]相等性（即地址相等性），即两个对象引用同一个内存地址。

    ```java
    public boolean equals(Object obj) {
        return (this == obj);
    }
    ```

    通常，子类需要覆盖这个方法以提供根据对象内容的相等性比较。

3. **`hashCode()`方法：** 返回对象的散列码。默认实现返回对象的内存地址的哈希码。

    ```java
    public int hashCode() {
        return super.hashCode();
    }
    ```

    通常，如果`equals`方法被覆盖，也应该覆盖`hashCode`方法，以保持一致性。

4. **`getClass()`方法：** 返回对象的运行时类。通常用于获取对象的类信息。

    ```java
    public final native Class<?> getClass();
    ```

5. **`clone()`方法：** 创建并返回对象的副本。需要实现`Cloneable`接口，否则会抛出`CloneNotSupportedException`异常。

    ```java
    protected native Object clone() throws CloneNotSupportedException;
    ```

6. **`notify()`、`notifyAll()`和`wait()`方法：** 用于线程之间的协调和通信，这些方法需要在同步块中使用。

    ```java
    public final native void notify();
    public final native void notifyAll();
    public final native void wait(long timeout) throws InterruptedException;
    public final void wait(long timeout, int nanos) throws InterruptedException;
    public final void wait() throws InterruptedException;
    ```

7. **`finalize()`方法：** 该方法在对象即将被垃圾回收器回收时调用，可以用于释放资源或执行一些清理操作。不推荐使用，因为不可靠。

    ```java
    protected void finalize() throws Throwable {}
    ```

`Object`类中的这些方法为所有Java类提供了基本的行为和功能。在实际开发中，这些方法通常会被子类重写，以满足特定的业务需求。