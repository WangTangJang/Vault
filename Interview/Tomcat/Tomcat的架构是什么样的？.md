Apache Tomcat的架构是模块化的，由多个组件组成，每个组件负责不同的任务。以下是Tomcat的基本架构：

1. **Connector（连接器）**：
   - 连接器是Tomcat与外部客户端（如浏览器）之间的接口。它负责处理网络请求、监听端口，并将请求传递给Tomcat的其他组件。常见的连接器包括HTTP连接器（用于处理HTTP请求）和AJP连接器（用于与Apache HTTP Server等连接）。

2. **Catalina（卡塔利娜）**：
   - Catalina是Tomcat的Servlet容器，它实现了Servlet规范，负责管理Servlet的生命周期、处理HTTP请求和响应，以及管理会话（Session）。

3. **Engine（引擎）**：
   - 引擎是Tomcat的顶层组件，负责接收来自连接器的请求，并将其路由到适当的虚拟主机（Host）。

4. **Host（虚拟主机）**：
   - 虚拟主机代表了Tomcat服务器上的一个虚拟主机。每个虚拟主机可以包含多个Web应用程序。它负责处理来自引擎的请求，并将其路由到适当的上下文（Context）。

5. **Context（上下文）**：
   - 上下文代表一个Web应用程序。Tomcat可以同时托管多个Web应用程序，每个都有自己的上下文。上下文包含Web应用程序的配置信息、Servlet、过滤器等。

6. **Servlet容器**：
   - Servlet容器是Catalina的一部分，负责加载、初始化、调用和卸载Servlet。它提供了Servlet规范定义的运行环境。

7. **JSP引擎**：
   - JSP引擎负责处理JavaServer Pages（JSP）文件。它将JSP文件转换为Java Servlet，并交给Servlet容器处理。

8. **ClassLoader（类加载器）**：
   - 类加载器负责加载Web应用程序中的类。每个Web应用程序都有自己的类加载器，确保应用程序之间的类不会发生冲突。

这些组件共同工作，形成了Tomcat的完整架构。连接器负责接收请求，引擎将请求路由到适当的虚拟主机，虚拟主机将请求路由到适当的上下文，上下文通过Servlet容器和JSP引擎处理请求，最终生成响应返回给客户端。这种模块化的架构使得Tomcat非常灵活，可以方便地定制和扩展。