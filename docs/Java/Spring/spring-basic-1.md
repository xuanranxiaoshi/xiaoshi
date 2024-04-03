# Spring 框架

**Spring** : 是一款开源的轻量级 Java 开发框架，旨在提高开发人员的开发效率以及系统的可维护性。

**Spring 框架**：一般指的都是 Spring Framework，它是很多模块的集合使用这些模块可以很方便地协助我们进行开发，比如说 Spring 支持 IoC（Inversion of Control:控制反转） 和 AOP(Aspect-Oriented Programming:面向切面编程)；下图为 Spring5.x 版本的主要模块；

<!-- more -->

![Spring 5.x base modules](./images/spring-base-modules.png)

**Spring、Spring MVC、SpringBoot 之间的关系**

* Spring 包含了多个功能模块，其中最重要的是 Spring-Core（主要提供 IoC 依赖注入功能的支持） 模块，  Spring MVC 也是的 Spring 的一个模块，其功能实现基本需要依赖于该模块

* Spring MVC 是 Spring 中的一个很重要的模块，主要赋予 Spring 快速构建 MVC 架构的 Web 程序的能力。**MVC** 是模型(Model)、视图(View)、控制器(Controller)的简写，其**核心思想是通过将业务逻辑、数据、显示分离来组织代码。**
* 使用 Spring 进行开发各种配置过于麻烦比如开启某些 Spring 特性时，需要用 XML 或 Java 进行显式配置；**Spring Boot 旨在简化 Spring 开发（减少配置文件，开箱即用！）**当需要构建 MVC 架构的 Web 程序，还是需要使用 Spring MVC 作为 MVC 框架，只是说 Spring Boot 简化了 Spring MVC 的很多配置



**Core Container** ：Spring 框架的核心模块，也可以说是基础模块，主要提供 **IoC 依赖注入**功能的支持，Spring 其他所有的功能基本都需要依赖于该模块。其中重要组件：

* **spring-core**：Spring 框架基本的核心工具类。

* **spring-beans**：提供对 bean 的创建、配置和管理等功能的支持。

* **spring-context**：提供对国际化、事件传播、资源加载等功能的支持。

* **spring-expression**：提供对表达式语言（Spring Expression Language） SpEL 的支持，只依赖于 core 模块，不依赖于其他模块，可以单独使用

