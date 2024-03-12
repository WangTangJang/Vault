# 传递参数:

1. **通过th:with指令定义局部变量**

```html
<div th:with="name='John Doe',age=30">
    <div th:replace="~{fragment :: frag(${name}, ${age})}"></div>
</div>
```

在`th:replace`中,可以使用`${name}`和`${age}`作为参数传递给`frag`片段。

2. **通过th:attr指令设置属性**

```html
<div th:replace="~{fragment :: frag(@__${name}__, @__${age}__)}"></div>
```

在`th:replace`中,使用`@__${expr}__`语法将表达式`${name}`和`${age}`的值设置为片段的属性。然后在片段中获取这些属性值。

3. **通过th:object指令绑定对象**

```html
<div th:object="${person}" th:replace="~{fragment :: frag(*{name}, *{age})}"></div>
```

这里使用`th:object`绑定了一个`person`对象,然后在`th:replace`中使用`*{...}`语法访问对象的`name`和`age`属性。

4. **通过行内写法传递参数**

```html
<div th:replace="~{::frag('John Doe', 30)}"></div>

<th:block th:fragment="frag(name, age)">
    <p th:text="${name}"></p>
    <p th:text="${age}"></p>
</th:block>
```

这种方式直接在`th:replace`中传递参数值。

# 接收
你说得对,我没有解释如何在模板片段中接收传递的参数。以下是在片段模板中接收参数的方式:

1. **通过片段签名中的参数接收**

```html
<th:block th:fragment="frag(name, age)">
    <p th:text="${name}"></p>
    <p th:text="${age}"></p>
</th:block>
```

在这个例子中, `th:fragment="frag(name, age)"`定义了一个名为`frag`的片段,它接受两个参数`name`和`age`。在片段内部,我们就可以直接使用`${name}`和`${age}`来访问这些参数的值。

2. **通过th:attr获取属性值**

```html
<th:block th:fragment="frag(attrs)">
    <p th:text="${attrs.name}"></p>
    <p th:text="${attrs.age}"></p>
</th:block>
```

使用这种方式,传递的参数会被设置为片段的属性。在片段内部,我们使用`th:attr`来获取这些属性值,语法为`${attrs.xxx}`。

3. **通过th:object绑定对象访问属性**

```html
<th:block th:fragment="frag(person)" th:object="${person}">
    <p th:text="*{name}"></p>
    <p th:text="*{age}"></p>
</th:block>
```

这里我们在片段签名中接收一个对象`person`作为参数,然后使用`th:object`绑定该对象,就可以在片段内使用`*{xxx}`语法访问对象的属性。

