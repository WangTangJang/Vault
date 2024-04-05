# 简介
**@Import** 注解是 Spring 框架提供的用于*导入其他配置类*的注解。@Import 注解可以用于类、方法或字段上。
# 四种用法
## 导入Bean
使用`@Import`注解可以直接导入普通的Java类作为Spring Bean,比如:
```java
@Configuration
@Import({AServiceImpl.class, BServiceImpl.class})
public class AppConfig {
    // 其他Bean定义...
}
```
在上面的例子中,`AServiceImpl`和`BServiceImpl`两个类将会被Spring容器作为Bean来管理,就像使用`@Component`注解一样。

这种导入方式有以下一些特点:
1. 被导入的类不需要任何注解,可以是任意的POJO类。
2. 被导入的类如果有接口,Spring会自动为该接口创建相应的Bean。
3. 被导入的类可以有构造函数、静态代码块等初始化逻辑,Spring会执行这些逻辑。
4. 被导入的类及其依赖也会被Spring自动管理其生命周期。
5. 如果被导入的类本身使用了`@Configuration`注解,那么该类中定义的`@Bean`方法也会被处理。
6. 导入的 Bean 的名称默认为 **全限定类名**。
这种直接导入Bean的方式适用于一些简单的场景,如果Bean有比较复杂的依赖关系和配置逻辑,最好还是使用Java配置类或XML配置的方式。
## 导入配置类
```java
@Import(MyAppConfig.class)
```
通过@Import导入其他配置类,被导入的配置类必须标注了@Configuration注解。使用这种方式等价于在XML中使用`<import>`标签导入其他配置文件。
## 导入ImportSelector实现
**ImportSelector** 是 Spring 框架提供的一个接口，用于在 Spring 容器启动时动态导入额外的 Bean 定义。它可以用于根据条件或环境动态调整 Spring 容器的配置。
**ImportSelector 的工作原理:**
1. 使用 `@Import` 注解将 `ImportSelector` 类导入到另一个配置类中。
2. Spring 容器在启动时会扫描所有配置类，并找到所有使用 `@Import` 注解导入的 `ImportSelector` 类。
3. Spring 容器会调用 `ImportSelector` 类的 `selectImports` 方法来获取要导入的 Bean 定义的名称。
4. Spring 容器会根据 `selectImports` 方法返回的 Bean 定义名称，将这些 Bean 定义注册到容器中。
**ImportSelector 的实现步骤:**
1. 创建一个类并实现 `ImportSelector` 接口。
2. 实现 `selectImports` 方法。该方法返回一个字符串数组，其中包含要导入的 Bean 定义的名称。
3. 可以根据条件或环境动态调整要导入的 Bean 定义的名称。
**ImportSelector 的示例:**
```Java
public class MyImportSelector implements ImportSelector {
    @Override
    public String[] selectImports(AnnotationMetadata importingClassMetadata) {
        // 根据条件或环境动态调整要导入的 Bean 定义的名称
        if (isConditionMet()) {
            return new String[] {"com.example.MyBean1", "com.example.MyBean2"};
        } else {
            return new String[] {"com.example.MyBean3"};
        }
    }
    private boolean isConditionMet() {
        // 判断条件是否满足
        return ...;
    }
}
@Import(MyImportSelector.class)
public class MyConfiguration {

}
```
在这个示例中，`MyImportSelector` 类实现了 `ImportSelector` 接口。`selectImports` 方法根据条件动态调整要导入的 Bean 定义的名称。

**ImportSelector 的使用场景:**
- 根据环境动态调整 Spring 容器的配置。例如，根据不同的运行环境，可以导入不同的数据源配置。
- 根据条件导入额外的 Bean 定义。例如，根据配置文件中的参数，可以导入特定的功能模块。
**ImportSelector 的注意事项:**
- `selectImports` 方法返回的 Bean 定义名称必须是完全限定的类名。
- `ImportSelector` 类不能被 `@Component` 注解标注。
## 导入ImportBeanDefinitionRegistrar实现
```java
@Import(MyBeanDefinitionRegistrar.class)
```
通过实现ImportBeanDefinitionRegistrar接口,手工添加Bean到Spring容器中。使用这种方式可以直接操作BeanDefinition。
# 属性
@Import 注解可以设置以下属性：
- **value**：要导入的配置类的类数组
- **beanNameGenerator**：Bean 名称生成器的类


