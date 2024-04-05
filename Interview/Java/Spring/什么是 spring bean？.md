在Spring框架中，一个“Bean”是指**由Spring容器管理的对象**。这些对象被称为Spring Bean，它们是Spring IoC（[[什么是控制反转？|控制反转]]）容器的核心组件之一。Bean是应用程序中的组件，由Spring容器负责创建、装配和管理。
# 重要概念：
1. **IoC容器：** IoC容器是Spring框架的核心，它负责管理和维护应用程序中的Bean。IoC容器通过控制反转的方式，将对象的创建和依赖关系的管理从应用程序代码中分离出来。
2. **Bean定义：** 在Spring中，每个Bean都有一个对应的Bean定义。Bean定义是一个元数据，它描述了一个Bean的属性、行为和依赖关系。Bean定义通常通过XML配置、Java配置或注解来定义。
3. **Bean的生命周期：** Spring容器负责管理Bean的[[请解释 Spring Bean 的生命周期？|生命周期]]，从创建到销毁。当应用程序需要一个Bean时，容器负责实例化该Bean；当Bean不再需要时，容器负责销毁它。开发者可以通过使用初始化方法和销毁方法来在Bean的生命周期的特定阶段执行自定义逻辑。
4. **Bean的作用域：** Spring支持不同的Bean作用域，包括单例（Singleton）、原型（Prototype）、会话（Session）、请求（Request）等。Bean的作用域定义了Bean实例在应用程序中的生命周期和可见性。
5. **依赖注入（DI）：** 通过依赖注入，Spring容器将Bean所需的依赖关系注入到Bean中，而不是Bean自己负责获取依赖。这样可以实现松耦合，提高可维护性和测试性。
# 示例
展示了如何在Spring中定义一个Bean：
```java
public class MyService {
    private MyRepository repository;

    // 构造函数注入
    public MyService(MyRepository repository) {
        this.repository = repository;
    }

    // 其他业务方法
}

public class MyRepository {
    // 数据访问逻辑
}
```
在这个例子中，`MyService`是一个Spring Bean，它通过构造函数注入了一个`MyRepository`的实例，这样就实现了依赖注入。在Spring容器中，你可以通过配置文件或注解来定义这些Bean，并由容器进行管理。