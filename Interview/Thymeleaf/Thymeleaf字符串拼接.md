Thymeleaf提供了多种方式来进行字符串拼接操作。以下是一些常见的方式:

1. **使用字符串连接运算符`+`**

```html
<span th:text="'Hello, ' + ${name} + '!'"></span>
```

2. **使用字符串连接运算符`+`和引号字面值**

```html
<span th:text="${'Hello, ' + name + '!'}"></span>
```

3. **使用字符串连接运算符`||`**

```html
<span th:text="'Hello, ' || ${name} || '!'"></span>
```

4. **使用预处理表达式`|`**

```html
<span th:text="|Hello, ${name}!|"></span>
```

5. **使用字符串连接工具类`th:with`**

```html
<span th:with="greeting='Hello, ' + ${name} + '!'">[[${greeting}]]</span>
```

6. **使用Thymeleaf的字符串操作工具类`th:block`**

```html
<th:block th:with="greeting='Hello, ' + ${name} + '!'">
    <span th:text="${greeting}"></span>
</th:block>
```

上述方式都可以用于拼接字符串。具体使用哪种方式取决于个人喜好和代码的可读性。值得注意的是,对于较长的字符串拼接操作,建议使用`th:with`或`th:block`,因为它们可以提高代码的可读性和可维护性。