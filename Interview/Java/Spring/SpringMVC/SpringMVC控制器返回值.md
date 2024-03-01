1. **String（视图名称）**:
    ```java
    @RequestMapping("/example")
    public String example() {
        // Some logic
        return "exampleView";
    }
    ```
   这样的控制器方法返回一个字符串，表示逻辑视图名称。这个逻辑视图名称将被解析成具体的视图页面（比如JSP、Thymeleaf等），用于渲染用户界面。
2. **ModelAndView**:
    ```java
    @RequestMapping("/example")
    public ModelAndView example() {
        // Some logic
        ModelAndView modelAndView = new ModelAndView();
        modelAndView.addObject("data", someData);
        modelAndView.setViewName("exampleView");
        return modelAndView;
    }
    ```
   这个方法返回一个`ModelAndView`对象，包含模型数据和逻辑视图名称。Spring MVC会使用配置的视图解析器来解析视图名称并渲染视图。
3. **ResponseBody（JSON数据）**:
    ```java
    @RequestMapping("/example")
    @ResponseBody
    public Map<String, Object> example() {
        // Some logic
        Map<String, Object> response = new HashMap<>();
        response.put("key", "value");
        return response;
    }
    ```
   使用`@ResponseBody`注解，方法返回的对象将直接作为HTTP响应的主体，通常用于返回JSON数据。这在RESTful API中很常见。
4. **Forward/Redirect**:
    ```java
    @RequestMapping("/example")
    public String example() {
        // Some logic
        return "forward:/newPath"; // forward to another path
        // or
        // return "redirect:/newPath"; // redirect to another path
    }
    ```
   可以使用`forward`或`redirect`关键字，将请求转发或重定向到另一个URL路径。
这只是一些基本的例子，实际上，根据应用程序的需求，控制器方法可能会返回更多类型的值，如`ResponseEntity`、`Callable`、`DeferredResult`等，以及使用异步处理和WebFlux的情况。
