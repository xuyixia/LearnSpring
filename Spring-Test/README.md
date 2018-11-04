# Spring-test

开发过程中，为了保证编译后不出现错误，通常需要进行测试。最早的测试只是简单的在测试类中新增一个main方法，在main方法中新建当前类并测试相应方法。  
不能说上述的测试方式不对，只是它确实有很多弊端和不足。例如，对代码的侵入性、人工对比测试结果、无法批量测试、实际代码和测试代码耦合性太高。  
针对这些缺陷，出现了一个专门用于测试的框架——Junit。它就能很好地解决这些问题。Junit已经为5代了，功能上更加强大。    
在J2EE领域的java项目都是web项目，Junit的功能无法作用到web项目上。在常用的Spring框架中，有一款面向Spring的测试框架spring-test。它可以模拟请求和响应。


## test模块

Spring-test模块的单元测试和集成测试功能实际上底层是由Junit4或testNG组件来实现的（可以称作Spring整合Junit4或testNG）。因此在使用Spring-test的时候，还需要附带引入支持组件的Jar包。  
针对Spring的测试，test模块提供了一致性地加载和缓存Spring上下文；针对SpringMVC,提供了用于单独测试代码的模拟对象（mock object）。






## 参考
* [《如何在Spring和Spring MVC项目中进行测试》](https://www.cnblogs.com/lawlietfans/p/7667518.html)(看点：介绍了test模块的定位，分别介绍了spring和springMVC的测试方法,在MVC中，文章分别对REST和基于HTTP的RPC请求调用做了测试。)
* [《Spring整合Junit4进行单元测试》](https://blog.csdn.net/qq_39781497/article/details/78470279)(看点：提到创建一个公共测试父类供继承，简单的介绍了下逻辑层的spring-test的用法)
