SpringBoot的4个特性

1. Spring boot starter
2. 自动配置
3. 命令行接口
4. Actuator

为了方便，后面将Spring Boot starter简称为s.b.s。

# SpringBootStarter
假如把所有要用到的JAR称之为依赖，那么Spring Boot starter依赖就是对一些常见依赖的有目的整合。比如某个项目以往需要手动引入100条依赖库，而s.b.s依赖直接整合这100条依赖，现在只需引入一条s.b.s依赖即可。

为了确保s.b.s不会引用过多无用的第三方库，所以对依赖的整合并不是“一锅端”，而是把细粒度稍微变粗、有明确目标用途的整合，也就是为了A用途整合几个依赖，为了B用途整合几个依赖。

S.b.s是通过其它的依赖管理工具（如maven，Gradle）来实现对用户透明引入依赖的。因此s.b的运行是建立在这些工具上的。

s.b.s依赖是这类具有整合特征的依赖的统称，不同的组合，不同的用途会有不同的s.b.s依赖。大致搜了下，挺多的，有空总结下常用的。

常用s.b.s依赖待补充

# 自动配置
自动配置的目的是为了削减spring的配置数量，它通过一些因素来推断项目中所需要的Spring配置。

哪些因素呢？
1. 文件触发。比如在类路径中嗅探到thymeleaf文件，s.b就会推断出我们要使用它，然后自动为我们配置相关的bean。
2. s.b.s依赖触发。当我们把一些s.b.s作为依赖加入到构建中来，比如web starter，s.b就推断出我们要用到Spring MVC,然后自动为我们配置相关的bean。

# CLI
说实话搞不懂这是干嘛的，据说根Groovy相关，如果我不用Groovy是不是就不用学这部分了？

# Actuator
中文翻译“驱动器”？？，看样子是给用户一个项目管理界面。