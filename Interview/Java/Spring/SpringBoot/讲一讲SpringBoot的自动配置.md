SpringBoot的核心特性之一就是**自动配置**，它可以自动配置应用程序所需的大部分[[什么是 spring bean？| bean]]，包括数据源、事务管理器、Web服务器等。自动配置可以简化开发人员的工作，使他们无需手动配置这些bean。
# 原理
SpringBoot的自动配置是基于**条件注解**实现的。条件注解可以根据环境条件判断是否创建某个bean。例如，`@ConditionalOnClass`注解可以根据环境中是否存在某个类来判断是否创建bean。
SpringBoot提供了很多常用的条件注解，例如：
- `@ConditionalOnClass`：判断环境中是否存在某个类
- `@ConditionalOnProperty`：判断配置文件中是否存在某个属性
- `@ConditionalOnMissingBean`：判断环境中是否存在某个bean
# 示例
```Java
@SpringBootApplication
public class App {

    public static void main(String[] args) {
        SpringApplication.run(App.class, args);
    }

    @ConditionalOnClass(DataSource.class)
    @Bean
    public DataSource dataSource() {
        return new HikariDataSource();
    }
}
```
在这个示例中，`dataSource()`方法只有在环境中存在`DataSource`类时才会被创建。
# 总结
SpringBoot的自动配置可以简化开发人员的工作，使他们无需手动配置应用程序所需的大部分bean。自动配置是基于条件注解实现的，开发人员可以使用条件注解来自定义自动配置逻辑。
