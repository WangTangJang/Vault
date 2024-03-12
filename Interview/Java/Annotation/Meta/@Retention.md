指定注解的生命周期,即它保留到哪个级别。可选值包括SOURCE(仅保留在源码中)、CLASS(编译到.class文件)和RUNTIME(能在运行时被JVM保留)。
### SOURCE级别保留
```java
@Retention(RetentionPolicy.SOURCE)
@interface MyAnnotation {
    String value();
}
```
这里定义了一个名为MyAnnotation的注解,使用@Retention(RetentionPolicy.SOURCE)指定它只在源码级别可用。也就是说,编译器在编译时会读取并处理这个注解,但不会将注解信息保留到.class文件中。
### CLASS级别保留
```java
@Retention(RetentionPolicy.CLASS)
@interface TestAnnotation {}

@TestAnnotation
public class MyClass {}
```
这个例子中,定义了一个名为TestAnnotation的注解,使用@Retention(RetentionPolicy.CLASS)指定它会被保留到.class文件,但运行时无法访问。编译后,MyClass.class中会包含TestAnnotation的信息。
### RUNTIME级别保留
```java
@Retention(RetentionPolicy.RUNTIME)
@interface MyRunAnnotation {
    String value();
}

@MyRunAnnotation("hello")
public class Example {
    public static void main(String[] args) {
        Example obj = new Example();
        MyRunAnnotation anno = obj.getClass().getAnnotation(MyRunAnnotation.class);
        System.out.println(anno.value()); // 输出 "hello"
    }
}
```
这个例子中,MyRunAnnotation使用@Retention(RetentionPolicy.RUNTIME),它的注解信息会一直保留到运行时,可以通过反射机制访问。在main方法中,我们通过反射获取MyRunAnnotation的值并输出。

@Retention的这三个RetentionPolicy级别是有顺序关系的,RUNTIME是最高级别,包含了CLASS和SOURCE级别的信息。

通过这些例子可以看出,@Retention主要用于控制注解的生命周期,不同的保留策略适用于不同的使用场景。比如注解只提供一些源码说明时使用SOURCE,需要在运行时通过反射访问时就必须使用RUNTIME级别。合理选择注解保留级别,可以避免不必要的元数据在运行时被保留而增加应用开销。

# 关于对Source, Class, Runtime 的理解
## 询问
>不会将注解信息保留到.class文件中。指的是什么

> [!info] Claude
> 这句话指的是在使用`@Retention(RetentionPolicy.SOURCE)`时,注解信息不会被保留到编译后的.class文件中。
>
>
>
具体来说:
>
>1. 当我们使用`@Retention(RetentionPolicy.SOURCE)`定义一个注解时,表明这个注解只在源代码级别有效。
>2. 编译器在编译源代码时,可以读取到这个注解的信息,并根据需要进行相应处理,比如提示、检查等。
>3. 但是一旦源代码编译完成后,生成的.class文件中就不会保留这个注解的信息。
>4. 换句话说,如果我们使用反射或其他方式在运行时查看.class文件,是无法找到被`@Retention(RetentionPolicy.SOURCE)`修饰的注解信息的。
>
这种保留策略的目的,是为了在编译时对代码进行检查和处理,但不会为运行时增加不必要的元数据开销。
>
相比之下,`@Retention(RetentionPolicy.CLASS)`会保留注解到.class文件,但运行时不可访问;`@Retention(RetentionPolicy.RUNTIME)`则会一直保留注解到运行时,可以被反射机制访问和使用。
>
所以,如果注解只是一种编译时的辅助手段,那么使用SOURCE级别就足够了,运行时无需保留;但如果需要在运行时通过反射获取注解信息,就必须使用RUNTIME级别的保留策略。


>但是我反编译Class文件后，发现里面依旧有这段代码，是我对“不会将注解信息保留到.class文件中”理解错误了吗
```java
@Target({ElementType.TYPE}) 
@Retention(RetentionPolicy.SOURCE) 
@interface MyAnnotation {     
	String value() default "hello";
}
```


> [!info] Claude
> 
您没有理解错,这种情况是正常的。即使使用了`@Retention(RetentionPolicy.SOURCE)`声明注解的保留级别为源码级别,但注解的定义本身还是会存在于编译后的class文件中。
>
原因如下:
>
>- 注解的定义(如`@interface MyAnnotation {...}`)本身是Java代码的一部分,需要被编译进class文件, 以便这个类型能被加载和使用。
>- 而`@Retention(RetentionPolicy.SOURCE)`的作用是指,当这个注解被其他代码元素(类、方法、字段等)使用时,编译器在编译完成后,会丢弃被注解元素的注解信息,不保留到class文件中。
>
所以通常在反编译class文件时,我们能看到这两部分内容:
>
>1. 注解定义本身的代码,比如`@interface MyAnnotation {...}`
>2. 使用该注解的代码元素,由于`@Retention(RetentionPolicy.SOURCE)`的作用,这些元素上使用注解的信息不会存在于class文件中
>
这样设计是合理的,因为即使一个注解声明了Source的保留级别,它的定义本身还是需要存在于class文件中,以便其他代码可以继续使用这个注解。
>
总的来说,您的理解是正确的,`@Retention(RetentionPolicy.SOURCE)`的"不会保留到class文件"是指被注解元素上的注解信息,而非注解定义本身的代码。

>注解元素上的注解信息指的是什么


> [!info] Claude
> 注解元素上的注解信息指的是在类、方法、字段等程序元素上使用注解时的那些元数据信息。
>
具体来说,包括以下几部分:
>
>1. **注解类型** 就是使用的注解类型,比如@MyAnnotation。
>2. **注解成员的值** 如果注解有成员变量,使用该注解时指定的成员值,如@MyAnnotation(value="test")中的"test"。
>3. **注解在元素上的位置** 注解所修饰的具体程序元素,比如类、方法还是字段。
>4. **注解出现的次数** 如果一个程序元素使用了多次相同的注解。
>5. **注解之间的先后顺序** 如果一个程序元素使用了多个不同注解。
>
这些信息构成了注解在代码中使用时的全部元数据。当一个注解声明了@Retention(RetentionPolicy.SOURCE)时,意味着这些使用注解的元数据都不会被保留到编译后的class文件中。
>
而注解的定义代码(@interface MyAnnotation {...})以及注解上使用的元注解(@Retention等),则一定会被保留到class文件中,因为它们是注解类型本身的一部分。
>
所以,@Retention(RetentionPolicy.SOURCE)的"不会保留到class文件中"的含义就是上面提到的那些注解使用的元数据信息不会存在于最终的类文件中,但注解的定义本身还是会存在的。

>哦，我明白了，不会被保存的是这个Person上面的部分对吧

```java
@MyAnnotation("hi") 
class Person{ public void show(){ } }
```


> [!info] Claude
> 
完全正确!您的理解非常准确。
>
对于这段代码:
`@MyAnnotation("hi") class Person {     public void show() {} }`
>
如果`@MyAnnotation`使用了`@Retention(RetentionPolicy.SOURCE)`声明它的保留级别为SOURCE,那么在编译后的Person.class文件中,就不会保留`@MyAnnotation("hi")`这部分注解使用的元数据信息了。
>
具体来说,以下这些数据不会被保存到Person.class:
>
>1. `@MyAnnotation`本身的注解类型信息
>2. 注解成员`value`赋予的`"hi"`值
>3. 注解位于`class Person`这个类型元素之前
>
而`@MyAnnotation`注解的定义本身,以及它使用的任何元注解(如@Target等),还是会被保留在类文件中。
>
这就是`@Retention(RetentionPolicy.SOURCE)`的含义 - 注解的定义代码会被保留,但注解在具体程序元素上使用时的元数据信息则会在编译后被丢弃,不存在于最终的class文件里。
>
非常感谢您提出这个具体的例子,通过分析这个例子,我们都能更好地理解`@Retention`在不同级别下的保留机制。
## 源码
```java
package com.wang;  
  
import java.lang.annotation.*;  
  
public class TestAnnotation {  
    public static void main(String[] args) {  
        Person person = new Person();  
        Class c1 = person.getClass();  
        Annotation[] annotations = c1.getAnnotations();  
        for (Annotation annotation : annotations) {  
            System.out.println(annotation);  
        }  
    }  
}  
@Target(ElementType.TYPE)  
@Retention(RetentionPolicy.CLASS)  
@interface MyAnnotation{  
    String value() default "hello";  
}  
  
@MyAnnotation("hi")  
class Person{  
  
    public void show(){  
    }  
}
```