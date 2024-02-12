`@Resource`和`@Autowired`都是用于依赖注入的注解，但它们来自不同的规范，并且在注入方式和默认行为上有一些区别。
## 来源：
`@Autowired`是Spring框架的注解，而`@Resource`是来自Java的JSR-250规范，是Java的标准注解。
## 注入方式：
`@Autowired`默认按**类型**进行装配（这个注解属于Spring），默认情况下它要求依赖对象必须存在，如果允许null值，可以设置它的required属性为false。如果我们想使用按名称装配，可以结合`@Qualifier`注解进行使用。
`@Resource`默认按**名称**进行装配（这个注解属于J2EE），默认情况下它的name属性为null，当没有指定name属性时，它会自动采用标注处Java成员变量的名称作为bean的名称。如果没有指定name属性，并且按照默认的名称进行装配时没有找到匹配的bean，那么`@Resource`注解会回退为按类型装配。如果既没有指定名称，又无法通过类型找到bean，那么会抛出异常。 ^unnamable
## 是否支持字段、方法和构造函数注入：
`@Autowired`可以用于字段、构造函数和setter方法，而`@Resource`只能用于字段和setter方法。
