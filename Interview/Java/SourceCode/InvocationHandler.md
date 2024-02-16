`InvocationHandler` 接口是 Java 中用于实现动态代理的核心接口之一，位于 `java.lang.reflect` 包中。它包含了一个单一的方法 `invoke`，用于在代理对象上处理方法调用。

```java
public interface InvocationHandler {
    Object invoke(Object proxy, Method method, Object[] args) throws Throwable;
}
```

- `proxy` 参数是代理对象本身，通常在 `invoke` 方法中不直接使用，但可以用于获取代理对象的信息。
- `method` 参数是被调用的方法对象，通过它可以获取方法的名称、返回类型、参数等信息。
- `args` 参数是方法调用时传递的参数数组。

在使用动态代理时，你需要提供一个实现 `InvocationHandler` 接口的类，然后在其 `invoke` 方法中定义对被代理对象方法的具体处理逻辑。

以下是一个简单的示例，演示了如何使用 `InvocationHandler` 接口实现一个简单的动态代理：

```java
import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;

interface Subject {
    void doSomething();
}

class RealSubject implements Subject {
    public void doSomething() {
        System.out.println("RealSubject is doing something.");
    }
}

class MyInvocationHandler implements InvocationHandler {
    private Object realSubject;

    public MyInvocationHandler(Object realSubject) {
        this.realSubject = realSubject;
    }

    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println("Before method execution");
        Object result = method.invoke(realSubject, args);
        System.out.println("After method execution");
        return result;
    }
}

public class DynamicProxyExample {
    public static void main(String[] args) {
        RealSubject realSubject = new RealSubject();
        InvocationHandler handler = new MyInvocationHandler(realSubject);

        // 创建动态代理对象
        Subject proxySubject = (Subject) Proxy.newProxyInstance(
                Subject.class.getClassLoader(),
                new Class[]{Subject.class},
                handler
        );

        // 通过代理对象调用真实对象的方法
        proxySubject.doSomething();
    }
}
```

在这个例子中，`MyInvocationHandler` 实现了 `InvocationHandler` 接口，它在 `invoke` 方法中加入了对方法调用前后的额外处理逻辑。通过 `Proxy.newProxyInstance` 方法创建了一个动态代理对象，该对象实现了 `Subject` 接口，并将方法调用委托给 `MyInvocationHandler` 中的 `invoke` 方法。