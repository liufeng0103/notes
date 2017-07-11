# Spring
[spring.io](http://spring.io/)

## 文章
- [跟开涛学SpringMVC](http://jinnianshilongnian.iteye.com/category/231099)
- [Thymeleaf 模板的使用](http://www.jianshu.com/p/ed9d47f92e37)
- [Spring Cloud构建微服务架构（一）服务注册与发现](http://blog.didispace.com/springcloud1/)
- [spring-data-jpa 多条件查询 学习记录](http://blog.csdn.net/lsk12162012/article/details/50442792)
- [怎么在Spring Controller里面返回404](http://jaskey.github.io/blog/2014/09/27/how-to-return-404-in-spring-controller/)
- [web.xml中出现<servlet-name>default</servlet-name>是什么意思](http://blog.csdn.net/hello5orld/article/details/9407905)
- [Spring Boot中使用Redis数据库](http://blog.didispace.com/springbootredis/)

spring只对RuntimeException进行事务回滚

## 配置文件
```xml

```

## 注解
```java
@Controller
@Service
@Component
@Repository
```

## 代码
```java
// 获取spring的context
ApplicationContext context = new ClassPathXmlApplicationContext("spring-config.xml");
ApplicationContext context = new FileSystemXmlApplicationContext("WebContent/WEB-INF/applicationContext.xml");
@ContextConfiguration({"classpath:applicationContext.xml"})
@ContextConfiguration({"file:WebContent/WEB-INF/applicationContext.xml"})

// 在Spring项目中获取classpath下的资源文件
File cfgFile = ResourceUtils.getFile("classpath:test.txt");
Resource fileRource = new ClassPathResource("test.txt");  
```

## SpringBoot
ctrl+shift+f9 编译 热更新thymeleaf模板

启动
1. 通过main启动
2. mvn spring-boot:run
3. java -jar xxx.jar --spring.profiles.active=prod

## SpringMVC

### web.xml配置
```xml
<!-- 在web.xml中配置SpringMVC前端控制器 -->
<servlet>  
    <servlet-name>springmvc</servlet-name>  
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>  
    <!-- 启动容器时初始化该Servlet -->
    <load-on-startup>1</load-on-startup>  
    <!-- 自己指定配置文件，默认使用classpath下的[DispatcherServlet的Servlet名字，在这里是springmvc]-servlet.xml -->
    <init-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:spring-mvc.xml</param-value>
    </init-param>
</servlet>  
<servlet-mapping>  
    <servlet-name>springmvc</servlet-name>  
    <url-pattern>/</url-pattern>  
</servlet-mapping>
<!-- org.springframework.web.filter.CharacterEncodingFilter用于解决POST方式造成的中文乱码问题 -->
<filter>  
    <filter-name>CharacterEncodingFilter</filter-name>  
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>  
    <init-param>  
        <param-name>encoding</param-name>  
        <param-value>utf-8</param-value>  
    </init-param>  
</filter>  
<filter-mapping>  
    <filter-name>CharacterEncodingFilter</filter-name>  
    <url-pattern>/*</url-pattern>  
</filter-mapping>
```

### SpringMVC配置
```xml
<!-- 自动扫描该包，使SpringMVC认为包下用了@Controller和@RestController注解的类是控制器 -->
<context:component-scan base-package="com.bnade.wow.controller" />

<!-- 配置注解的处理器映射器和处理器适配器 -->
<mvc:annotation-driven />

<!-- 直接配置path的view name和ParameterizableViewController类似，收到相应请求后直接选择相应的视图 -->
<mvc:view-controller path="/" view-name="redirect:/index" />

<!-- 定义无Controller的path到view直接映射，逻辑静态资源路径到物理静态资源路径的支持 -->
<mvc:resources mapping="/views/**" location="/WEB-INF/views/" />

<!-- 当在web.xml中DispatcherServlet使用<url-pattern>/</url-pattern> 映射时，能映射静态资源.当Spring Web MVC框架没有处理请求对应的控制器时（如一些静态资源），转交给默认的Servlet来响应静态文件，否则报404找不到资源错误 -->
<mvc:default-servlet-handler>

<!-- ViewResolver, InternalResourceViewResolver：用于支持Servlet、JSP视图解析 -->  
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">  
    <!-- viewClass：JstlView表示JSP模板页面需要使用JSTL标签库，classpath中必须包含jstl的相关jar包 -->
    <property name="viewClass" value="org.springframework.web.servlet.view.JstlView"/>  
    <!-- prefix和suffix：查找视图页面的前缀和后缀，比如传进来的逻辑视图名为hello，则该jsp视图页面应该存放在“WEB-INF/views/hello.jsp -->
    <property name="prefix" value="/WEB-INF/views/"/>  
    <property name="suffix" value=".jsp"/>  
</bean>

<!-- 注册拦截器, 自定义拦截器通过继承HandlerInterceptorAdapter实现 -->
<mvc:interceptors></mvc:interceptors>
```

### 注解
```java
// 用于标识是处理器类
@Controller
// 相当于Controller和ResponseBody的组合注解
@RestController
// 请求到处理器功能方法的映射规则
@RequestMapping
// 映射多个url
@RequestMapping(value={"/member/remove","/member/delete"})
// 请求参数到处理器功能处理方法的方法参数上的绑定
@RequestParam
// 请求参数到命令对象的绑定
@ModelAttribute
// 用于声明session级别存储的属性，放置在处理器类上，通常列出模型属性（如@ModelAttribute）对应的名称，则这些属性会透明的保存到session中
@SessionAttributes
// 自定义数据绑定注册支持，用于将请求参数转换到命令对象属性的对应类型
@InitBinder
// cookie数据到处理器功能处理方法的方法参数上的绑定
@CookieValue
// 请求头（header）数据到处理器功能处理方法的方法参数上的绑定
@RequestHeader
// 请求的body体的绑定（通过HttpMessageConverter进行类型转换）
@RequestBody
// 处理器功能处理方法的返回值作为响应体（通过HttpMessageConverter进行类型转换）
@ResponseBody
// 定义处理器功能处理方法/异常处理器返回的状态码和原因
@ResponseStatus
// 注解式声明异常处理器
@ExceptionHandler
// 请求URI中的模板变量部分到处理器功能处理方法的方法参数上的绑定，从而支持RESTful架构风格的URI
@PathVariable
// 验证元数据
@Valid
// 用于在基于Java类定义Bean配置中开启MVC支持，和XML中的<mvc:annotation-driven>功能一样
@EnableWebMvc
```

### 代码
```java
// ModelAndView
//1、收集参数、验证参数  
//2、绑定参数到命令对象  
//3、将命令对象传入业务对象进行业务处理  
//4、选择下一个页面  
ModelAndView mv = new ModelAndView();  
//添加模型数据 可以是任意的POJO对象  
mv.addObject("message", "Hello World!");  
//设置逻辑视图名，视图解析器会根据该名字解析到具体的视图页面  
mv.setViewName("hello")

// 可以使用RestTemplate来调用restfull
```

### SpringMVC配置文件示例
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans
	xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:tx="http://www.springframework.org/schema/tx"
	xmlns:context="http://www.springframework.org/schema/context"  
	xmlns:mvc="http://www.springframework.org/schema/mvc"  
	xsi:schemaLocation="http://www.springframework.org/schema/beans
	http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
	http://www.springframework.org/schema/tx
	http://www.springframework.org/schema/tx/spring-tx-3.0.xsd
	http://www.springframework.org/schema/context
    http://www.springframework.org/schema/context/spring-context-3.0.xsd
	http://www.springframework.org/schema/mvc
    http://www.springframework.org/schema/mvc/spring-mvc-3.0.xsd">


    <!-- 自动扫描包，可以写多个 -->
    <context:component-scan base-package="com.xxx,com.xxx.session,com.xxx.xxx" ></context:component-scan>

    <!-- 多视图处理器 -->
    <bean class="com.xxx.core.web.MixedViewResolver">
		<property name="resolvers">
			<map>
				<entry key="jsp">
					<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
						<property name="prefix" value="/WEB-INF/jsp/"/>
						<property name="viewClass" value="org.springframework.web.servlet.view.JstlView"></property>
					</bean>
				</entry>
				<entry key="ftl">
					<bean class="org.springframework.web.servlet.view.freemarker.FreeMarkerViewResolver">
						<property name="cache" value="true"/>
						<property name="contentType" value="text/html;charset=UTF-8"></property>
						<!-- 宏命令的支持  -->  
						<property name="exposeSpringMacroHelpers" value="true"/>
						<property name="viewClass" value="org.springframework.web.servlet.view.freemarker.FreeMarkerView"/>
						<property name="requestContextAttribute" value="rc"></property>
					</bean>
				</entry>
			</map>
		</property>
	</bean>

	<!-- freemarker config -->
    <bean id="freeMarkerConfigurer" class="org.springframework.web.servlet.view.freemarker.FreeMarkerConfigurer">
        <property name="templateLoaderPath" value="/WEB-INF/ftl/" />
        <property name="freemarkerSettings">
            <props>
                <prop key="template_update_delay">5</prop>
                <prop key="default_encoding">UTF-8</prop>
                <prop key="locale">zh_CN</prop>
            </props>
        </property>
    </bean>

    <!-- 日志拦截器-->
    <bean id="logNDCInteceptor" class="com.xxx.core.web.LogNDCInteceptor"/>

    <!-- 权限拦截器-->
    <bean id="myPermissionsInteceptor" class="com.xxx.userplatform.mvc.MyPermissionsInteceptor"></bean>

    <!-- RequestHelper拦截器-->
    <bean id="myRequestHelperInteceptor" class="com.xxx.core.web.MyRequestHelperInteceptor"></bean>

    <!-- 用户信息拦截器-->
    <bean id="myUserInfoInteceptor" class="com.xxx.userplatform.mvc.MyUserInfoInteceptor"></bean>

    <!-- 注解请求映射  -->
    <bean class="org.springframework.web.servlet.mvc.annotation.DefaultAnnotationHandlerMapping">        
		<property name="interceptors">
		    <list>  
		    	<ref bean="logNDCInteceptor"/>   <!-- 日志拦截器 -->
		    	<ref bean="myRequestHelperInteceptor"/>   <!-- RequestHelper拦截器-->
		    	<ref bean="myPermissionsInteceptor"/>  <!-- 权限拦截器-->
		    	<ref bean="myUserInfoInteceptor"/>  <!-- 用户信息拦截器-->
		    </list>        
		</property>        
	</bean>  	
	<bean class="org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter">
		<property name="messageConverters">  
			<list>  
				<ref bean="byteArray_hmc" />  
				<ref bean="string_hmc" />  
				<ref bean="resource_hmc" />  
				<ref bean="source_hmc" />  
				<ref bean="xmlAwareForm_hmc" />  
				<ref bean="jaxb2RootElement_hmc" />  
				<ref bean="jackson_hmc" />  
			</list>  
		</property>  
	</bean>  
	<bean id="byteArray_hmc" class="org.springframework.http.converter.ByteArrayHttpMessageConverter" /><!-- 处理.. -->
	<bean id="string_hmc" class="org.springframework.http.converter.StringHttpMessageConverter" /><!-- 处理.. -->
	<bean id="resource_hmc" class="org.springframework.http.converter.ResourceHttpMessageConverter" /><!-- 处理.. -->
	<bean id="source_hmc" class="org.springframework.http.converter.xml.SourceHttpMessageConverter" /><!-- 处理.. -->
	<bean id="xmlAwareForm_hmc" class="org.springframework.http.converter.xml.XmlAwareFormHttpMessageConverter" /><!-- 处理.. -->
	<bean id="jaxb2RootElement_hmc" class="org.springframework.http.converter.xml.Jaxb2RootElementHttpMessageConverter" /><!-- 处理.. -->
	<bean id="jackson_hmc" class="org.springframework.http.converter.json.MappingJacksonHttpMessageConverter" /><!-- 处理json-->


	<!-- 总错误处理-->
	<bean id="exceptionResolver" class="org.springframework.web.servlet.handler.SimpleMappingExceptionResolver">

		<property name="exceptionMappings">
			<props>
			<!-- 上传文件大于最大尺寸后转向出错页面 -->
				<prop key="org.springframework.web.multipart.MaxUploadSizeExceededException">
					redirect:/uploadError.jsp
				</prop>
			</props>
		</property>
		<property name="defaultErrorView">  
		 	<value>forward:/error.jsp</value>
		</property>
		<property name="defaultStatusCode">  
		 	<value>200</value>
		</property>		 	
		<property name="warnLogCategory">  
		 	<value>org.springframework.web.servlet.handler.SimpleMappingExceptionResolver</value>
		</property>		 	

	</bean>

	<!-- 允许对静态资源文件的访问 -->
	<mvc:default-servlet-handler/>

	<!-- 数据源 ,DBCP连接池-->
	<bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
		<property name="driverClassName" value="oracle.jdbc.driver.OracleDriver"/>
		<property name="url" value="jdbc:oracle:thin:@192.168.3.141:1521:xxx"/>
		<property name="username" value="xxxdb"/>
		<property name="password" value="xxxdb"/>
		<property name="initialSize" value="2"/>
		<property name="maxActive" value="10"/>
		<property name="maxIdle" value="10"/>
		<property name="maxWait" value="1000"/>
		<property name="poolPreparedStatements" value="true"/>
	</bean>

	<!-- JNDI数据源
	<bean id="dataSource" class="org.springframework.jndi.JndiObjectFactoryBean">
		<property name="jndiName">
			<value>jdbc/xxx</value>
		</property>
	</bean>
	-->

	<!-- JDBC模板 -->
	<bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate" >
		<property name="dataSource" ref="dataSource" />
	</bean>
	<!-- 事务管理器 -->
	<bean id="transactionManager"
		class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
		<property name="dataSource" ref="dataSource" />
	</bean>
	<!-- 用注解来实现事务管理 -->
	<tx:annotation-driven transaction-manager="transactionManager" proxy-target-class="true"/>

    <!-- 用于持有ApplicationContext,可以使用SpringContextHolder.getBean('xxxx')的静态方法得到spring bean对象 -->  
    <bean class="com.xxxxx.SpringContextHolder" lazy-init="false" />  

</beans>
```
