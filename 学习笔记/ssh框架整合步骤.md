**struct2框架步骤**

1.导入jar包

2.添加struct核心配置文件

3.在web.xml中添加核心过滤器

```
<!-- Spring的核心监听器 -->
<listener>
    <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
</listener>
<!-- 加载Spring的配置文件的路径的，默认加载的/WEB-INF/applicationContext.xml -->
<context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>classpath:applicationContext.xml</param-value>
</context-param>
```



**有可能的错误：**

1，struts.xml文件名错误

2，struts.xml文件放置路径错误。一定要将此文件放置在src目录下。编译成功后，要确认是否编译到classes目录中

3，struts.xml文件内容错误



**Spring框架步骤**

1.导入jar包

2.添加spring核心配置文件（application.xml）

3.在web.xml文件中添加核心监听器

```
<!-- Spring的核心监听器 -->
<listener>
    <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
</listener>
<!-- 加载Spring的配置文件的路径的，默认加载的/WEB-INF/applicationContext.xml -->
<context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>classpath:applicationContext.xml</param-value>
</context-param>
```

**使用**

取代所有可以new的地方

​	1.获取servletContext域 

​	2.将applicationContext.xml从域中取出

​	3.getBean() 获取对象

示例代码：

```
ServletContext servletContext = ServletActionContext.getServletContext();
WebApplicationContext applicationContext =
        WebApplicationContextUtils.getWebApplicationContext(servletContext);
UserService userService = (UserService) applicationContext.getBean("userService");
userService.save(user);
```



可以使用一个struts-spring-plungs.jar插件

​	1.导入struts2-spring-plugin-2.5.16.jar包

​	2.定义一下属性并提供set方法

​	3.直接使用

示例代码：

```
UserService userService;
public void setUserService(UserService userService) {
    this.userService = userService;
}
```

```
public String save(){
    userService.save(user);
 }
```

**hibernate框架步骤**

1.引入jar包

2.导入hibernate.cfj.xml配置文件，引入jdbc.properties（如果使用spring可以直接在spring中配置）

​	2.1在jdbc中配置hibernate

```
<!--配置hibernate-->
<!--引入属性文件-->
<context:property-placeholder location="classpath:jdbc.properties"/>
<!--连接池-->
<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
    <property name="driverClassName" value="${jdbc.driverclass}" />
    <!--属性文件当中的名称不能和name名称一样-->
    <property name="url" value="${jdbc.url}" />
    <property name="username" value="${jdbc.username}" />
    <property name="password" value="${jdbc.password}" />
</bean>
<!-- Spring整合Hibernate -->
<!-- 引入Hibernate的配置的信息=============== -->
<bean id="sessionFactory" class="org.springframework.orm.hibernate5.LocalSessionFactoryBean">
    <!-- 注入连接池 -->
    <property name="dataSource" ref="dataSource"/>
    <!-- 配置Hibernate的相关属性 -->
    <property name="hibernateProperties">
        <props>
            <prop key="hibernate.dialect">org.hibernate.dialect.MySQL5Dialect</prop>
            <prop key="hibernate.show_sql">true</prop>
            <prop key="hibernate.format_sql">true</prop>
            <prop key="hibernate.hbm2ddl.auto">update</prop>
        </props>
    </property>
    <!-- 设置映射文件 -->
    <property name="mappingResources">
        <list>
            <value>com/itlike/domain/Account.hbm.xml</value>
        </list>
    </property>
</bean>
```

添加事务：

```
<!--配置事务管理器-->
<bean id="transactionManager"
      class="org.springframework.orm.hibernate5.HibernateTransactionManager">
    <property name="sessionFactory" ref="sessionFactory"/>
</bean>
<!--开启注解  增强-->
<tx:annotation-driven transaction-manager="transactionManager"/>
```

3.导入domain的*.hbm.xml文件与表映射

```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE hibernate-mapping PUBLIC
        "-//Hibernate/Hibernate Mapping DTD 3.0//EN"
        "http://www.hibernate.org/dtd/hibernate-mapping-3.0.dtd">
<hibernate-mapping>
    <class name="com.ybstore.domain.User" table="account" >
        <!--建立类属性哪一个是主键  还要跟数据库当中主键进行对象-->
        <id name="id" column="id" >
            <generator class="native"/>
        </id>
        <!--建立类中的普通属性与数据库当中字段进行关联-->
        <property name="name" column="name" />
        <property name="money" column="money"/>
    </class>
</hibernate-mapping>

```

4.如果dao层需要操作的话

​	1.在applicationContext.xml中先注入sessionFactory

```
<!--将dao交给spring管理-->
<bean id="userDao" class="com.ybstore.dao.UserDaoImpl">
    <!--注意这里的sessionFactory一定要注入不需要再创建模板因为sessionFactory里面会自动帮我们注入模板-->
    <!--不注入的话开启服务器会报错-->
    <property name="sessionFactory" ref="sessionFactory"></property>
</bean>
```

​	2.先继承HibernateDaoSupport

​	3.添加注解@Transactional

​	4.直接this.getHibernateTemplate();

```
@Transactional
public class UserDaoImpl extends HibernateDaoSupport implements UserDao {
    @Override
    public void save(User user) {
        System.out.println("已经保存到数据库了");
        HibernateTemplate hibernateTemplate = this.getHibernateTemplate();
        hibernateTemplate.save(user);
    }
}

```

​	