Spring MVC中常用的注解有很多，它们用于在Controller类、处理器方法、请求参数、响应、视图等方面进行配置和标记。以下是一些常用的Spring MVC注解：

## @Controller：
用于标记一个类作为Spring MVC的控制器。
## @RequestMapping：
用于映射Web请求到处理器类或处理器方法上，并指定处理请求的URL路径。
## @GetMapping：
用于映射HTTP GET请求到处理器方法上。
## @PostMapping：
用于将特定的HTTP请求映射到带有`@Controller`或`@RestController`注解的方法上。它是`@RequestMapping`注解的一个特定变体，专门用于处理HTTP [[HTTP请求里POST和GET的区别|POST请求。]]
### 基本用法：
```java
@RestController
@RequestMapping("/example")
public class ExampleController {

   @PostMapping("/submit")
   public ResponseEntity<String> handleSubmit(@RequestBody String data) {
	   // 处理POST请求的业务逻辑
	   return ResponseEntity.ok("Submission successful");
   }
}
```
### 指定Consumes和Produces：
可以使用`consumes`和`produces`属性来指定处理请求的`Content-Type`和返回的`Content-Type`。例如：
   ```java
   @PostMapping(value = "/submit", consumes = MediaType.APPLICATION_JSON_VALUE, produces = MediaType.APPLICATION_JSON_VALUE)
   public ResponseEntity<MyResponse> handleSubmit(@RequestBody MyRequest request) {
       // 处理请求和返回业务逻辑
       return ResponseEntity.ok(new MyResponse("Submission successful"));
   }
   ```
上述示例中，通过`consumes`和`produces`属性，限定了请求和响应的`Content-Type`为JSON。
## @PutMapping：
用于映射HTTP PUT请求到处理器方法上。

6. **@DeleteMapping：** 用于映射HTTP DELETE请求到处理器方法上。

7. **@PatchMapping：** 用于映射HTTP PATCH请求到处理器方法上。

8. **@PathVariable：** 用于将请求URL中的模板变量绑定到处理器方法的参数上。

9. **@RequestParam：** 用于将请求参数绑定到处理器方法的参数上。

10. **@ModelAttribute：** 用于将请求参数绑定到处理器方法的参数上，并将其添加到模型中。

11. **@RequestBody：** 用于将HTTP请求的请求体（Body）绑定到处理器方法的参数上，常用于接收JSON或XML格式的请求数据。

12. **@ResponseBody：** 用于将处理器方法的返回值直接作为HTTP响应的内容返回给客户端，常用于返回JSON或XML格式的响应数据。

13. **@ResponseStatus：** 用于设置处理器方法返回的HTTP响应状态码和原因短语。

14. **@ExceptionHandler：** 用于定义一个全局异常处理器，处理Controller中抛出的特定类型的异常。

15. **@SessionAttributes：** 用于标记一个模型属性，使其存储在会话（Session）中，以便多个请求之间共享。

16. **@CookieValue：** 用于将HTTP请求中的Cookie值绑定到处理器方法的参数上。

17. **@RequestHeader：** 用于将HTTP请求头信息绑定到处理器方法的参数上。

18. **@InitBinder：** 用于在Controller中初始化数据绑定器，用于对请求参数的预处理。

这些注解使得在Spring MVC中进行Web开发变得更加简单和灵活，开发者可以通过使用这些注解来快速地实现请求映射、数据绑定、异常处理等功能。