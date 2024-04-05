**@Bean** 注解是 Spring 框架提供的用于*将方法返回值注册为 Bean 的注解*。@Bean 注解可以用于类、方法或字段上。
# 用法
@Bean 注解的用法很简单，只需要在需要注册为 Bean 的方法上加上 @Bean 注解即可。例如：
```Java
@Configuration
public class AppConfig {

    @Bean
    public MyBean myBean() {
        return new MyBean();
    }

}
```
在这个示例中，`myBean()` 方法会被 Spring 框架注册为 Bean，并可以使用 `@Autowired` 注解注入到其他 Bean 中。
# 属性
- **name**：Bean 的名称，默认为方法名
- **initMethod**：Bean 的初始化方法
- **destroyMethod**：Bean 的销毁方法
- **scope**：Bean 的作用域，默认为 **singleton**

