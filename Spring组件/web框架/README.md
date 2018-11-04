Spring MVC框架是Spring框架的一个模块。

Spring MVC对应Web应用三层架构中的表现层，属于高层。一般来说，SpringMVC肯定是搭配Spring的相关模块（如IOC容器）来运作的。

考虑这样几个问题，什么时候加载IOC容器?在哪加载IOC容器？

在单独使用Spring的IOC容器时，我们会在调用栈的栈底（先进后出）创建BeanFactory,然后取出要使用的Bean。在使用Spring MVC后，前端控制器DispacherServlet并不会让我们在其中创建BeanFactory,Spring MVC所有要调用的Bean被分配在两个上下文中（父上下文和子上下文），我们分情况单独讨论。


在谈父子上下文之前，需要说下跟它们相关的Listener。



在Spring MVC中，父子上下文是绝对的焦点。

父上下文（WebApplicationContext）

父上下文不能访问子上下文，反之可以。
父上下文被保存在ServletContext中。
父上下文使用监听器加载Bean
父上下文中管理的Bean包含业务逻辑层、持久化层、