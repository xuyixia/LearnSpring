IOC容器负责容纳bean并对其进行管理。IOC容器在Spring核心模块中的实现是`org.springframework.beans.factory.BeanFactory `,由它来完成IOC容器概念上的功能。

BeanFactory是IOC容器的核心接口，它的职责包括：实例化、定位、配 置应用程序中的对象及建立这些对象间的依赖。

根据获取配置信息方式上的不同，核心模块提供了几种BeanFactory的实现。
1. XmlBeanFactory (基于XML配置文件)
2. 注解

如何选择实现呢？

1. 基于注解的java配置类目前是大势所趋，基于XML的文件配置有着太多的劣势，所以优先考虑注解。
2. 顺带提下基于注解的自动扫描，由于自动扫描使我们省掉了对象间依赖关系的配置，提高了开发效率，但是也正因为没了可视的对象关系，给后期维护带来了不良的影响。基于以上原因，最好是在开发阶段使用自动扫描，上线后换成java配置类或XML。


# 配置文件（广义）中包含哪些信息？
宏观上：
1. 组成应用的所有对象
2. 对象间依赖关系

微观上:
web三层架构的对象、Hibernate SsssionFactory对象、JMS Queue对象等等，项目复杂程度决定了bean的多寡。

# XML配置文件的方案
一、Spring团队推荐方案

将bean按照一定的分类生成多个XML文件，最后通过ApplicationContext构造器将它们加载为一个applicationContext文件。


这也是Spring团队推荐的做法。上述做法的好处在于实现了配置文件间的松耦合。无论是添加bean文件还是删除，都不会对其它配置文件造成影响。

二、其它方案

通过applicationContext引入其它bean文件，这种做法跟上述其实也差不多。
```` xml
<beans>
    <import resource="resources/themeSource.xml" /> 
</beans>
````

# XML配置文件元素和属性的简单介绍
一、 元素bean

1、 属性ID和属性Name

除了在唯一性上有所不同外，两者本质上一样。Id必须唯一。

2、 属性lazy-init和属性default-lazy-init

针对某个bean元素可以使用lazy-init属性设置其为延迟加载。这样的话只有该Bean在被调用的时候才会被初始化。但如果某个非延迟初始化bean依赖某个延迟初始化Bean,后者一样会随着容器初始化。

如果需要批量设置一批Bean延迟初始化，可以在Beans元素上设置default-lazy-init属性。

针对延迟初始化的一些思考：有无必要使用？可能在Bean比较多的情况下，延迟初始化会有启动效率上的优势。还可能尚未用到的Bean占用系统资源。非延迟初始化的优势就是能立即检查出配置文件上的错误，但是使用注解后这方面的优势也不复存在。延迟加载的优势似乎是有局限性的，非延迟加载的优势可以被取代。我个人感觉没必要使用。

3、注入方式的子元素property和constructor-arg以及注入类型的属性ref和内联Bean

DI的方式有两种，一个是setter注入，对应子元素property；另一个是构造器注入，对应子元素constructor-arg。

注入的类型可以是同容器中其它的Bean，用子元素ref定义。也可以是内联Bean。内联Bean指的是由property和constructor-arg元素定义的子元素。

内联Bean有：
1. 直接量（基本类型和String等）由子元素Value定义;value标签的值为空的时候，代表空字符串`“”`,而不是null。
2. 集合 通过<list/>、<set/>、<map/>及<props/>元素可以定义和设置与 Java Collection 类型对应 List、Set、Map 及 Properties 的值。3. nulls 

针对常用子元素的简写形式

由于子元素Value和ref用得比较频繁，所以诞生了简写形式。直接在对应的父元素上以属性的形式给出。

4、属性depends-on

这个属性我把它理解为显式的强制bean初始化，或者说强调一个Bean的依赖关系。除此之外我不知道它的作用