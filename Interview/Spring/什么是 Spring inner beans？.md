Spring框架中的"inner beans"（内部Bean）指的是在**另一个**Bean的内部定义的Bean，而不是在容器级别单独声明的独立Bean。内部Bean通常是一种局部性的Bean，其作用域限定在包含它的外部Bean内。

使用内部Bean的情况通常是因为这个Bean只在外部Bean内部使用，而不需要在容器的其他地方引用它。这有助于封装和组织相关的Bean，使得配置文件更加清晰，只有在需要时才创建这些内部Bean。

以下是一个使用内部Bean的示例：
```xml
<bean id="outerBean" class="com.example.OuterBean">
    <property name="innerBean">
        <!-- Inner Bean 的定义 -->
        <bean class="com.example.InnerBean"/>
    </property>
</bean>
```

在这个例子中，`outerBean` 包含了一个名为 `innerBean` 的内部Bean。这个内部Bean的定义直接嵌套在外部Bean的配置中，不需要在配置文件的其他地方引用它。这种方式使得 `innerBean` 变成了 `outerBean` 的私有实例。

使用内部Bean可以带来一些好处，如：

1. **封装性：** 内部Bean只在外部Bean内部可见，不会污染容器的全局命名空间，使得配置更加清晰和模块化。

2. **局部性：** 内部Bean只在包含它的外部Bean的上下文中存在，不会对其他部分的应用程序产生影响。

3. **简洁性：** 对于一些仅在一个地方使用的小型Bean，使用内部Bean可以避免在配置文件中为其分配一个全局的ID。

需要注意的是，内部Bean在某些情况下可能会导致该Bean无法被其他Bean引用，因此在选择使用内部Bean时，需要确保其适用于特定的场景。