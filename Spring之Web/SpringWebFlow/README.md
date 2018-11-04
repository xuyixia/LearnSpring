# SpringWebFlow

目录索引:
[TOC]

SpringWebFlow是Spring的一个子项目、一个web框架、一个功能模块。当前最新版本为2.4.3.RELEASE。

````xml
<dependency>
    <groupId>org.springframework.webflow</groupId>
    <artifactId>spring-webflow</artifactId>
    <version>2.4.3.RELEASE</version>
</dependency>
````

当前版本的SpringWebFlow还未实现基于Java配置，因此使用XML配置是唯一方法。

## 一、它的作用

一般的web应用在访问过程中会遇到两种情况，有访问流程和没有访问流程。没有访问流程的应用类似门户网站那种的超链接随便点，前一个请求和后一个请求上没有任何关系。有访问流程的应用一般来说后一个请求位于前一个请求的页面当中，流程中后一个请求必须建立在前一个请求已经被访问了的基础上。如果应用没有实现流程化，容易出现越级访问的现象。  
SpringWebFlow框架让我们可以简单、快速的为web应用添加流程管理。  

## 二、实现原理

SpringWebFlow由两个组件构成  

1. 流程执行器
2. 流程定义


## 疑问
应用的访问流程在Spring Web Flow面世之前是如何实现的呢？印象中好像有个JPBM的东西，它也可以实现工作流。两者有什么区别呢？Spring web flow的“页面之间跳转”的这一功能，用session是否也可以实现？

## 参考
* [《Spring Web Flow 2.0 入门详解》](https://www.cnblogs.com/xwdreamer/archive/2011/11/10/2296939.html)