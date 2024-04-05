**@Repeatable** 注解是 JDK 1.8 中引入的一个新注解，它允许在同一个地方重复使用同一个注解。

**@Repeatable 注解的语法:**

```java
@Repeatable(ContainerAnnotation.class)
public @interface Annotation {
    // ...
}

@interface ContainerAnnotation {
    Annotation[] value();
}
```
**@Repeatable 注解的用法:**
```Java
// 定义一个 @Skill 注解
@Repeatable(Skills.class)
public @interface Skill {
    String value() default "";
}

// 定义一个 @Skills 注解，用于包含多个 @Skill 注解
@interface Skills {
    Skill[] value();
}

// 使用 @Skill 注解标注一个类
@Skill("Java")
@Skill("Python")
public class Programmer {

}

// 获取 Programmer 类上的所有 @Skill 注解
Skill[] skills = Programmer.class.getAnnotationsByType(Skill.class);

// 遍历所有 @Skill 注解
for (Skill skill : skills) {
    System.out.println(skill.value());
}
```

在这个示例中，我们定义了两个注解：

- `@Skill` 注解：用于表示一个技能
- `@Skills` 注解：用于包含多个 `@Skill` 注解

我们使用 `@Repeatable` 注解将 `@Skill` 注解标记为可重复使用。然后，我们可以使用 `@Skill` 注解多次标注 `Programmer` 类，以表示该类支持的技能。

**@Repeatable 注解的优势:**

- 提高代码的可读性：可以将多个相关注解组合成一个注解，使代码更加简洁易懂。
- 提高代码的可维护性：可以更容易地添加和删除注解，而不会影响代码的结构。
