在Java中，代理（Proxy）通常指的是代理[[设计模式]]，它*允许一个对象（代理对象）作为另一个对象（被代理对象）的接口，以控制对被代理对象的访问*。代理对象通常用于在访问真实对象之前或之后执行一些额外的操作，比如记录日志、权限控制、性能监控等。代理模式主要分为两类：静态代理和动态代理。

### 1. 静态代理：
静态代理是在编译时就已经确定代理关系的代理模式。在静态代理中，代理类和真实对象实现同一个接口，代理类持有对真实对象的引用，并在代理方法中调用真实对象的方法，同时可以在代理方法中执行一些额外的操作。

```java
// 接口
interface Subject {
    void request();
}

// 真实对象
class RealSubject implements Subject {
    public void request() {
        System.out.println("RealSubject: Processing request.");
    }
}

// 代理类
class Proxy implements Subject {
    private RealSubject realSubject;

    public Proxy(RealSubject realSubject) {
        this.realSubject = realSubject;
    }

    public void request() {
        // 额外的操作
        System.out.println("Proxy: Pre-processing request.");
        
        // 调用真实对象的方法
        realSubject.request();
        
        // 额外的操作
        System.out.println("Proxy: Post-processing request.");
    }
}

// 使用静态代理
public class StaticProxyExample {
    public static void main(String[] args) {
        RealSubject realSubject = new RealSubject();
        Proxy proxy = new Proxy(realSubject);
        
        // 通过代理调用真实对象的方法
        proxy.request();
    }
}
```

### 2. 动态代理：
动态代理是在运行时动态生成代理对象，而不是在编译时确定的。Java中的动态代理通常通过 `java.lang.reflect.Proxy` 类和 `java.lang.reflect.InvocationHandler` 接口来实现。

```java
import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;

// 接口
interface Subject {
    void request();
}

// 真实对象
class RealSubject implements Subject {
    public void request() {
        System.out.println("RealSubject: Processing request.");
    }
}

// InvocationHandler 实现
class MyInvocationHandler implements InvocationHandler {
    private Object realSubject;

    public MyInvocationHandler(Object realSubject) {
        this.realSubject = realSubject;
    }

    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        // 额外的操作
        System.out.println("Proxy: Pre-processing request.");
        
        // 调用真实对象的方法
        Object result = method.invoke(realSubject, args);
        
        // 额外的操作
        System.out.println("Proxy: Post-processing request.");

        return result;
    }
}

// 使用动态代理
public class DynamicProxyExample {
    public static void main(String[] args) {
        RealSubject realSubject = new RealSubject();
        InvocationHandler handler = new MyInvocationHandler(realSubject);
        
        // 创建动态代理对象
        Subject proxy = (Subject) Proxy.newProxyInstance(
                Subject.class.getClassLoader(),
                new Class[] { Subject.class },
                handler
        );
        
        // 通过代理调用真实对象的方法
        proxy.request();
    }
}
```

动态代理使得代理的创建更加灵活，不需要为每个接口都创建一个对应的代理类。代理对象的生成是在运行时进行的，可以根据需要动态地决定代理的行为。动态代理通常应用于AOP、RMI等场景中。