---
title: Spring
date: 2020-06-22
sidebar: false
description: 小时候总是莫名的抵触java，不喜欢struts，spring。现在这个年纪看来，无知真可怕……学习些Spring
categories:
  - "IT"
---

## Spring IoC(Inversion Of Control)

- [DI(Dependency Injection)](https://www.zhihu.com/question/32108444/answer/309208647) 依赖注入，软件实体被动接受其依赖的其它组件被IoC容器注入 
- DL(Dependency Lookup)    软件实体主动去服务注册地查找其依赖的服务

Spring 框架最早是通过 XML 配置文件的形式来描述 bean 与 bean 之间的关系的，随着 Java 业界研发技术和理念的转变，基于 Java 代码和 Annotation 元信息的描述方式也日渐兴盛（比如 @Autowired 和 @Inject），但不管使用哪种方式，都只是为了简化绑定逻辑描述的各种“表象”，最终都是为本阶段的最终目的服务

主要特性：

1. 非侵入式：基于Spring开发的应用中的对象可以不依赖于Spring的API
2. 控制反转：IOC——Inversion of Control，指的是将对象的创建权交给Spring去创建。使用Spring之前，对象的创建都是由我们自己在代码中new创建。而使用Spring之后。对象的创建都是由给了Spring框架。
3. 依赖注入：DI——Dependency Injection，是指依赖的对象不需要手动调用setXX方法去设置，而是通过配置赋值。
4. 面向切面编程：Aspect Oriented Programming——AOP。通过预编译方式和运行期动态代理实现程序功能的统一维护。主要功能：日志记录，性能统计，安全控制，事物处理，异常处理等。  
5. 容器：Spring是一个容器，因为它包含并且管理应用对象的生命周期
6. 组件化：Spring实现了使用简单的组件配置组合成一个复杂的应用。在 Spring 中可以使用XML和Java注解组合这些对象。
7. 一站式：在IOC和AOP的基础上可以整合各种企业应用的开源框架和优秀的第三方类库（实际上Spring 自身也提供了表述层的SpringMVC和持久层的Spring JDBC）

**核心思想：IOC和AOP**  
Ioc控制反转，谁控制谁？控制什么？为什么要控制？
DI依赖注入，谁依赖谁？为什么要依赖？谁注入谁？为什么要注入？

AOP，基于动态代理，如果要代理对象，实现了某个接口，那么Spring AOP会使用JDK Proxy创建代理。AOP在日志记录和事务处理方面应用较多。

## Spring MVC
前后端解偶 @RestController

参考文章：  
[Spring MVC过时了吗？](https://www.zhihu.com/question/294282002/answer/521229241)

## Spring Boot

习惯优于配置

spring4.X提倡使用java配置和注解配置组合，而Spring Boot不需要任何xml配置