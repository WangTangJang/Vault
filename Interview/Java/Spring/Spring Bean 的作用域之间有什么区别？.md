Spring框架中，Bean的作用域定义了在应用程序中创建的Bean实例的生命周期和可见范围。Spring框架支持以下几种主要的Bean作用域：
## 单例（Singleton）：
- 在整个应用程序中，只存在一个Bean实例。
- 当容器启动时，就会创建该Bean实例，并在整个应用生命周期内共享。
- 默认的作用域是Singleton，如果在XML配置文件或使用注解时不指定作用域，则默认为Singleton。
```xml
<bean id="exampleBean" class="com.example.ExampleBean" scope="singleton"/>
```
```java
@Component
@Scope("singleton")
public class ExampleBean {
    // ...
}
```
## 原型（Prototype）：
- 每次请求该Bean时，容器都会创建一个新的实例。
- 每个客户端或使用该Bean的地方都有自己的实例，实例之间相互独立。
```xml
<bean id="exampleBean" class="com.example.ExampleBean" scope="prototype"/>
```
```java
@Component
@Scope("prototype")
public class ExampleBean {
    // ...
}
```
## 会话（Session）：
- 每个HTTP会话都会有一个单独的Bean实例。
- 仅在Web应用程序中有效，对于每个用户会话都创建一个独立的Bean实例。
```xml
<bean id="exampleBean" class="com.example.ExampleBean" scope="session"/>
```
```java
@Component
@Scope("session")
public class ExampleBean {
    // ...
}
```
## 请求（Request）：
- 每个HTTP请求都会有一个单独的Bean实例。
- 仅在Web应用程序中有效，对于每个HTTP请求都创建一个独立的Bean实例。
```xml
<bean id="exampleBean" class="com.example.ExampleBean" scope="request"/>
```
```java
@Component
@Scope("request")
public class ExampleBean {
    // ...
}
```
## 全局会话（Global Session）：
- 仅在使用portlet上下文时有效。
- 在全局会话中，一个Bean实例对于每个portlet上下文都是唯一的。
```xml
<bean id="exampleBean" class="com.example.ExampleBean" scope="globalSession"/>
```
```java
@Component
@Scope("globalSession")
public class ExampleBean {
    // ...
}
```
## 总结：
选择合适的作用域取决于应用程序的需求和设计。通常来说，单例是最常用的作用域，因为它在大多数情况下都能满足要求，并且可以提高性能。但是，在某些情况下，原型作用域可能更为适用，特别是当Bean包含有状态信息且不应该被共享时。
