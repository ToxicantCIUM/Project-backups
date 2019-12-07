## Spring

1.导入jar包

2.引入配置xml配置文件（applicationContext.xml）

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
    http://www.springframework.org/schema/aop
    http://www.springframework.org/schema/aop/spring-aop.xsd
     http://www.springframework.org/schema/tx
        http://www.springframework.org/schema/tx/spring-tx.xsd
">
    <!--注解扫描-->
    <context:component-scan base-package="com.ssm"/>
    
</beans>
```

3.在web.xml中配置核心过滤器

```
<!--Spring的核心监听器-->
<listener>
    <listener-class>
        org.springframework.web.context.ContextLoaderListener
    </listener-class>
</listener>
<!--
 加载Spring的配置文件的路径的
 默认加载的/WEB-INF/applicationContext.xml
 -->
<context-param>
    <param-name> contextConfigLocation</param-name>
    <param-value>classpath:applicationContext.xml</param-value>
</context-param>
```

**spring注解使用**

声明Bean的注解：
@Component : 组件,没有明确的角色
@Service : 在业务逻辑层(service层)使用
@Repository : 在数据访问层(dao层)使用.
@Controller : 在展现层(MVC--SpringMVC)使用

注入Bean的注解:
@Aautowired : Spring提供的注解.
@Inject : JSR-330提供的注解
@Resource : JSR-250提供的注解
@Primary 注入时优先使用此注解下的实现类，对应org.springframework.beans.factory.NoUniqueBeanDefinitionException异常

## SpringMVC

1.引入jar包

2.引入sqlMapConfig.xml配置文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <settings>
        <setting name="logImpl" value="STDOUT_LOGGING"/>
    </settings>
    <typeAliases>
        <!-- 批量别名定义，扫描整个包下的类，别名为类名（大小写不敏感） -->
        <package name="com.ssm.domain" />
    </typeAliases>
</configuration>
```

3.在web.xml配置文件中配springMVC的前段过滤器，并解决下post请求乱码问题

```xml
<!-- 解决post乱码问题 -->
<filter>
    <filter-name>encoding</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <!-- 设置编码参是UTF8 -->
    <init-param>
        <param-name>encoding</param-name>
        <param-value>UTF-8</param-value>
    </init-param>
</filter>
<filter-mapping>
    <filter-name>encoding</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>

<!-- 配置SpringMVC前端控制器 -->
<servlet>
    <servlet-name>mySpringMVC</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <!-- 指定SpringMVC配置文件 -->
    <!-- SpringMVC的配置文件的默认路径是/WEB-INF/${servlet-name}-servlet.xml -->
    <init-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:springmvc.xml</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
</servlet>
<servlet-mapping>
    <servlet-name>mySpringMVC</servlet-name>
    <!-- 拦截所有,不包括jsp,包含.js .png.css     建议使用  -->
    <url-pattern>/</url-pattern>
</servlet-mapping>
```

## mybatis

1.引入jar包

2.创建sqlMapConfig.xml配置文件

```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <settings>
        <setting name="logImpl" value="STDOUT_LOGGING"/>
    </settings>
    <typeAliases>
        <!-- 批量别名定义，扫描整个包下的类，别名为类名（大小写不敏感） -->
        <package name="com.ssm.domain" />
    </typeAliases>
</configuration>
```

3.在applicationContext.xml中配置相关信息

（第二步可以不做，直接在mybatis工程中用property来配置也行）

```
<!--mybatis-spring整合-->
<!--加载数据库属性文件-->
<context:property-placeholder location="classpath:db.properties"/>
<!--连接池-->
<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
    <property name="driverClassName" value="${jdbc.driver}" />
    <!--属性文件当中的名称不能和name名称一样-->
    <property name="url" value="${jdbc.url}" />
    <property name="username" value="${jdbc.username}" />
    <property name="password" value="${jdbc.password}" />
</bean>
<!-- 配置事务管理器 -->
<bean id="transactionManager"
      class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
    <!-- 数据源 -->
    <property name="dataSource" ref="dataSource" />
</bean>
<!-- 开启注解事务 -->
<tx:annotation-driven transaction-manager="transactionManager"/>


<!-- Mybatis的工厂 -->
<bean id="sqlSessionFactoryBean" class="org.mybatis.spring.SqlSessionFactoryBean">
    <property name="dataSource" ref="dataSource"/>
    <!-- 核心配置文件的位置 -->
    <property name="configLocation" value="classpath:sqlMapConfig.xml"/>
    <!--配置mapper映射文件的路径-->
    <property name="mapperLocations" value="classpath:com/ssm/mapper/*.xml"/>
</bean>
<!-- 配置Mapper接口扫描 -->
<bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
    <!-- 配置Mapper扫描包 -->
    <property name="basePackage" value="com.ssm.mapper" />
</bean>
```

**需要注意两个地方**

a.配置Mapper接口扫描，需要指定一下扫描那个包下的xml文件

b.核心配置文件的位置和mapper映射文件的位置  * 号代表任意



### 测试

1.创建一个与数据库的关系映射domain（javabean）提供get，set方法

2.创建一个Controller控制器

```
@Controller
public class CustomerController {
    @Autowired
    private CustomerService customerService;

    @RequestMapping("saveCustomer")
    public String addcustomer(Customer customer){
        System.out.println("CustomerController===="+customer);
        customerService.saveCustomer(customer);
        return "result";
    }
}
```



3.创建个业务层

```
@Service("customerService")
@Transactional
public class CustomerServiceImpl implements CustomerService {
    @Autowired
    private CustomerMapper customerMapper;

    @Override
    public void saveCustomer(Customer customer) {
        customerMapper.insertCustomer(customer);
    }
}

```



4.创建个mapper及同名的xml

5.通过测试页面的form表单测试ssm整合是否成功

```
<form action="${pageContext.request.contextPath}/saveCustomer">
  名字:<input type="text" name="cust_name"> <br>
  职业:<input type="text" name="cust_profession"/> <br>
  电话: <input type="text" name="cust_phone"/> <br>
  邮件: <input type="text" name="email"/> <br>
  <input type="submit" value="添加">
</form>
```

**注意**

由于在springmvc.xml文件中配置了视图解析器，所以return 结果页时只需要写名称

（写全路径的忽视本条）

```
<!--配置视图解析器-->
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="prefix" value="/WEB-INF/view/"/>
    <property name="suffix" value=".jsp"/>
</bean>
```

# shiro

1.在pom文件中加入需要的jar包依赖

2.在web.xml文件中配置过滤器拦截处理所有的请求

```
  <!--shiro过滤器-->
  <!-- 拦截到所有请求,使用spring一个bean来进行处理 -->
  <filter>
    <filter-name>shiroFilter</filter-name>
    <filter-class>org.springframework.web.filter.DelegatingFilterProxy</filter-class>
    <!-- 是否filter中的init和 destroy-->
    <init-param>
      <param-name>targetFilterLifecycle</param-name>
      <param-value>true</param-value>
    </init-param>
  </filter>
  <filter-mapping>
    <filter-name>shiroFilter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>
</web-app>
```

3.在sprig中配置shiro过滤器和安全管理器

```
<!-- 配置shiro过滤器 -->
<bean id="shiroFilter" class="org.apache.shiro.spring.web.ShiroFilterFactoryBean">
    <property name="securityManager" ref="securityManager"></property>
    <!-- 配置shiro过滤器pattern -->
    <property name="filterChainDefinitions">
        <value>
            /static/** = anon   <!--不需要登录验证-->
            /login.jsp = anon   <!--不需要登录验证-->
            /**=authc     <!--除指定请求外,其它所有的请求都需要身份验证-->
        </value>
    </property>
</bean>
<!-- 配置shiro安全管理器 -->
<bean id="securityManager" class="org.apache.shiro.web.mgt.DefaultWebSecurityManager"></bean>

```

