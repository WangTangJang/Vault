# 概念
**@Configuration 注解** 是 Spring 框架中用于定义**配置类**的注解。被标注的类会被 Spring 容器扫描并注册为 Bean。
# 属性:
- **value:** 指定配置类的名称，默认为类名。
- **proxyBeanMethods:** 是否使用 CGLIB 代理来创建 Bean。
# 用法
- 在类上使用 @Configuration 注解，声明该类为配置类。
- 在配置类中使用 @Bean 注解标注方法，定义 Bean。
- 使用 @Autowired 注解注入 Bean。
# 常见场景
- 定义数据库连接池。
- 定义事务管理器。
- 定义缓存管理器。
- 定义消息队列。
- 定义安全配置。
# 示例:
```Java
@Configuration
public class MyConfig {
    @Bean
    public MyService myService() {
        return new MyServiceImpl();
    }
}
```
# 注意事项
- @Configuration 注解不能用于 final 类。
- @Configuration 注解不能用于抽象类。
- @Configuration 注解不能用于接口。
# 扩展
- @Import 注解：用于导入其他配置类。
- @ComponentScan 注解：用于扫描指定包下的配置类和 Bean。
- @EnableXXX 注解：用于启用 Spring 的特定功能。
