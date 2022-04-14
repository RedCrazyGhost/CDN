# SSM
Spring + SpringMVC + Mybatis

Webapp web.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <!--WEB 应用名称-->
    <display-name>ssm</display-name>

    <!--WEB 应用描述-->
    <description>Spring+SpringMVC+Mybatis Web应用</description>

    <!--首先加载Spring容器加载器-->
    <!--
        servlet API的版本2.3增加了对事件监听程序的支持
        事件监听程序在建立、修改、删除会话或servlet环境时得到通知
        Listener元素指出事件监听程序类
    -->
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>

    <servlet>
        <servlet-name>SpringMVC</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:spring/application.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>

    
</web-app>
```

Maven 依赖 POM.xml 
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>redcrazyghost</groupId>
    <artifactId>ssm</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
        <springframework-version>5.3.18</springframework-version>
        <log4j-version>2.17.2</log4j-version>
        <druid-version>1.2.8</druid-version>
        <mysql-version>8.0.28</mysql-version>
        <mybatis-veriosn>3.5.9</mybatis-veriosn>
        <mybatis-spring-version>2.0.7</mybatis-spring-version>
    </properties>


    <dependencies>

        <!--SpringMVC依赖-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>${springframework-version}</version>
        </dependency>
        
        <!--log4j日志框架-->
        <dependency>
            <groupId>org.apache.logging.log4j</groupId>
            <artifactId>log4j-core</artifactId>
            <version>${log4j-version}</version>
        </dependency>
        <dependency>
            <groupId>org.apache.logging.log4j</groupId>
            <artifactId>log4j-api</artifactId>
            <version>${log4j-version}</version>
        </dependency>
        
        <!--Java MySQL 连接驱动-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>${mysql-version}</version>
        </dependency>
        
        <!--alibaba druid 数据库连接池-->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>${druid-version}</version>
        </dependency>
        
        <!--Spring-JDBC框架-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>${springframework-version}</version>
        </dependency>
        
        <!--Mybatis 数据库框架-->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>${mybatis-veriosn}</version>
        </dependency>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis-spring</artifactId>
            <version>${mybatis-spring-version}</version>
        </dependency>
        
    </dependencies>

</project>
```
