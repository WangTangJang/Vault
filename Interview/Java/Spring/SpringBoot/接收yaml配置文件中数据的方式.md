在 Spring Boot 中，可以通过以下几种方式来读取 YAML 配置文件中的数据:
## 使用 @Value 注解
可以使用 `@Value` 注解来注入单个的属性值，例如：
```java
@Value("${my.property.name}")
private String propertyName;
```
## 使用 @ConfigurationProperties 注解
`@ConfigurationProperties` 注解可以将配置文件中的属性自动绑定到结构化的对象上，例如：
```java
@Component
@ConfigurationProperties(prefix = "my.config")
public class MyConfig {
    private String name;
    private int age;
    // getter and setter
}
```
然后在 `application.yml` 中定义相应的属性：
```yaml
my:
  config:
    name: John
    age: 30
```
## 使用类型安全的配置属性
Spring Boot 还提供了一种**类型安全**的方式来读取配置属性，通过创建一个接口来定义属性，例如：
```java
@ConfigurationProperties("my.config")
public interface MyConfigProperties {
    String getName();
    int getAge();
}
```
然后在需要使用配置属性的地方，通过自动装配的方式注入该接口的实现：
```java
@Autowired
private MyConfigProperties myConfig;
```
## 直接访问 Environment
也可以直接访问 Spring 的 `Environment` 对象来获取配置属性的值，例如：
```java
@Autowired
private Environment env;

public void method() {
    String propertyValue = env.getProperty("my.property.name");
}
```

总的来说，使用 `@ConfigurationProperties` 注解或类型安全的配置属性是最常用和推荐的方式，因为它们提供了更好的类型安全性和可维护性。而 `@Value` 注解通常用于注入单个属性值，`Environment` 则提供了一种更低层次的方式来访问属性。