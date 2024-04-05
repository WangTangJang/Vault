**@ModelAttribute 注解**用于将**请求参数**、**方法参数**或**返回值**绑定到**模型**中，并提供以下功能：

- **将数据绑定到模型:** 可以将请求参数、方法参数或返回值绑定到模型中，方便在视图页面中访问。
- **简化视图代码:** 无需在视图页面中使用 EL 表达式获取模型数据，可以直接使用模型属性名访问。
- **支持复杂数据类型:** 可以绑定复杂数据类型，例如 POJO 对象、List 集合等。

**@ModelAttribute 注解的使用位置:**

- **类上:** 绑定到类上的所有方法。
- **方法上:** 绑定到该方法。
- **方法参数上:** 绑定到该方法参数。

**@ModelAttribute 注解的属性:**

- **value:** 指定模型属性的名称。
- **binding:** 指定如何将数据绑定到模型属性。
- **condition:** 指定绑定条件。

**示例:**

**1. 类上使用 @ModelAttribute 注解**

```Java
@ModelAttribute
public class User {

    private String name;
    private int age;

    // ...

}
```

**2. 方法上使用 @ModelAttribute 注解**
```Java
@RequestMapping("/user")
public String user(Model model) {

    // 将当前登录用户绑定到模型
    model.addAttribute("user", SecurityContextHolder.getContext().getAuthentication().getPrincipal());

    return "user";

}
```

**3. 方法参数上使用 @ModelAttribute 注解**
```Java
@RequestMapping("/user/{id}")
public String user(@PathVariable("id") Long id, Model model) {

    // 根据 ID 查询用户并绑定到模型
    model.addAttribute("user", userService.findById(id));

    return "user";

}
```

**4. 使用 @ModelAttribute 注解绑定复杂数据类型**


```Java
@RequestMapping("/user/list")
public String list(Model model) {

    // 查询所有用户并绑定到模型
    model.addAttribute("users", userService.findAll());

    return "user/list";

}
```


**总结:**

- **@ModelAttribute 注解**是 Spring MVC 中一个非常有用的注解，可以简化模型数据的绑定和访问。
- 了解 @ModelAttribute 注解的用法和属性，可以帮助您更好地开发 Spring MVC 应用程序。