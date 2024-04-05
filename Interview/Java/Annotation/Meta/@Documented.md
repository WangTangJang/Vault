`@Documented`是一个标记注解,它被用作元注解,以指示被它修饰的那个注解应当被javadoc或其他工具文档化。

具体来说,使用`@Documented`的主要目的有以下几点:

1. **生成注解说明文档**
Javadoc工具在生成API文档时,会读取并保留使用了`@Documented`修饰的注解的说明信息,以便帮助文档化这个注解的用途。

2. **标记公共注解**
`@Documented`通常被用于标记那些将被其他开发者使用的公共注解。方便其他开发人员查看和理解该注解的作用。

3. **保留注解信息** 
使用了`@Documented`的注解,其注解信息会被保留在javadoc生成的API文档中,而不会像一些源码级别的注解那样被丢弃。

在Java的注解类型定义中,如果使用了`@Documented`修饰,就表明这个注解应当被文档工具记录下来,供开发人员参考。例如:

```java
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
public @interface TestAnnotation {
    String value();
}
```

这个`TestAnnotation`将会被Javadoc记录并生成相应的文档说明。

反之,如果没有使用`@Documented`修饰注解,那么该注解即使被标准化了,也不会被Javadoc等工具文档化,只在源代码级别可见。

总之,`@Documented`为了方便注解被开发人员理解和使用,起到了指示文档生成工具记录注解信息的作用。对于需要发布给其他开发者使用的公共注解来说,使用`@Documented`是一种很好的实践。