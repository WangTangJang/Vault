## Spring Boot 中的 Profile

**Profile** 是 Spring Boot 提供的一种功能，用于根据不同的环境加载不同的配置。例如，我们可以为开发环境、测试环境和生产环境分别配置不同的数据库连接、日志级别等。
### 使用 Profile
#### 配置文件
Spring Boot 会自动加载位于 `src/main/resources` 目录下的 `application.properties` 或 `application.yml` 配置文件。如果存在多个配置文件，例如 `application-dev.properties` 和 `application-prod.properties`，Spring Boot 会根据激活的 Profile 来选择加载哪些配置文件。
#### 激活 Profile
**1. 主配置文件中指定**
在主配置文件中，可以使用 `spring.profiles.active` 属性来指定激活的 Profile。例如：
```Properties
spring.profiles.active=dev
```
**2. 命令行参数**
在启动 Spring Boot 应用时，可以使用 `--spring.profiles.active` 参数来指定激活的 Profile。例如：
```bash
java -jar app.jar --spring.profiles.active=dev
```
**3. 环境变量**
可以设置 `SPRING_PROFILES_ACTIVE` 环境变量来指定激活的 Profile。例如：
```bash
export SPRING_PROFILES_ACTIVE=dev
```
#### 使用 @Profile 注解
在 Spring Boot 中，可以使用 `@Profile` 注解来控制某个类或方法是否在特定的 Profile 下生效。例如：
```Java
@Profile("dev")
public class DevConfig {

    // ...

}
```
### 示例
假设我们有一个 Spring Boot 应用，需要连接不同的数据库。我们可以为开发环境和生产环境分别创建不同的配置文件：
```Properties
# application-dev.properties
spring.datasource.url=jdbc:mysql://localhost:3306/dev
```
```Properties
# application-prod.properties
spring.datasource.url=jdbc:mysql://localhost:3306/prod
```
然后，我们可以使用 `@Profile` 注解来指定哪个配置类在哪个 Profile 下生效：
Java
```
@Configuration
public class DataSourceConfig {

    @Bean
    @Profile("dev")
    public DataSource devDataSource() {
        // ...
    }

    @Bean
    @Profile("prod")
    public DataSource prodDataSource() {
        // ...
    }

}
```
这样，在开发环境下启动应用时，会使用 `devDataSource` 创建数据库连接；在生产环境下启动应用时，会使用 `prodDataSource` 创建数据库连接。
### 总结
**Profile** 是 Spring Boot 中一个非常有用的功能，可以让我们根据不同的环境加载不同的配置。通过使用 Profile，我们可以更方便地管理不同环境下的配置，并使我们的应用更加灵活。