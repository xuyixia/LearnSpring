# 部署服务器

应用服务器有很多，而我只用过Jetty和Tomcat。在服务器中部署项目，有很多种部署方式，下面分情况总结。

## Tomcat

### 一、外部部署

外部部署指的是将项目部署到外部服务器应用指定的目录下。它又分为静态项目部署和动态项目部署。

### 二、嵌入式部署

将应用服务器以项目组件的方式引入到项目中，实现standlone方式的运行。它有两种实现方式分别是“maven插件”和“Jar包依赖”。

## Jetty

### 一、外部部署
和Tomcat的外部部署类似，不再赘述。  

### 二、嵌入式部署

和Tomcat类似，也分为“maven插件”和“Jar包依赖”两种情况。maven插件需要执行mvn命令，而Jar包嵌入则需要新建一个standlone类型的JettyServer类，在main方法中启动。

#### 1、Jetty-Plugin

在启动Jetty插件后，它会自动去默认（也可指定）位置寻找下述文件

````xml
resources in ${project.basedir}/src/main/webapp
classes in ${project.build.outputDirectory}
web.xml in ${project.basedir}/src/main/webapp/WEB-INF/
````

前提是当前项目必须被maven管理，否则路径对不上。  
如果想要使用Servlet 3.0新增的基于Java配置的项目描述文件，需要注意Jetty对应的支持版本。  
我在“Jetty插件+基于java配置的项目描述文件”的实践环境中，遇到以下问题：  
1. 如果我的项目中同时存在web.xml和java配置的项目描述文件，后者是不被加载到Jetty服务器中的。在《spring action 4th》书中，作者提到两者可以共存，如何实现呢？
2. 某些注解的属性值配置错误，导致项目不能正确启动，该如何避免这类问题呢？如果错误启动，该怎么知晓哪个地方出问题了呢？  

我在实践的过程中，在配置子上下文的时候错误配置注解属性值，导致请求到达dispatcherServlet无法找到对应的控制器。这个排查错误的过程耗费了我4天，实在是无力吐槽。

````java
@Configuration
@EnableWebMvc
@ComponentScan("com.xuyixia.springmvc.javaconfig.action")
/*com/xuyixia/springmvc/javaconfig/action*/
public class ServletConfig extends WebMvcConfigurationSupport
```` 

## 参考文档

* [《maven项目配置jetty9插件》](https://blog.csdn.net/iamlihongwei/article/details/72782649)
* [《Maven创建支持Servlet3.0规范项目》](https://blog.csdn.net/wellplaying/article/details/79129176)（用到Jetty和tomcat插件，未用到MVC框架，没有前端Servlet,直接配置的Servlet）

https://blog.csdn.net/u014229282/article/details/73928680