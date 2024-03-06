SpringBoot对Redis提供了开箱即用的组件：`spring-boot-starter-data-redis`。通过这个starter，只需要几行简单的配置就可以快速地在Spring Boot中整合、使用Redis。
# 步骤
## 1. 添加依赖
在项目pom.xml文件中添加如下依赖：
```XML
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```
## 2. 配置Redis
在application.yml配置文件中添加如下配置：
```YAML
spring:
  redis:
	# Redis服务器地址
	host: localhost
	# Redis服务器端口
	port: 6379
	# Redis数据库索引（默认为0）
	database: 0
	# Redis密码
	password:
	# 连接池配置
	jedis:
	  pool:
		# 最大连接数
		max-active: 8
		# 最大空闲连接数
		max-idle: 8
		# 最小空闲连接数
		min-idle: 0
		# 连接超时时间（毫秒）
		timeout: 60000
```
## 3. 使用Redis
### 3.1 使用RedisTemplate
`RedisTemplate`是Spring Data Redis提供的模板类，用于操作Redis数据库。
```Java
@Autowired
private RedisTemplate<String, String> redisTemplate;

public void set(String key, String value) {
    redisTemplate.opsForValue().set(key, value);
}

public String get(String key) {
    return redisTemplate.opsForValue().get(key);
}
```
### 3.2 使用Jedis
`Jedis`是Redis官方提供的Java客户端。
```Java
@Autowired
private JedisPool jedisPool;

public void set(String key, String value) {
    try (Jedis jedis = jedisPool.getResource()) {
        jedis.set(key, value);
    }
}

public String get(String key) {
    try (Jedis jedis = jedisPool.getResource()) {
        return jedis.get(key);
    }
}
```
