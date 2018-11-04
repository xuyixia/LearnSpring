# 33

Spring AOP使用AspectJ的切点表达式语言来定义切点和切面，但是SpringAOP仅支持AspectJ切点指示器的一个子集。不能全面兼容AspectJ的原因是“SpringAOP是基于代理的，而切点表达式是与基于代理的AOP无关的”。  

SpringAOP支持的AspectJ切点指示器有如下：

||AspectJ指示器||
|--|--|--|
||execution( )||
|| arg( )||
||@args()||
||this()||
||target||
||@target()||
||within()||
||@within()||
||@annotation()||

SpringAOP在上述基础上新增了一个自有的指示器“bean( )”。  
上述SpringAOP支持的AspectJ指示器只是AspectJ指示器的一个==子集==，SpringAOP环境下非此子集的指示器会抛出IllegelArgument-Exception异常。  
指示器==execution()==是==实际执行匹配==的，其它的都是==限制匹配==的。  

### 多个指示器之间的操作符（逻辑运算符）  

指示器之间存在着逻辑上的关系，如“与” “或” “非”。  
由于 **&** 在XML中有特殊含义，因此在不同的配置环境中操作符的表示有区别。  
|基于java配置|基于XML配置|
|--|--|
|&&|and|
|\|\||or|
|!|not|

指示器的操作符是切点表达式的重要组成部分，如

```` java
execution(
    * com.google.test.Test.test(..) 
    && within(com.google.test.*)
)
````



## AOP实践

SpringAOP的实践在配置上有两种方式：基于java配置和基于XML配置。如何选择需要视情况而谈。  

### 一、基于java配置
