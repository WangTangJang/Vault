# 简介
**@Import** 注解是 Spring 框架提供的用于*导入其他配置类*的注解。@Import 注解可以用于类、方法或字段上。
# 用法
@Import 注解的用法很简单，只需要在需要导入的配置类上加上 @Import 注解即可。例如：
```Java
@Configuration
public class AppConfig {
    @Import(AppConfig2.class)
    public class AppConfig2 {
    }
}
```
在这个示例中，`AppConfig` 类会导入 `AppConfig2` 类。
# 属性
@Import 注解可以设置以下属性：
- **value**：要导入的配置类的类数组
- **beanNameGenerator**：Bean 名称生成器的类


