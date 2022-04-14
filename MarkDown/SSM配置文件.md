# SSM配置文件

### web.xml
开启监听
```xml
<listener>
    <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
</listener>
```
初始化全局参数配置
```xml
<context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>classpath:application.xml</param-value>
</context-param>
```
配置Servlet
```xml
 <servlet>
    <servlet-name>SpringMVC</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <!--初始化参数-->
    <init-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:spring/spring-*.xml</param-value>
    </init-param>
    <!--
        装载Servlet顺序
        值为自然数(0或正整数)时：Servlet从小到大的顺序装载
        值为负数或未定义时：Servlet在Web客户端首次访问这个Servlet加载(lazyload)
    -->
    <load-on-startup>1</load-on-startup>
</servlet>
<servlet-mapping>
    <servlet-name>SpringMVC</servlet-name>
    <!--拦截所有请求-->
    <url-pattern>/</url-pattern>
</servlet-mapping>
```

### application.xml
扫描除controller层其他层级
```xml
<context:component-scan base-package="redcrazyghost">
    <!--排除controller层-->
    <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
</context:component-scan>
```
获取jdbc配置数据
```xml
<context:property-placeholder location="classpath:jdbc.properties" />
```
配置数据源(本文使用的是alibaba druid 数据库连接池)
```xml
<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource" init-method="init" destroy-method="close"
        p:url="${jdbc.url}"
        p:username="${jdbc.username}"
        p:password="${jdbc.password}"
/>
```
配置连接工厂
```xml
<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean"
          p:dataSource-ref="dataSource"
          p:configLocation="classpath:/mybatis-config.xml"
    />
```
配置MapperScanner扫描Dao层
```xml
<bean class="org.mybatis.spring.mapper.MapperScannerConfigurer"
          p:basePackage="redcrazyghost.dao"
    />
```

### spring-mvc.xml
> 配置controller层

扫描controller层
```xml
<context:component-scan base-package="redcrazyghost.controller"/>
```
开启SpringMVC注解
```xml
<mvc:annotation-driven />
```
开启SpringMVC默认拦截器(开放默认静态文件)
```xml
<mvc:default-servlet-handler/>
```
配置InternalResourceViewResolver
```xml
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"
        p:prefix="/WEB-INF/views/"
        p:suffix=".jsp"
        p:viewClass="org.springframework.web.servlet.view.JstlView"
/>
```