# maven

**1.创建maven工程**

​	A.groupid:分组

​	B.artifactid：项目名称	

​	C.version：版本号

ABC组成坐标

**2.选中自己的maven版本**

**3.Add Maven Property**

​	Name:archetypeCatalog

​	Value:internal

generating project in batch mode 很慢,是应为maven获取archetype-catalog.xml导致
用浏览器打开http://repo1.maven.org/maven2/archetype-catalog.xml很慢

添加Add Maven Property目的是为了解决上述问题，让maven加载本地配置就行。

**4.工程创建完成后进入界面需要点击右下角的**

**Enable Auto-Import 让他自动的导入插件**

**5.补充文件夹**

src 下有main和test

main下有java（标记成Sources），resource（Resources），webapp

test下有java和testresource

java（标记成test Sources）

testresource（标记成test resources）

**6.所有的xml文件都要放到资源目录下**

**7.创建完成**



# 准备工作

**1.在pom.xml中关联所需jar包代码段**

```
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.yb</groupId>
  <artifactId>ssmMavenCopy</artifactId>
  <version>1.0</version>
  <packaging>war</packaging>

  <name>ssmMavenCopy Maven Webapp</name>
  <!-- FIXME change it to the project's website -->
  <url>http://www.example.com</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.7</maven.compiler.source>
    <maven.compiler.target>1.7</maven.compiler.target>

    <!--定义版本号   ${org.springframework.version}-->
    <org.springframework.version>5.0.7.RELEASE</org.springframework.version>
    <org.mybatis.version>3.4.6</org.mybatis.version>
  </properties>

  <dependencies>

    <!--单元测试-->
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
    <!--lombok-->
    <dependency>
      <groupId>org.projectlombok</groupId>
      <artifactId>lombok</artifactId>
      <version>1.16.6</version>
    </dependency>
    <!-- servlet-api -->
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>servlet-api</artifactId>
      <version>2.5</version>
      <scope>provided</scope>
    </dependency>
    <!--mysql驱动-->
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>8.0.13</version>
    </dependency>
    <!-- druid -->
    <dependency>
      <groupId>com.alibaba</groupId>
      <artifactId>druid</artifactId>
      <version>1.0.14</version>
    </dependency>
    <!-- common-lang -->
    <dependency>
      <groupId>commons-lang</groupId>
      <artifactId>commons-lang</artifactId>
      <version>2.6</version>
    </dependency>
    <!--spring-test-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-test</artifactId>
      <version>${org.springframework.version}</version>
      <scope>test</scope>
    </dependency>
    <!--spring-core-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>${org.springframework.version}</version>
    </dependency>
    <!--spring-context-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>${org.springframework.version}</version>
    </dependency>
    <!--spring-context-support-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context-support</artifactId>
      <version>${org.springframework.version}</version>
    </dependency>
    <!--spring-expression-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-expression</artifactId>
      <version>${org.springframework.version}</version>
    </dependency>
    <!--spring-jdbc-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>${org.springframework.version}</version>
    </dependency>
    <!--spring-tx-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-tx</artifactId>
      <version>${org.springframework.version}</version>
    </dependency>
    <!--spring-web-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>${org.springframework.version}</version>
    </dependency>
    <!--spring-aop-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aop</artifactId>
      <version>${org.springframework.version}</version>
    </dependency>
    <!--spring-webmvc-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>${org.springframework.version}</version>
    </dependency>

    <!-- aspectj -->
    <dependency>
      <groupId>org.aspectj</groupId>
      <artifactId>aspectjrt</artifactId>
      <version>1.7.4</version>
    </dependency>
    <!--aspectj weaver-->
    <dependency>
      <groupId>org.aspectj</groupId>
      <artifactId>aspectjweaver</artifactId>
      <version>1.7.4</version>
    </dependency>

    <!-- cglib -->
    <dependency>
      <groupId>cglib</groupId>
      <artifactId>cglib</artifactId>
      <version>3.1</version>
    </dependency>

    <!-- mybatis -->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>${org.mybatis.version}</version>
    </dependency>
    <!--mybatis-spring-->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis-spring</artifactId>
      <version>1.3.0</version>
      <!--出现这个错误时rg.mybatis.spring.transaction.SpringManagedTransaction.getTimeout()Ljava/lang/Integer;
        把是因为版本太低了
      -->
    </dependency>

    <!-- jackson-core -->
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-core</artifactId>
      <version>2.9.4</version>
    </dependency>
    <!--jackson-databind-->
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
      <version>2.9.4</version>
    </dependency>
    <!--jackson-annotations-->
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-annotations</artifactId>
      <version>2.9.4</version>
    </dependency>

    <!--slf4j-api-->
    <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-api</artifactId>
      <version>1.7.6</version>
    </dependency>
    <!--slf4j-log4j12-->
    <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-log4j12</artifactId>
      <version>1.7.6</version>
    </dependency>
    <!--log4j-->
    <dependency>
      <groupId>log4j</groupId>
      <artifactId>log4j</artifactId>
      <version>1.2.17</version>
    </dependency>
    <!--commons-fileupload-->
    <dependency>
      <groupId>commons-fileupload</groupId>
      <artifactId>commons-fileupload</artifactId>
      <version>1.3.1</version>
    </dependency>
    <!-- jstl -->
    <dependency>
      <groupId>jstl</groupId>
      <artifactId>jstl</artifactId>
      <version>1.2</version>
    </dependency>
    <!-- standard -->
    <dependency>
      <groupId>taglibs</groupId>
      <artifactId>standard</artifactId>
      <version>1.1.2</version>
    </dependency>
    <!--pagehelper-->
    <dependency>
      <groupId>com.github.pagehelper</groupId>
      <artifactId>pagehelper</artifactId>
      <version>4.1.4</version>
    </dependency>


  </dependencies>

  <build>
    <finalName>ssmMavenCopy</finalName>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
      <plugins>
        <plugin>
          <artifactId>maven-clean-plugin</artifactId>
          <version>3.1.0</version>
        </plugin>
        <!-- see http://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_war_packaging -->
        <plugin>
          <artifactId>maven-resources-plugin</artifactId>
          <version>3.0.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.8.0</version>
        </plugin>
        <plugin>
          <artifactId>maven-surefire-plugin</artifactId>
          <version>2.22.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-war-plugin</artifactId>
          <version>3.2.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-install-plugin</artifactId>
          <version>2.5.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-deploy-plugin</artifactId>
          <version>2.8.2</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
</project>

```

**2.加入ssm相关的配置文件**

Spring：applicationContext.xml

SpringMVC：application-mvc.xml

mybatis：application-mybatis.xml    ,     sqlMapConfig.xml

数据库的db.properties

日志文件的log4j.properties

## spring-springMVC

1.在web.xml中配置前段控制器

```
<web-app xmlns="http://java.sun.com/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
                      http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
         version="3.0"
         metadata-complete="false">
  <absolute-ordering/>
  <display-name>web</display-name>
  <welcome-file-list>
    <welcome-file>index.html</welcome-file>
    <welcome-file>index.htm</welcome-file>
    <welcome-file>index.jsp</welcome-file>
  </welcome-file-list>


  <!--配置前端控制器-->
  <servlet>
    <servlet-name>SpringMVC</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <!--加载的主配置文件-->
      <param-value>classpath:applicationContext.xml</param-value>
    </init-param>
    <!-- 项目启动就加载框架 -->
    <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
    <servlet-name>SpringMVC</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>
  <!-- form表单编码过滤器 -->
  <filter>
    <filter-name>CharacterEncoding</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
      <param-name>encoding</param-name>
      <param-value>utf-8</param-value>
    </init-param>
  </filter>
  <filter-mapping>
    <filter-name>CharacterEncoding</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>
</web-app>
```

2.配置application-mvc.xml

```
<mvc:annotation-driven />
<!--静态资源处理 -->
<mvc:default-servlet-handler/>
<!--视图解析器 -->
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="prefix" value="/WEB-INF/views/"/>
    <property name="suffix" value=".jsp" />
</bean>
```

3.在applicationContext.xml中引入application-mvc.xml

```
<!--导入springMVC-->
<import resource="classpath:application-mvc.xml"/>
```

## spring-mybatis

1.配置application-mybatis.xml

```
    <!--注解扫描-->
    <context:component-scan base-package="com.yb"/>

    <!--spring-Mybatis整合-->
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
<!--        &lt;!&ndash;配置mapper映射文件的路径&ndash;&gt;
        <property name="mapperLocations" value="classpath:com.yb.mapper/*Mapper.xml"/>-->
    </bean>

    <!-- 配置Mapper接口扫描 -->
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <!-- 配置Mapper xml文件扫描包 -->
        <property name="basePackage" value="com.yb.mapper" />
    </bean>
```

2.在applicationConntext.xml中引入application-mybatis.xml

```
<!--导入mybatis-->
<import resource="classpath:application-mybatis.xml"/>
```

# 插件

代码生成器：mybatis-generator

1.导入插件代码到pom.xml中（不能写到默认的pubginManagement可能会不生效，自己写一个plugsins）

```
<plugins>
  <plugin>
    <groupId>org.mybatis.generator</groupId>
    <artifactId>mybatis-generator-maven-plugin</artifactId>
    <version>1.3.2</version>
    <configuration>
      <verbose>true</verbose>
      <overwrite>false</overwrite>
    </configuration>
    <dependencies>
      <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.13</version>
      </dependency>
    </dependencies>
  </plugin>
</plugins>
```

2.导入generatorConfig.xml文件

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
      PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
      "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
<!-- 配置生成器 -->
<generatorConfiguration>

   <context id="mysql" defaultModelType="hierarchical"
          targetRuntime="MyBatis3Simple">

      <!-- 自动识别数据库关键字，
      默认false，如果设置为true，
      根据SqlReservedWords中定义的关键字列表；
      一般保留默认值，
      遇到数据库关键字（Java关键字），
      使用columnOverride覆盖 -->
      <property name="autoDelimitKeywords" value="false" />
      <!-- 生成的Java文件的编码 -->
      <property name="javaFileEncoding" value="UTF-8" />
      <!-- 格式化java代码 -->
      <property name="javaFormatter"
              value="org.mybatis.generator.api.dom.DefaultJavaFormatter" />
      <!-- 格式化XML代码 -->
      <property name="xmlFormatter"
              value="org.mybatis.generator.api.dom.DefaultXmlFormatter" />

      <!-- beginningDelimiter和endingDelimiter：指明数据库的用于标记数据库对象名的符号，
      比如ORACLE就是双引号，MYSQL默认是`反引号； -->
      <property name="beginningDelimiter" value="`" />
      <property name="endingDelimiter" value="`" />

      <!--阻止生成日期和注释-->
      <commentGenerator>
         <property name="suppressDate" value="true" />
         <property name="suppressAllComments" value="true" />
      </commentGenerator>

      <!-- 数据库连接信息 -->
      <jdbcConnection driverClass="com.mysql.cj.jdbc.Driver"
                  connectionURL="jdbc:mysql://localhost:3306/mybatis?serverTimezone=UTC"
                  userId="root" password="123456">

         <property name ="nullCatalogMeansCurrent" value = "true"/>
      </jdbcConnection>

      <!-- java类型处理器 用于处理数据库中的类型到Java中的类型，
          默认使用JavaTypeResolverDefaultImpl；
          注意一点，默认会先尝试使用Integer，Long，Short等来对应DECIMAL和
         NUMERIC数据类型； -->
      <javaTypeResolver
            type="org.mybatis.generator.internal.types.JavaTypeResolverDefaultImpl">
         <!-- true：使用BigDecimal对应DECIMAL和 NUMERIC数据类型 f
             alse：默认, scale>0;length>18：使用BigDecimal;
            scale=0;length[10,18]：使用Long； scale=0;length[5,9]：
            使用Integer； scale=0;length<5：使用Short； -->
         <property name="forceBigDecimals" value="false" />
      </javaTypeResolver>


      <!--
      配置domain生成策略
        targetProject:把自动生成的domian放在哪个工程里面
        targetPackage:哪个包下
      -->
      <javaModelGenerator targetPackage="com.yb.domain"
                     targetProject="src/main/java">
         <!-- for MyBatis3/MyBatis3Simple
         自动为每一个生成的类创建一个构造方法，
         构造方法包含了所有的field；而不是使用setter； -->
         <property name="constructorBased" value="false" />

         <!-- for MyBatis3 / MyBatis3Simple
         是否创建一个不可变的类，如果为true，
         那么MBG会创建一个没有setter方法的类，
         取而代之的是类似constructorBased的类 -->
         <property name="immutable" value="false" />

         <!-- 设置是否在getter方法中，
         对String类型字段调用trim()方法 -->
         <property name="trimStrings" value="true" />
      </javaModelGenerator>

      <!--
            配置mapper.xml的生成策略
            targetPackage:把自动生成的mapper放在哪个工程里面
            targetProject:哪个包下
        -->
      <sqlMapGenerator targetPackage="com.yb.mapper"
                   targetProject="src/main/java">
         <!-- 在targetPackage的基础上，
         根据数据库的schema再生成一层package，
         最终生成的类放在这个package下，默认为false -->
         <property name="enableSubPackages" value="true" />
      </sqlMapGenerator>

      <!--
           mapper接口生成策略
        -->
      <javaClientGenerator targetPackage="com.yb.mapper"
                      type="XMLMAPPER" targetProject="src/main/java">
         <property name="enableSubPackages" value="true" />
      </javaClientGenerator>

      <table schema="mybatis" tableName="teacher" domainObjectName="Teacher"></table>

   </context>
</generatorConfiguration>
```

mysql8.x的数据库需要配置：

在jdbcConnection中加入

<property name ="nullCatalogMeansCurrent" value = "true"/>

否则生成的文件会出错（由于8.x的数据库会默认将所有的查找一遍）

```
<!--对应数据库的表和生成的domain名-->
<table schema="mybatis" tableName="teacher" domainObjectName="Teacher"></table>
```

# 测试

创建一个form表单，尝试将文本框里的数据插入到数据库中

# 注意点

1.要将生成的mapper.xml文件放到resources资源目录下

在resources下再创建一个同名的文件夹

2.在application-mybatis.xml中要配置一下mapper.xml文件的路径

```
<!-- Mybatis的工厂 -->
<bean id="sqlSessionFactoryBean" class="org.mybatis.spring.SqlSessionFactoryBean">
    <property name="dataSource" ref="dataSource"/>
    <!-- 核心配置文件的位置 -->
    <property name="configLocation" value="classpath:sqlMapConfig.xml"/>
    <!--配置mapper映射文件的路径-->
    <property name="mapperLocations" value="classpath:com.yb.mapper/*Mapper.xml"/>
</bean>
```

