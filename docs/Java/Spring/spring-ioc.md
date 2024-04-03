# Spring 基础（二）IOC
## 一、IoC 设计思想
**IoC（Inversion of Control 控制反转）** 是一种设计思想，而不是一个具体的技术实现。IoC 的思想就是将原本在程序中手动创建对象的控制权，交由 Spring 框架来管理。不过， IoC 并非 Spring 特有，在其他语言中也有应用。

**控制**：指的是创建（实例化、管理）对象权力

**反转**：指将控制权交给外部环境（Spring 框架、IoC 容器）

将对象之间的相互 **依赖关系** 交给 IoC 容器来管理，并由 **IoC 容器** 完成对象的 **注入**。这样可以很大程度上简化应用的开发，把应用从复杂的依赖关系中解放出来。 IoC 容器就像是一个工厂一样，当我们需要创建一个对象的时候，只需要配置好配置文件/注解即可，完全不用考虑对象是如何被创建出来的。

在 Spring 中， IoC 容器是 Spring 用来实现 IoC 的载体， IoC 容器实际上就是个 **Map（key，value**），Map 中存放的是各种对象。

## 二、Spring Bean
Bean 代指的就是那些被 IoC 容器所管理的对象。配置元数据 用于定义 IoC 容器所需要管理的对象，配置元数据可以是 XML 文件、注解或者 Java 配置类。 

### 1. 声明 Bean 的注解
**@Component**：通用的注解，可标注任意类为 Spring 组件。如果一个 Bean 不知道属于哪个层，可以使用该注解标注。

**@Repository**： 对应持久层即 Dao 层，主要用于数据库相关操作。

**@Service**： 对应服务层，主要涉及一些复杂的逻辑，需要用到 Dao 层。

**@Controller**：对应 Spring MVC 控制层，主要用于接受用户请求并调用 Service 层返回数据给前端页面。

> @Componen 是通用注解，其他注解是它的特例，这些注解的区别在于它们的语义和用途，但它们都属于 Spring 的组件扫描和管理范围内，并且能够使 Spring 容器能够识别和实例化这些类

### 2. @Bean 和 @Component  的区别
@Component 注解作用于类，而 @Bean 注解作用于方法。

@Component 通常是通过类路径扫描来自动侦测以及自动装配到 Spring 容器中（我们可以使用@ComponentScan 注解定义要扫描的路径从中找出标识了需要装配的类自动装配到 Spring 的 bean 容器中）。

@Bean 注解通常是我们在标有该注解的方法中定义产生这个 bean, @Bean 告诉了 Spring 这是某个类的实例，当我需要用它的时候还给我。

@Bean 注解比 @Component 注解的自定义性更强，而且很多地方我们只能通过 @Bean 注解来注册 bean。比如当我们引用第三方库中的类需要装配到 Spring容器时，则只能通过 @Bean 来实现。

### 3. @AutoWired 和 @Resource 的区别
* @Autowired 是 Spring 提供的注解，@Resource 是 JDK 提供的注解。

* Autowired 默认的注入方式为 **byType**（根据类型进行匹配），@Resource 默认注入方式为 **byName**（根据名称进行匹配）。当一个接口存在多个实现类的情况下，@Autowired 和@Resource都需要通过名称才能正确匹配到对应的 Bean。

* Autowired 可以通过 @Qualifier 注解来显式指定名称，@Resource可以通过 name 属性来显式指定名称

* @Autowired 支持在 **构造函数、方法、字段** 和 **参数** 上使用。@Resource 主要用于 **字段** 和 **方法** 上的注入，不支持在构造函数或参数上使用。

### 4. Bean 的作用域
* **singleton** : IoC 容器中只有唯一的 bean 实例。Spring 中的 bean 默认都是单例的，是对单例设计模式的应用。

* **prototype** : 每次获取都会创建一个新的 bean 实例。也就是说，连续 getBean() 两次，得到的是不同的 Bean 实例。

* **request** （仅 Web 应用可用）: 每一次 HTTP 请求都会产生一个新的 bean（请求 bean），该 bean 仅在当前 HTTP request 内有效。

* **session** （仅 Web 应用可用） : 每一次来自新 session 的 HTTP 请求都会产生一个新的 bean（会话 bean），该 bean 仅在当前 HTTP session 内有效。

* **application/global-session** （仅 Web 应用可用）：每个 Web 应用在启动时创建一个 Bean（应用 Bean），该 bean 仅在当前应用启动时间内有效。

* **websocket** （仅 Web 应用可用）：每一次 WebSocket 会话产生一个新的 bean。

### 5. Bean 的线程安全问题
Spring 框架中的 Bean 是否线程安全，取决于其 **作用域** 和 **状态**。

prototype 作用域下，每次获取都会创建一个新的 bean 实例，不存在资源竞争问题，所以不存在线程安全问题。

singleton 作用域下，IoC 容器中只有唯一的 bean 实例，可能会存在资源竞争问题（取决于 Bean 是否有状态）。如果这个 bean 是有状态的话，那就存在线程安全问题（有状态 Bean 是指包含可变的成员变量的对象）。

对于有状态单例 Bean 的线程安全问题，常见的有两种解决办法：

* 在 Bean 中尽量避免定义可变的成员变量。

* 在类中定义一个 **ThreadLocal** 成员变量，将需要的可变成员变量保存在 ThreadLocal 中（推荐的一种方式）。

## 三、Bean   生命周期 —— 源码解析

