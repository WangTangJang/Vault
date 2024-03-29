`Object` 类是 Java 中所有类的根类。以下是 `Object` 类的一些常用方法：
1. **`equals(Object obj)`**：
   - 用于比较两个对象是否相等。
   - 默认实现是比较对象的引用是否相同，但可以在子类中重写以自定义相等的逻辑。
2. **`hashCode()`**：
   - 返回对象的哈希码值。
   - 常用于[[哈希表]]等数据结构中。
3. **`toString()`**：
   - 返回对象的字符串表示。
   - 默认实现返回对象的类名和哈希码，但可以在子类中重写以提供更有意义的字符串表示。
4. **`getClass()`**：
   - 返回对象的运行时类。
   - 常用于获取对象的类信息。
5. **`clone()`**：
   - 创建并返回对象的副本（浅拷贝）。
   - 需要实现 `Cloneable` 接口，并在子类中重写。
6. **`finalize()`**：
   - 在对象被垃圾回收前调用。
   - 不推荐使用，因为不确定何时会被调用。
7. **`wait()`、`notify()`、`notifyAll()`**：
   - 用于线程间的通信和同步。
   - 需要在同步代码块中使用。
8. **`getClassLoader()`**：
   - 返回加载该对象的类加载器。

这些方法是 `Object` 类的基本方法，其他类都继承了这些方法。在自定义类中，可以根据需要重写这些方法，以满足特定的业务逻辑。