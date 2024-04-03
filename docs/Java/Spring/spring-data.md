# Spring Data

!!! 摘要
    Spring Data 是 Spring 框架的一个子项目，旨在简化与各种数据存储技术（如关系型数据库、NoSQL数据库、图数据库等）的集成和操作。它提供了一种统一的编程模型和API，使开发人员能够以一致的方式访问和操作不同类型的数据存储。Spring Data 通过提供通用的 CRUD 操作、查询方法、事务管理和数据访问抽象层等功能，简化了数据访问层的开发工作。它还提供了与 Spring 框架其他模块（如Spring Boot、Spring MVC等）的无缝集成，使开发人员能够更轻松地构建全栈应用程序。


## 概念辨析

### 1. JDBC 和 JPA 的区别
JPA（Java Persistence API）和 JDBC（Java Database Connectivity）是 Java 平台上用于与数据库进行交互的两种不同的技术，它们之间有以下区别：  

* JDBC 是一种较低级别的 API，它提供了一组接口和类，允许 Java 应用程序直接与数据库进行交互。使用 JDBC，开发人员需要编写 SQL 查询、执行数据库事务等底层操作。 
*  JPA 则是一种较高级别的 API，它基于 [ORM（对象-关系映射）](https://www.cnblogs.com/qlqwjy/p/7782207.html)的思想，提供了一种更加面向对象的方式来处理数据持久化。开发人员可以使用 JPA 来操作 Java 对象，而不必直接与数据库交互，JPA 会自动将对象与数据库中的表进行映射。

## 参考资料
[1][Spring Data 中文文档](https://springdoc.cn/spring-data/#preface)  
[2][Spring Boot 整合使用 H2 内存数据库](https://springdoc.cn/spring-boot-h2-database/)  
[3][Spring Boot Database Initialization](https://docs.spring.io/spring-boot/docs/current/reference/html/howto.html#howto.data-initialization.using-hibernate)