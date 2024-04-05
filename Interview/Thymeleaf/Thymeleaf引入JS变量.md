在 Thymeleaf 中，我们可以通过以下几种方式来引入 JS 变量:

1. **使用 th:inline 内联表达式**

```html
<script th:inline="javascript">
/*<![CDATA[*/
    var name = /*[[${name}]]*/ "默认值";
    var age = /*[[${age}]]*/ 0;
/*]]>*/
</script>
```

上述代码将在 JavaScript 中创建两个变量 `name` 和 `age`，从 Thymeleaf 模型中获取相应的值。如果模型中不存在这些变量，则使用提供的默认值。

2. **使用 th:attr 设置 JS 变量**

```html
<script th:attr="var-name=${name}, var-age=${age}">
    console.log(varName, varAge);
</script>
```

这种方式通过设置 `var-name` 和 `var-age` 属性来传递变量值。在 JavaScript 中，使用驼峰式命名访问这些变量。

3. **使用 th:inline 和 th:removeTag**

```html
<script th:inline="javascript" th:removeTag="κεψ"></script>
    var name = [[${name}]];
    var age = [[${age}]];
</script>
```

这种方式将模板代码直接内联到 JavaScript 中，并移除 `<script>` 标签。

4. **使用 th:object 和 th:fields**

```html
<div th:object="${person}">
    <script th:inline="javascript">
    /*<![CDATA[*/
        var name = /*[[*{name}]]*/ "默认值";
        var age = /*[[*{age}]]*/ 0;
    /*]]>*/
    </script>
</div>
```

在这种情况下，我们使用 `th:object` 选择模型对象，然后使用 `th:fields` 从对象中获取字段值。

无论使用哪种方式，都需要注意防范潜在的 XSS 攻击。建议对从模型中获取的值进行适当的转义或验证。此外，也可以考虑将 JavaScript 代码分离到单独的文件中，以提高可维护性。