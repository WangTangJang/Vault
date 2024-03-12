`@Target`是Java中的一个元注解,它用于*指定被它所修饰的注解能够修饰哪些程序元素。*

`@Target`元注解的值是一个由`ElementType`常量组成的数组,`ElementType`是一个[[Enum|枚举]]类型,定义了各种可修饰的程序元素,如下:

- `TYPE` - 类、接口、枚举、注解类型
- `FIELD` - 字段,包括枚举常量
- `METHOD` - 方法
- `PARAMETER` - 参数
- `CONSTRUCTOR` - 构造方法
- `LOCAL_VARIABLE` - 局部变量
- `ANNOTATION_TYPE` - 注解类型
- `PACKAGE` - 包

使用`@Target`可以约束自定义注解的使用范围。例如:

```java
@Target({ElementType.TYPE, ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME) 
@interface MyAnnotation {
    // ...
}
```

这里`@Target`指定了`MyAnnotation`只能修饰类、接口或方法,不能修饰字段、构造器等其他程序元素。如果将上面的`MyAnnotation`注解加到一个字段上,编译器就会产生错误。
如果在定义注解时没有使用`@Target`指定目标,则**默认**该注解可以修饰所有程序元素。

# 源码
```java
@Documented  
@Retention(RetentionPolicy.RUNTIME)  
@Target({ElementType.ANNOTATION_TYPE})  
public @interface Target {  
    ElementType[] value();  
}
```

```java
public enum ElementType {  
    TYPE,  
    FIELD,  
    METHOD,  
    PARAMETER,  
    CONSTRUCTOR,  
    LOCAL_VARIABLE,  
    ANNOTATION_TYPE,  
    PACKAGE,  
    TYPE_PARAMETER,  
    TYPE_USE,  
    MODULE;  
  
    private ElementType() {  
    }  
}
```