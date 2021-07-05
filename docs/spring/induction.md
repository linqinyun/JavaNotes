# Spring从入门到进阶

## Spring入门

### Spring概述
- Spring是一个开源框架
- Spring为简化企业级应用开发而生，使用Spring可以使简单的JavaBean实现以前只有EJB才能实现的功能
- Spring是JavaSE/EE的一站式框架
### Spring的优点
* 方便解耦，简化开发
  - Spring就是一个大工厂，可以将所有对象创建和依赖关系维护，交给Spring管理
* AOP编程的支持
  - Spring提供面向切面编程，可以方便的实现对程序进行权限拦截、运行监控等。
* 声明式事务的支持
  - 只需要通过配置就可以完成对事务的管理，而无需手动编程
* 方便程序的测试
  - Spring对Junit4支持，可以通过注解方便的测试Spring程序
* 方便集成各种优秀框架
  - Spring不排斥各种优秀的开源框架，其内部提供了对各种优秀框架（Struts、Hibernate、MyBatis等）的直接支持
* 降低JavaEE API的使用难度
  - Spring对JavaEE开发中非常难用的一些API（JDBC、JavaMail、远程调用等），都提供从封装，使这些API应用难度大大降低

### Spring IOC的底层原理实现
- OCP原则：open close原则，对程序扩展是open，对修改程序代码是close。尽量做到不修改程序的源码，实现对程序的扩展。
- 工厂模式
- 工厂+反射+配置文件
- IoC（Inversion of Control）的直译是“控制反转”，就是将bean交给容器来创建，而不是直接在需要的时候通过new来创建。
- DI（Dependency Injection）的直译是依赖注入，也称为被动接受依赖，就是在需要某个bean的时候容器将对象注入进来（可以简单理解为对象实例化）。

### Spring IOC入门流程
- 下载Spring开发包
- 复制Spring开发jar包到工程
- 理解IOC控制反转和DI依赖注入
- 编写Spring核心配置文件
- 在程序中读取Spring配置文件，通过Spring框架获得Bean，完成相应操作

### IOC与DI
- IOC Inverse of Control 反转控制的概念，就是将原本在程序中手动创建的UserService对象的控制权，交由Spring框架管理
- 创建UserService对象的控制权被反转到了Spring框架
- DI Dependency Injection 依赖注入的概念，就是在Spring创建这个对象的过程中，将这个对象所依赖的属性注入进去

## Spring Bean管理

### Spring的工厂类
### Spring的Bean管理（XML方式）
#### 三种实例化Bean的方式
- 使用类构造器实例化（默认无参数）
- 使用静态工厂方法实例化（简单工厂模式）
- 使用实例工厂方法实例化（工厂方法模拟）
### Bean的配置
- id与name
  - 一般情况下，装配一个Bean时，通过指定一个id属性作为Bean的名称
  - id属性在IOC容器中必须时唯一的
  - 如果Bean的名称中含有特殊字符，就需要使用name属性
- class
  - class用于设置一个类的完全路径名称，主要作用是IOC容器生成类的实例
- scope作用域
### Spring容器中Bean的生命周期
Spring初始化bean或销毁bean时，有时需要做一些处理工作，因此spring可以在创建和销毁bean的时候调用bena的两个生命周期方法。
1. instantiate bean对象实例化
2. populate properties 封装属性
3. 如果Bean实现BeanNameAware执行setBeanName
4. 如果Bean实现BeanFactoryAware或者ApplicationContextAware设置工厂setBeanFactory或者上下文对象setApplicationContext
5. 如果存在类实现BeanPostProcessor（后处理Bean），执行postProcessBeforeInitialization
6. 如果Bean实现InitializingBean执行afterPropertiesSet
7. 调用\<bean init-method="init">指定初始化方法
8. 如果存在类实现BeanPostProcessor（处理Bean），执行postProcessAfterInitialization
9. 执行业务处理
10. 如果Bean实现DisposableBean执行destroy
11. 调用\<bean destroy-method="customerDestroy">指定销毁方法customerDestroy
12. 项目使用

## Spring AOP

## 基于AspectJ的AOP开发

## JDBC Template

## Spring事务管理

## 实例项目：人员管理系统