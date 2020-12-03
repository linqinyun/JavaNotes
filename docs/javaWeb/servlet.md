# servlet
1. 了解什么是bs架构模式，浏览器和服务器
2. 掌握servlet开发技巧
3. 掌握servlet原理
- 软件发展史
1. 单机时代

    优点 安装简单，使用方便 ，结构简单  
    缺点 不易共享 不够安全

2. 联机时代 cs架构 客户端 服务器

    优点 数据共享方便，安全性高  
    缺点 必须要下载客户端 不易维护更新

3. 互联网时代 bs架构 浏览器 服务器

    优点 方便快捷 开发简单 数据容易共享  
    缺点 执行速度，用户体验差一点

## 请求与响应：
    从浏览器发出送给服务区的数据包称为请求（Request）
    从服务器返回给浏览器的结果称为“响应（Response ）”
    J2EE（Java 2 Platform Enterprise Edition）是指Java 2 企业版
    开发BS应用程序就是J2EE最核心的功能
## J2EE的模块：
    Servlet JSP JDBC XML EJ（企业级Java Bean） RMI（远程调用） JNDI（目录服务） JMS（消息服务） JTA（事务管理） JavaMail（发送/接受Email） JAF（安全架构） CORBA（CORBA集成） JTS（CORBA事务监控）
    Apache Tomcat：Web应用服务器程序
## J2EEE与TOMCAT关系：
    J2EE是一组技术规范与指南，具体实现是由软件厂商决定。
    Tomcat是J2EE Web （Servlet与JSP）标准的实现者
    J2SE是J2EE的运行基石，运行Tomcat离不开J2SE