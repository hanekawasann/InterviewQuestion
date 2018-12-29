[TOC]

## Spring

**Spring框架中的核心思想**

IOC控制反转，DI依赖注入，AOP面向切面

**Spring Bean的作用域**

Singleton（单例）、Prototype（每次从从其中获取bean）、Request（每次请求）、Session（每一个Session）

**Spring事务管理力度的级别，如何管理事务**

方法级别，可分为编程式事务和声明式事务，提供了七种事务传播行为
PROPAGATION_REQUIRED（默认）：有则加入，没有则创建。
PROPAGATION_SUPPORTS：有则加入，没有则执行。
PROPAGATION_MANDATORY：必须已经存在事务并加入，否则抛出异常
PROPAGATION_REQUIRES_NEW：始终创建新事务
PROPAGATION_NOT_SUPPORTED：不支持事务，有则挂起
PROPAGATION_NEVER：永远不需要事务，有则抛出异常
PROPAGATION_NESTED（Spring特有）：有则嵌套子事务，没有则创建
> Struts2是类级别

**Spring Bean的声明周期**

实例化、填充属性、检查Aware接口（设置一些资源：name、factory、applicationContext）、检查BeanPostProcessor接口（传入所有bean）、检查InitializingBean接口（调整bean内部状态）、可用、DisposableBean接口销毁方法、自定义销毁方法。

**Spring MVC生命周期**

请求、DispatcherServlet、HandlerMapping、Controller、ModelAndView、ViewResolver、View

## JDBC

**什么是JDBC?**

JDBC是允许用户在不同数据库之间做选择的一个抽象层。JDBC允许开发者用JAVA写数据库应用程序，而不需要关心底层特定数据库的细节。
> 规范

## Hibernate

**主键生成策略**

assigned（自然主键）：Java程序负责生成标识符。
uuid（代理主键）。
increment（代理主键）：由Hibernate维护一个自增变量。
identity（代理主键）：由底层数据库生成自动增长标识符。
sequence（代理主键）：根据底层数据库序列生成标识符。
hilo（代理主键）：Hibernatetoo通过高低位值来生成标识符。
native（代理主键）：根据底层数据库自动选择identity、sequence、hilo。

**Hibernate对象状态**

临时状态：在数据库中没有对应数据，没有在Hibernate的缓存管理之内（new）
持久化状态：在数据库中有对应数据，在Hibernate的缓存管理之中（get、load）
游离状态：在数据库中没有对应数据，没有在Hibernate的缓存管理之内

**Hibernate对象状态转换**

临时->持久化：save、saveOrUpdate
持久化->临时：delete

持久化->游离：evict、close、clear
游离->持久化：lock、update、saveOrUpdate

游离->临时：delete

**get跟load的区别**

load方法使用延迟加载的机制来加载这个对象，而get方法会直接查询数据库。

**Hibernate缓存**

一级缓存是Session缓存，即事务级别的缓存。Session缓存是必须的，不允许而且事实上也无法卸除。在Session级缓存中，持久化类的每个实例都具有唯一的OID。
二级缓存是SessionFactory缓存，即应用级别的缓存，需要采用适当的并发访问策略。
三级缓存是查询缓存。它主要是针对普通属性结果集的缓存， 而对于实体对象的结果集只缓存id。

## Mybatis

**`$`与`#`号的区别**

`#`将传入的数据都当成一个字符串，会对自动传入的数据加一个双引号，`#`能防止SQL注入，并且具有预编译效果（预编译为`?`），而`$`不会，所以一般用于传入数据库对象，例如传入表名。

**resultType和resultMap的区别**

两者都是表示查询结果集与java对象之间的一种关系，处理查询结果集，映射到java对象。
使用resultType进行输出映射，只有查询出来的列名和bean中的属性名一致，该列才可以映射成功。
resultMap可以对列名和pojo属性名之间作一个映射关系，是更加高级、灵活的映射方案。

**parameterType和parameterMap的区别**

对应resultType和resultMap

## 其他

**ORM的理解**

ORM（Object Relation Mapping）被称为对象关系映射，其中O指的就是java对象，R指的就是关系型数据库，M指的是java对象和关系型数据库之间的映射关系。ORM框架有Hibernate、Mybatis和Ibatis.

**Struts2和SpringMVC的区别**

架构：Struts2是类级别的拦截， 一个类对应一个request上下文，请求参数通过setter方法。SpringMVC是方法级别的拦截，一个方法对应一个request上下文（请求参数通过方法形参）。
实现：SpringMVC的入口是servlet，而Struts2是filter。
配置：SpringMVC在Handler、验证、处理、响应的配置上都可以使用注解，而且与Spring无缝整合，几乎零配置，相比而言，Struts2需要XML配置，而且非常繁琐。

**Hibernate和Mybatis的区别**

Hibernate是将数据库中的数据表映射为持久层的java对象，实现数据表的完整性控制。MyBatis是将sql语句中的输入参数和输出参数映射为java对象，获得了更灵活和响应性能更快的优势。 
简单性、灵活性、移植性

**JDBC、Hibernate、Mybatis的区别**

JDBC是较底层的持久层操作方式，而Hibernate和MyBatis都是在JDBC的基础上进行了封装使其更加方便程序员对持久层的操作。 
Hibernate是将数据库中的数据表映射为持久层的java对象，实现数据表的完整性控制。MyBatis是将sql语句中的输入参数和输出参数映射为java对象，获得了更灵活和响应性能更快的优势。 
如果进行底层编程，而且对性能要求极高的话，应该采用JDBC的方式。如果要对数据库进行完整性控制的话建议使用Hibernate。如果要灵活使用sql语句的话建议采用MyBatis框架。

**webservice是什么**

webservice是一种跨编程语言和跨操作系统的远程调用技术，遵循SOPA/WSDL规范。

**springCloud是什么**

springcloud是一个微服务框架，并提供全套分布式系统解决方案。
