Spring MVC的核心组件包括以下几个：
## DispatcherServlet（前端控制器）：
DispatcherServlet是Spring MVC的核心，负责接收客户端的请求，然后将请求分发给合适的处理器（Controller）进行处理。
## Controller（控制器）：
控制器是处理用户请求的组件，负责业务逻辑的处理，并返回相应的视图或数据。Controller通常使用`@Controller`注解进行标识。
## HandlerMapping（处理器映射）：
HandlerMapping负责将请求映射到相应的处理器（Controller）。Spring MVC支持多种HandlerMapping，包括`RequestMappingHandlerMapping`、`BeanNameUrlHandlerMapping`等。
## ViewResolver（视图解析器）：
视图解析器负责将逻辑视图名称解析为实际的视图对象。视图对象可以是JSP、Thymeleaf模板等。Spring MVC支持不同类型的视图解析器，如`InternalResourceViewResolver`、`ThymeleafViewResolver`等。
## ModelAndView： 
ModelAndView是一个包含模型数据和视图名称的对象，它将处理器方法的处理结果传递给DispatcherServlet，然后由DispatcherServlet根据视图解析器解析视图。
