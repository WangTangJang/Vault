
SpringBoot在启动时会按照一定的顺序加载配置文件，并最终将所有配置合并成一个完整的配置对象。配置文件的加载顺序如下：
## 1. 命令行参数
命令行参数具有最高的优先级，可以覆盖任何配置文件中的配置。
## 2. 来自java:comp/env的JNDI属性
JNDI属性是 Java 命名和目录接口的缩写，可以通过 JNDI 服务器来存储和访问配置信息。
## 3. Java系统属性
Java系统属性可以通过 `-D` 参数来指定，也可以通过 `System.getProperties()` 方法来获取。
## 4. 操作系统环境变量

操作系统环境变量可以通过 `System.getenv()` 方法来获取。
## 5. 默认配置文件
SpringBoot会自动加载以下位置的默认配置文件：
- `file:./config/application.properties` 当前项目的config目录下
- `file:./application.properties` 当前项目的根目录 
- `classpath:/config/application.properties` classpath的/config目录
- `classpath:/application.properties` classpath的根目录
如果同一个目录下存在多个配置文件，则会按照以下顺序进行加载：
- `application.yml`
- `application.properties`
## 6. 外部配置文件
可以通过 `spring.config.location` 属性来指定外部配置文件的位置。
## 7. 配置文件合并
SpringBoot会将所有配置文件中的配置合并成一个完整的配置对象。合并时，会按照配置文件的加载顺序进行覆盖，即后加载的配置文件会覆盖先加载的配置文件中的同名配置。
