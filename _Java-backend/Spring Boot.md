---
title: "Spring Boot"
collection: Java-backend
permalink: /Java-backend/Spring Boot
excerpt: 'Spring Boot'
date: 2023-02-05
venue: 'February 5'
---
# **Spring Boot** Deeply

## Hello Spring Boot

## 自动配置原理

SpringBoot默认会在底层配好所有的组件。但是如果用户自己配置了以用户的优先

虽然我们127个场景的所有自动配置启动的时候默认全部加载。xxxxAutoConfiguration
按照条件装配规则（@Conditional），最终会按需配置

### 依赖管理

```java
依赖管理    
<parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.3.4.RELEASE</version>
</parent>

他的父项目
 <parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-dependencies</artifactId>
    <version>2.3.4.RELEASE</version>
  </parent>

几乎声明了所有开发中常用的依赖的版本号,自动版本仲裁机制
    无需关注版本号，自动版本仲裁
    1、引入依赖默认都可以不写版本
    2、引入非版本仲裁的jar，要写版本号。
    
    
可以修改默认版本号
    1、查看spring-boot-dependencies里面规定当前依赖的版本 用的 key。
    2、在当前项目里面重写配置
    <properties>
        <mysql.version>5.1.43</mysql.version>
    </properties>
    
    
开发导入starter场景启动器--起步依赖
    1、见到很多 spring-boot-starter-* ： *就某种场景
    2、只要引入starter，这个场景的所有常规需要的依赖我们都自动引入
    3、SpringBoot所有支持的场景
    https://docs.spring.io/spring-boot/docs/current/reference/html/using-spring-boot.html#using-boot-starter
    4、见到的  *-spring-boot-starter： 第三方为我们提供的简化开发的场景启动器。
    5、所有场景启动器最底层的依赖
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter</artifactId>
      <version>2.3.4.RELEASE</version>
      <scope>compile</scope>
    </dependency>
```

![image-20221118094237279](/images/image-20221118094237279.png)

![image-20221118095138455](/images/image-20221118095138455.png)

### 自动配置

- **自动配好Tomcat**

- - 引入Tomcat依赖。
  - 配置Tomcat

```java
<dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-tomcat</artifactId>
      <version>2.3.4.RELEASE</version>
      <scope>compile</scope>
    </dependency>
```

- **自动配好SpringMVC**

- - **引入SpringMVC全套组件**
  - **自动配好SpringMVC常用组件（功能）**

- 自动配好Web常见功能，如：字符编码问题

- - SpringBoot帮我们配置好了所有web开发的常见场景

- **默认的包结构**

- - **主程序所在包及其下面的所有子包里面的组件都会被默认扫描进来**
  - 无需以前的包扫描配置
  - **想要改变扫描路径，@SpringBootApplication(scanBasePackages="com.eddie")**

- ![image-20221118100718091](/images/image-20221118100718091.png)

- - - **或者@ComponentScan 指定扫描路径**

```java
@SpringBootApplication
等同于
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan("com.eddie.boot")
```

![image-20221118100837667](/images/image-20221118100837667.png)

![image-20221118095415107](/images/image-20221118095415107.png)

![image-20221118095627629](/images/image-20221118095627629.png)

- **各种配置拥有默认值**

- - **默认配置**最终都是**映射到某个类上**，如：MultipartProperties

- ![image-20221118101147970](/images/image-20221118101147970.png)

- ![image-20221118101132664](/images/image-20221118101132664.png)

- - **配置文件的值最终会绑定每个类上，这个类会在容器中创建对象**

- **按需加载所有自动配置项**

- - 非常多的starter
  - **引入了哪些场景这个场景的自动配置才会开启**
  - SpringBoot所有的自动配置功能都在 spring-boot-autoconfigure 包里面

- ```java
      <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-autoconfigure</artifactId>
        <version>2.7.5</version>
        <scope>compile</scope>
      </dependency>
  ```

- 

### 查看Spring Boot为我们自动配置的组件

```java
@SpringBootApplication
public class SpringHelloApplication {
    public static void main(String[] args) {
        //返回的IOC容器
        ConfigurableApplicationContext run = SpringApplication.run(SpringHelloApplication.class, args);
        //获取IOC容器中所有组件的name
        String[] beanDefinitionNames = run.getBeanDefinitionNames();
        for (String name :
                beanDefinitionNames) {
            System.out.println(name);
        }
    }
}
```

![image-20221118100245199](/images/image-20221118100245199.png)

### Spring自动配置原理

![image-20221118193315466](/images/image-20221118193315466.png)

![image-20221118192600694](/images/image-20221118192600694.png)

### 按需加载（@Conditional条件装配）

#### @Import(AutoConfigurationImportSelector.class)

```java
1、利用getAutoConfigurationEntry(annotationMetadata);给容器中批量导入一些组件
2、调用List<String> configurations = getCandidateConfigurations(annotationMetadata, attributes)获取到所有需要导入到容器中的配置类
3、利用工厂加载 Map<String, List<String>> loadSpringFactories(@Nullable ClassLoader classLoader)；得到所有的组件
4、从META-INF/spring.factories位置来加载一个文件。
	默认扫描我们当前系统里面所有META-INF/spring.factories位置的文件
    spring-boot-autoconfigure-2.3.4.RELEASE.jar包里面也有META-INF/spring.factories
    
```

![image-20221118195405828](/images/image-20221118195405828.png)

#### 按需加载

虽然我们127个场景的所有自动配置启动的时候默认全部加载。xxxxAutoConfiguration
按照条件装配规则（@Conditional），最终会按需配置。

![image-20221118195201168](/images/image-20221118195201168.png)

### IOC容器功能

#### 组件添加

##### @Configuration|@Bean

**.`@Configuration`配置类是有主次之分的，主配置类是驱动整个程序的入口，可以是一个，也可以是多个（若存在多个，支持使用@Order排序）**

- 基本使用
- **Full模式与Lite模式**

- - 示例
  - 最佳实战

- - - 配置 **类组件之间无依赖关系用Lite模式加速容器启动过程**，减少判断并能**提高Spring启动速度**
    - **配置类组件之间有依赖关系**，方法会被**调用得到之前单实例组件**，**用Full模式**

  - @Configuration（proxyBeanMethods = true）配置类为代理对象 会到IOC容器进行寻找Bean 保证单例Bean

  - Full——>proxyBeanMethods = true单例模式 会到IOC容器中寻找Bean

  - Lite——>proxyBeanMethods = false多例模式

```java
@Configuration//指明是配置类 配置类也是IOC容器中的组件
public class MyConfig {

    @Bean//给容器中添加组件 方法名为组件的id(可以通过name属性指定组件的id) 返回类型就是组件的类型 返回的值就是组件
                            //spring默认的单列Bean
    public Book myBook(){//组件注册方法
        return new Book(1,"Information Technology","Eddie Study Java","Persevere");
    }
}

@SpringBootApplication
public class SpringHelloSsm1Application {

    public static void main(String[] args) {
        ConfigurableApplicationContext run = SpringApplication.run(SpringHelloSsm1Application.class, args);
        Book javaBean1 = run.getBean("myBook", Book.class);
        Book javaBean2 = run.getBean("myBook", Book.class);
        Book javaBean3 = run.getBean("myBook", Book.class);
        if (javaBean3 == javaBean2 && javaBean2 == javaBean1){
            System.out.println("myBook is  simple");
        }
    }

}

console
    myBook is  simple
```

![image-20221118112300368](/images/image-20221118112300368.png)

##### @Component

标识为任意层组件的注解

![image-20221118114221633](/images/image-20221118114221633.png)

```java
public @interface Component {
    String value() default "";
}
```

##### @Controller

标识为Controller层的注解

![image-20221118114325489](/images/image-20221118114325489.png)

```java
public @interface Controller {
    @AliasFor(
        annotation = Component.class
    )
    String value() default "";
}
```

##### @Service

标识为Service层的注解

![image-20221118114312465](/images/image-20221118114312465.png)

```java
public @interface Service {
    @AliasFor(
        annotation = Component.class
    )
    String value() default "";
}
```

##### @Repository

标识为DAO层的注解

![image-20221118114350935](/images/image-20221118114350935.png)

```java
public @interface Repository {
    @AliasFor(
        annotation = Component.class
    )
    String value() default "";
}
```

##### @ComponentScan

开启组件扫描并指定组件扫描的包范围的注解

@ComponentScan(basePackages = "com.example")

![image-20221118114040367](/images/image-20221118114040367.png)

##### @Import

@Import（{JdbcConfig.class,SpringMvcConfig.class}）默认在IOC容器中的BeanName为全类名

给容器中自动创建出这两个类型的组件、默认组件的名字就是全类名

**用来导入其他配置类**

![image-20221118131103698](/images/image-20221118131103698.png)

```java
public @interface Import {
    Class<?>[] value();
}
```

##### @Conditional

**条件装配**：满足Conditional指定的条件，则进行组件注入

```java
=====================测试条件装配==========================
@Configuration//告诉SpringBoot这是一个配置类 == 配置文件
//@ConditionalOnBean(name = "tom")当IOC容器中有name为"tom"的bean时 配置类中的@Bean的配置方法才会生效
@ConditionalOnMissingBean(name = "tom")//当IOC容器中没有name为"tom"的bean时 配置类中的@Bean的配置方法才会生效
public class MyConfig {

	
    @Bean //给容器中添加组件。以方法名作为组件的id。返回类型就是组件类型。返回的值，就是组件在容器中的实例
    //@ConditionalOnBean(name = "tom")当IOC容器中有name为"tom"的bean时 此@Bean的配置方法才会生效
    public User user01(){
        User zhangsan = new User("zhangsan", 18);
        //user组件依赖了Pet组件
        zhangsan.setPet(tomcatPet());
        return zhangsan;
    }

    @Bean("tom22")
    public Pet tomcatPet(){
        return new Pet("tomcat");
    }
}

public static void main(String[] args) {
        //1、返回我们IOC容器
        ConfigurableApplicationContext run = SpringApplication.run(MainApplication.class, args);

        //2、查看容器里面的组件
        String[] names = run.getBeanDefinitionNames();
        for (String name : names) {
            System.out.println(name);
        }

        boolean tom = run.containsBean("tom");
        System.out.println("容器中Tom组件："+tom);

        boolean user01 = run.containsBean("user01");
        System.out.println("容器中user01组件："+user01);

        boolean tom22 = run.containsBean("tom22");
        System.out.println("容器中tom22组件："+tom22);


    }
```

![image-20221118130304008](/images/image-20221118130304008.png)

#### 配置文件引入

##### @ImportResource("classpath:配置文件名")

引入xml等配置文件

```java
@ImportResource("classpath:beans.xml")
public class MyConfig {}

======================测试=================
        boolean haha = run.containsBean("haha");
        boolean hehe = run.containsBean("hehe");
        System.out.println("haha："+haha);//true
        System.out.println("hehe："+hehe);//true
```



```xml
======================beans.xml=========================
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

    <bean id="haha" class="com.atguigu.boot.bean.User">
        <property name="name" value="zhangsan"></property>
        <property name="age" value="18"></property>
    </bean>

    <bean id="hehe" class="com.atguigu.boot.bean.Pet">
        <property name="name" value="tomcat"></property>
    </bean>
</beans>
```

#### 配置绑定（读取配置内容封装成实体类对象）

**确保实体类作为IOC容器中的组件** @Component或者@EnableConfigurationProperties（实体类.class）开启实体类的属性绑定功能

**将配置文件中的内容读取**并且**封装成Java实体对象**以**供后续使用**

##### 方式一@Component+@ConfigurationProperties

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
@Component
@ConfigurationProperties(prefix = "user")//指定前缀
public class User {//需要提供get和set方法
    private String username;
    private Integer age;
    private char gender;
}
```

```yaml
user:
  username: EddieZhang
  age: 21
  gender: 男
```

![image-20221118185924766](/images/image-20221118185924766.png)

![image-20221118185905550](/images/image-20221118185905550.png)

##### 方式二@EnableConfigurationProperties+@ConfigurationProperties

![image-20221118190541939](/images/image-20221118190541939.png)

![image-20221118190553453](/images/image-20221118190553453.png)

![image-20221118190601920](/images/image-20221118190601920.png)

![image-20230131182755492](/images/image-20230131182755492.png)



![image-20221118185905550](/images/image-20221118185905550.png)

### 使用CommandLineRunner

**容器加载后**   **项目启动前**调用CommandLineRunner接口的run方法

![image-20221120235927335](/images/image-20221120235927335.png)

![image-20221121000131841](/images/image-20221121000131841.png)

![image-20221121000949904](/images/image-20221121000949904.png)



### 修改默认配置

```java
        @Bean
		@ConditionalOnBean(MultipartResolver.class)  //容器中有这个类型组件
		@ConditionalOnMissingBean(name = DispatcherServlet.MULTIPART_RESOLVER_BEAN_NAME) //容器中没这个名字 multipartResolver 的组件
		public MultipartResolver multipartResolver(MultipartResolver resolver) {
            //给@Bean标注的方法传入了对象参数，这个参数的值就会从容器中找。
            //SpringMVC multipartResolver。防止有些用户配置的文件上传解析器不符合规范
			// Detect if the user has created a MultipartResolver but named it incorrectly
			return resolver;
		}
        给容器中加入了文件上传解析器；
```

SpringBoot默认会在底层配好所有的组件。但是如果用户自己配置了以**用户的优先**

自己@Bean注册一个组件到容器中 SpringBoot会以用户的为准

```java
    @Bean
	@ConditionalOnMissingBean
	public CharacterEncodingFilter characterEncodingFilter() {
    }
```

### 总结

总结：

- SpringBoot**先加载所有的自动配置类**  xxxxxAutoConfiguration
- 每个自动配置类**按照条件进行生效**，**默认都会绑定配置文件**指定的值。xxxxProperties里面拿。**xxxProperties和配置文件进行了绑定**
- 生效的配置类就会给容器中装配很多组件
- 只要容器中有这些组件，相当于这些功能就有了
- 定制化配置

- - 用户直接自己**@Bean替换底层的组件**
  - 用户去看这个组件是获取的**配置文件**什么值就去**修改**。

**xxxxxAutoConfiguration ---> 组件  --->** **xxxxProperties里面拿值  ----> application.properties**

### 最佳实践

- 引入场景依赖

- - https://docs.spring.io/spring-boot/docs/current/reference/html/using-spring-boot.html#using-boot-starter

- 查看自动配置了哪些（选做）

- - 自己分析，引入场景对应的自动配置一般都生效了
  - 配置文件中debug=true开启自动配置报告。Negative（不生效）\Positive（生效）

- 是否需要修改

- - 参照文档修改配置项

- - - https://docs.spring.io/spring-boot/docs/current/reference/html/appendix-application-properties.html#common-application-properties
    - 自己分析。xxxxProperties绑定了配置文件的哪些。

- - 自定义加入或者替换组件

- - - @Bean、@Component。。。

- - 自定义器  **XXXXXCustomizer**；
  - ......

### 使用容器

![image-20221120234910779](/images/image-20221120234910779.png)

![image-20221120235032509](/images/image-20221120235032509.png)

![image-20221120234936825](/images/image-20221120234936825.png)

![image-20221120234946229](/images/image-20221120234946229.png)

## Lombok

### 简化domain开发

![image-20221118223930965](/images/image-20221118223930965.png)

![image-20221118223916959](/images/image-20221118223916959.png)

![image-20221111095900057](/images/image-20221111095900057.png)

![image-20221118224021282](/images/image-20221118224021282.png)

### @Slf4j日志

![image-20221118224249140](/images/image-20221118224249140.png)

![image-20221118224508000](/images/image-20221118224508000.png)

![image-20221118224457296](/images/image-20221118224457296.png)

## Dev-Tools

热更新

ctrl+F9

![image-20221118225154707](/images/image-20221118225154707.png)

![image-20221118224724053](/images/image-20221118224724053.png)

|      |      |
| ---- | ---- |
|      |      |
|      |      |
|      |      |

## 配置文件

application.properties > application.yml > application.yaml

### .yaml格式文件

核心规则：**数据前**面要**加空格与冒号隔开**

![image-20221118232049221](/images/image-20221118232049221.png)

![image-20221118232104622](/images/image-20221118232104622.png)

![image-20221118230428882](/images/image-20221118230428882.png)

优点： 容易阅读 

yaml 类型的配置文件比 xml 类型的配置文件更容易阅读，结构更加清晰 容易与脚本语言交互 以数据为核心，重数据轻格式 

yaml 更注重数据，而 xml 更注重格式

YAML 文件扩展名：

 .yml (主流) 

![image-20221118230326497](/images/image-20221118230326497.png)

.yaml

#### 基本语法

- key: value；kv之间有空格
- 大小写敏感
- 使用缩进表示层级关系
- 缩进不允许使用tab，只允许空格
- 缩进的空格数不重要，只要相同层级的元素左对齐即可
- '#'表示注释
- 字符串无需加引号，如果要加，''与""表示字符串内容 会被 转义/不转义

#### 数据类型

- 字面量：单个的、不可再分的值。date、boolean、string、number、null

```yaml
location: classpath:banner.jpg
```

- 对象：键值对的集合。map、hash、set、object 

```yaml
行内写法：  k: {k1:v1,k2:v2,k3:v3}
#或
k: 
  k1: v1
  k2: v2
  k3: v3
```

- 数组：一组按次序排列的值。array、list、queue

```yaml
行内写法：  k: [v1,v2,v3]
#或者
k:
 - v1
 - v2
 - v3
```

#### 配置提示

自定义的类和配置文件绑定一般没有提示

可以引入spring-boot-configuration-processor依赖

建议打包的时候把配置处理器（对于我们配置有友好提示的作用）exclude掉 没必要将与项目运行无关的进行打包

```java
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-configuration-processor</artifactId>
            <optional>true</optional>
        </dependency>
      //建议打包的时候把配置处理器（对于我们配置有友好提示的作用）exclude掉 没必要将与项目运行无关的进行打包      
      <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <configuration>
                    <excludes>
                        <exclude>
                            <groupId>org.springframework.boot</groupId>
                            <artifactId>spring-boot-configuration-processor</artifactId>
                        </exclude>
                    </excludes>
                </configuration>
            </plugin>
        </plugins>
    </build>
```

![image-20221118231624133](/images/image-20221118231624133.png)

### properties文件

![image-20221118231400615](/images/image-20221118231400615.png)

![image-20221118231333469](/images/image-20221118231333469.png)

### 多环境配置

![image-20221120234428578](/images/image-20221120234428578.png)

## Web开发

### 静态资源访问

原理： 静态映射/**。

请求进来，先去找Controller看能不能处理。不能处理的所有请求又都交给静态资源处理器。静态资源也找不到则响应404页面

![image-20221118235847527](/images/image-20221118235847527.png)

#### 静态资源目录

只要静态资源放在类路径下： called `/static` (or `/public` or `/resources` or `/META-INF/resources`

访问 ： 当前项目根路径/ + 静态资源名

#### 改变默认的静态资源路径以及访问前缀

默认目录： called `/static` (or `/public` or `/resources` or `/META-INF/resources`

默认无前缀

前缀的指定会由于SpringBoot的原因 影响**欢迎页面**以及**Favicon图标**

```yaml
spring:
  mvc:
    static-path-pattern: /res/**
    # 配置静态资源访问前缀

  resources:
    static-locations: [classpath:/haha/]
    # 静态资源路径目录
```

#### webjar（了解）

自动映射 /[webjars](http://localhost:8080/webjars/jquery/3.5.1/jquery.js)/**

https://www.webjars.org/

```xml
        <dependency>
            <groupId>org.webjars</groupId>
            <artifactId>jquery</artifactId>
            <version>3.5.1</version>
        </dependency>
```

访问地址：[http://localhost:8080/webjars/**jquery/3.5.1/jquery.js**](http://localhost:8080/webjars/jquery/3.5.1/jquery.js)   后面地址要按照依赖里面的包路径

### 欢迎页面

- 静态资源路径下  index.html

- - 可以配置静态资源路径
  - 但是**不可以配置静态资源的访问前缀**。否则**导致 index.html不能被默认访问**

![image-20221119000456276](/images/image-20221119000456276.png)

### 自定义 `Favicon`

图标

![image-20221119110404974](/images/image-20221119110404974.png)

favicon.ico 放在静态资源目录下即可 同时Browser禁用缓存

![image-20221119001256834](/images/image-20221119001256834.png)

![image-20221119001319853](/images/image-20221119001319853.png)

![image-20221119001327388](/images/image-20221119001327388.png)

### 静态资源配置原理

- SpringBoot启动默认加载  xxxAutoConfiguration 类（自动配置类）
- SpringMVC功能的自动配置类 WebMvcAutoConfiguration，生效

![image-20221119103203003](/images/image-20221119103203003.png)

配置文件的相关属性进行了绑定

```
WebProperties------"spring.web"
ResourceProperties------"spring.resources"
```

![image-20221119103948983](/images/image-20221119103948983.png)

**配置类只有一个有参构造**

//有参构造器所有参数的值都会从容器中确定

```java
//ResourceProperties resourceProperties；获取和spring.resources绑定的所有的值的对象
//WebMvcProperties mvcProperties 获取和spring.mvc绑定的所有的值的对象
//ListableBeanFactory beanFactory Spring的beanFactory
//HttpMessageConverters 找到所有的HttpMessageConverters
//ResourceHandlerRegistrationCustomizer 找到 资源处理器的自定义器。=========
//DispatcherServletPath  
//ServletRegistrationBean   给应用注册Servlet、Filter....
public WebMvcAutoConfigurationAdapter(WebProperties webProperties, WebMvcProperties mvcProperties, ListableBeanFactory beanFactory, ObjectProvider<HttpMessageConverters> messageConvertersProvider, ObjectProvider<WebMvcAutoConfiguration.ResourceHandlerRegistrationCustomizer> resourceHandlerRegistrationCustomizerProvider, ObjectProvider<DispatcherServletPath> dispatcherServletPath, ObjectProvider<ServletRegistrationBean<?>> servletRegistrations) {
    this.resourceProperties = webProperties.getResources();
    this.mvcProperties = mvcProperties;
    this.beanFactory = beanFactory;
    this.messageConvertersProvider = messageConvertersProvider;
    this.resourceHandlerRegistrationCustomizer = (WebMvcAutoConfiguration.ResourceHandlerRegistrationCustomizer)resourceHandlerRegistrationCustomizerProvider.getIfAvailable();
    this.dispatcherServletPath = dispatcherServletPath;
    this.servletRegistrations = servletRegistrations;
    this.mvcProperties.checkConfiguration();
}
```

#### 资源处理器的默认规则

![image-20221119110431494](/images/image-20221119110431494.png)

```java
public void addResourceHandlers(ResourceHandlerRegistry registry) {
    if (!this.resourceProperties.isAddMappings()) {
        logger.debug("Default resource handling disabled");
    } else {
        this.addResourceHandler(registry, "/webjars/**", "classpath:/META-INF/resources/webjars/");
        this.addResourceHandler(registry, this.mvcProperties.getStaticPathPattern(), (registration) -> {
            registration.addResourceLocations(this.resourceProperties.getStaticLocations());
            if (this.servletContext != null) {
                ServletContextResource resource = new ServletContextResource(this.servletContext, "/");
                registration.addResourceLocations(new Resource[]{resource});
            }

        });
    }
}
```

```java
public static class Resources {
    private static final String[] CLASSPATH_RESOURCE_LOCATIONS = new String[]{"classpath:/META-INF/resources/", "classpath:/resources/", "classpath:/static/", "classpath:/public/"};
    private String[] staticLocations;
    private boolean addMappings;
    private boolean customized;
    private final WebProperties.Resources.Chain chain;
    private final WebProperties.Resources.Cache cache;

    public Resources() {
        this.staticLocations = CLASSPATH_RESOURCE_LOCATIONS;
        this.addMappings = true;
        this.customized = false;
        this.chain = new WebProperties.Resources.Chain();
        this.cache = new WebProperties.Resources.Cache();
    }
```

![image-20221119105017981](/images/image-20221119105017981.png)

#### 欢迎页的处理规则

```java
HandlerMapping：处理器映射。保存了每一个Handler能处理哪些请求。	

    @Bean
	public WelcomePageHandlerMapping welcomePageHandlerMapping(ApplicationContext applicationContext,
			FormattingConversionService mvcConversionService, ResourceUrlProvider mvcResourceUrlProvider) {
		WelcomePageHandlerMapping welcomePageHandlerMapping = new WelcomePageHandlerMapping(
				new TemplateAvailabilityProviders(applicationContext), applicationContext, getWelcomePage(),
				this.mvcProperties.getStaticPathPattern());
		welcomePageHandlerMapping.setInterceptors(getInterceptors(mvcConversionService, mvcResourceUrlProvider));
		welcomePageHandlerMapping.setCorsConfigurations(getCorsConfigurations());
		return welcomePageHandlerMapping;
	}

WelcomePageHandlerMapping(TemplateAvailabilityProviders templateAvailabilityProviders,
		ApplicationContext applicationContext, Optional<Resource> welcomePage, String staticPathPattern) {
	if (welcomePage.isPresent() && "/**".equals(staticPathPattern)) {
        //要用欢迎页功能，必须是/**
		logger.info("Adding welcome page: " + welcomePage.get());
		setRootViewName("forward:index.html");
	}
	else if (welcomeTemplateExists(templateAvailabilityProviders, applicationContext)) {
        // 调用Controller  /index
		logger.info("Adding welcome page template: index");
		setRootViewName("index");
	}
}
```

![image-20221119110827085](/images/image-20221119110827085.png)

### 请求参数处理

#### 请求映射

##### rest使用与原理

###### 使用

**针对From表单提交**（由于From表单只有get和post两个请求方式 并且默认为get请求）

因此需要**HiddenMethodFilter**来进行包装 进而有POST GET DELETE PUT四种请求

- @xxxMapping；
- Rest风格支持（*使用**HTTP**请求方式动词来表示对资源的操作*）

- - *以前：**/getUser*  *获取用户*    */deleteUser* *删除用户*   */editUser*  *修改用户*      */saveUser* *保存用户*
  - *现在： /user*    *GET-**获取用户*    *DELETE-**删除用户*     *PUT-**修改用户*      *POST-**保存用户*
  - **核心Filter；HiddenHttpMethodFilter**

- - - 用法： **表单method=post，隐藏域 _method=put**
    - **SpringBoot中手动开启**
    - 如何把_method 这个名字换成我们自己喜欢的。**自定义一个HiddenMethodFilter取代系统提供的 并setMethodParam**

  - ![image-20221119121935857](/images/image-20221119121935857.png)

```html
<form th:action="@{/target/hiddenMethodTest}" method="POST">
  <input type="hidden" name="_method" value="put">
  name: <input type="text" name="name" value="">
  password: <input type="password" name="password" value="">
  <input type="submit" value="submit">
</form>
```

![image-20221119121612285](/images/image-20221119121612285.png)

![image-20221119121548291](/images/image-20221119121548291.png)

###### 原理

Rest原理（表单提交要使用REST的时候）

- 表单提交会带上**_method=PUT**
- **请求过来被**HiddenHttpMethodFilter拦截

- - 请求是否正常，并且是POST

- - - 获取到**_method**的值。
    - 兼容以下请求；**PUT**.**DELETE**.**PATCH**
    - **原生request（post），包装模式requestWrapper重写了getMethod方法，返回的是传入的值。**
    - **过滤器链放行的时候用wrapper。以后的方法调用getMethod是调用**  **requesWrapper的。**



**Rest使用客户端工具，**

- 如PostMan直接发送Put、delete等方式请求，无需Filter。

### 请求映射原理

SpringMVC中所有的请求都会过**DispatcherServlet**（前端控制器）

所有的请求映射都在**HandlerMapping**中。

- SpringBoot自动配置欢迎页的 WelcomePageHandlerMapping 。访问 /能访问到index.html；
- SpringBoot自动配置了默认 的 **RequestMappingHandlerMapping--对应的@RequestMapping注解**
- 请求进来，挨个尝试所有的HandlerMapping看是否有请求信息。

- - 如果有就找到这个请求对应的handler
  - 如果没有就是下一个 HandlerMapping

- 我们需要一些自定义的映射处理，我们也可以自己给容器中放**HandlerMapping**。自定义 **HandlerMapping**

![image-20221119152055026](/images/image-20221119152055026.png)

SpringMVC功能分析都从 org.springframework.web.servlet.DispatcherServlet-》doDispatch（）

![image-20221119152009891](/images/image-20221119152009891.png)

![image-20221119153118917](/images/image-20221119153118917.png)

![image-20221119153126839](/images/image-20221119153126839.png)

**RequestMappingHandlerMapping**：保存了所有**@RequestMapping** 和**handler**的映射规则。

![img](https://cdn.nlark.com/yuque/0/2020/png/1354552/1603181662070-9e526de8-fd78-4a02-9410-728f059d6aef.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_48%2Ctext_YXRndWlndS5jb20g5bCa56GF6LC3%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10)

![image-20221119153541356](/images/image-20221119153541356.png)

### 参数处理原理

@PathVariable、@RequestHeader、@ModelAttribute、@RequestParam、@MatrixVariable、@CookieValue、@RequestBody

**Servlet API：**

WebRequest、ServletRequest、MultipartRequest、 HttpSession、javax.servlet.http.PushBuilder、Principal、InputStream、Reader、HttpMethod、Locale、TimeZone、ZoneId

**复杂参数：**

**Map**、**Model（map、model里面的数据会被放在request的请求域  request.setAttribute）、**Errors/BindingResult、**RedirectAttributes（ 重定向携带数据）**、**ServletResponse（response）**、SessionStatus、UriComponentsBuilder、ServletUriComponentsBuilder

**参数处理原理**

- HandlerMapping中找到能处理请求的Handler（Controller.method()）
- 为当前Handler 找一个适配器 HandlerAdapter； **RequestMappingHandlerAdapter**
- 适配器执行目标方法并确定方法参数的每一个值

![image-20221119190120881](/images/image-20221119190120881.png)

![image-20221119190253118](/images/image-20221119190253118.png)

**HandlerAdapter**

![image-20221119190139817](/images/image-20221119190139817.png)

0 - 支持方法上标注@RequestMapping 

1 - 支持函数式编程的

**执行目标方法**

```java
// Actually invoke the handler.
//DispatcherServlet -- doDispatch
mv = ha.handle(processedRequest, response, mappedHandler.getHandler());
```

```java
mav = invokeHandlerMethod(request, response, handlerMethod); //执行目标方法


//ServletInvocableHandlerMethod
Object returnValue = invokeForRequest(webRequest, mavContainer, providedArgs);
//获取方法的参数值
Object[] args = getMethodArgumentValues(request, mavContainer, providedArgs);
```

![image-20221119190416461](/images/image-20221119190416461.png)

**参数解析器-HandlerMethodArgumentResolver**

确定将要执行的目标方法的每一个参数的值是什么

SpringMVC目标方法能写多少种参数类型。取决于参数解析器

![image-20221119193354170](/images/image-20221119193354170.png)

- 当前解析器是否支持解析这种参数
- 支持就调用 resolveArgument

**返回值处理器**

![image-20221119193413441](/images/image-20221119193413441.png)

# Spring Boot

[Spring Boot](https://spring.io/projects/spring-boot)

![image-20221120230430368](/images/image-20221120230430368.png)



## Web组件

### 拦截器Interceptor

![image-20221121122042619](/images/image-20221121122042619.png)

### Servlet

![image-20221121123511247](/images/image-20221121123511247.png)

![image-20221121123835671](/images/image-20221121123835671.png)

### Filter

![image-20221121130741548](/images/image-20221121130741548.png)

#### CharacterEncodingFilter解决响应中文乱码的Filter

yml配置

![image-20221121131916091](/images/image-20221121131916091.png)

![image-20221121132024668](/images/image-20221121132024668.png)

## &Mybatis

![image-20221121161514152](/images/image-20221121161514152.png)

### @Mapper&@MapperScan

![image-20221121161609495](/images/image-20221121161609495.png)

![image-20221121161621789](/images/image-20221121161621789.png)

![image-20221121161640952](/images/image-20221121161640952.png)

![image-20221121161628019](/images/image-20221121161628019.png)

![image-20221121161649372](/images/image-20221121161649372.png)

### &Spring事务

#### Spring中的事务管理：

1）：管理事务的对象：事务管理器（接口，接口有很多实现类）

使用JDBC或Mybatis访问数据库，使用**事务管理器DataSourceTransactionManager**

2）：**声明式事务**：使用注解说明事务控制的内容--**底层使用 AOP 原理**

**控制事务：隔离级别；传播行为；超时时间**

3）：事务的处理方式：

1.**Spring中的@Transactional注解**

2.aspectj框架可以再xml文件中声明事务的内容

![image-20221121180257137](/images/image-20221121180257137.png)

#### 隔离级别

![image-20221121175430623](/images/image-20221121175430623.png)

#### 传播行为

![image-20221121175258014](/images/image-20221121175258014.png)

![image-20221121175900789](/images/image-20221121175900789.png)

#### 超时时间

![image-20221121175509079](/images/image-20221121175509079.png)

## REST风格

**REST风格：使用url表示资源；使用http动作操作资源**

**RESTful风格**中，当请求路径中将某些数据通过路径的方式传输到服 务器中，就可以在相应的@RequestMapping注解的value属性中通过占位符{xxx}表示传输的数据，在 **通过@PathVariable注解，将占位符所表示的数据赋值给控制器方法的形参**

**url地址+请求方式确保是唯一**的 否则系统无法辨别 **导致启动出错**

![image-20221027163300977](/images/image-20221027163300977.png)

**http请求中仅支持get以及post请求** 

### 使用PUT&DELETE请求

**org.springframework.web.filter.HiddenHttpMethodFilter**

若需要实现put以及delete请求需要使用**HiddenMethodFilter**通过**对post请求进行包装（装饰者模式）**成**put或delete请求**

![image-20221121184206446](/images/image-20221121184206446.png)

@GetMapping

@PostMapping

@PutMapping

@DeleteMapping

## &Redis

![image-20221121224051661](/images/image-20221121224051661.png)

### Template对象

```java
StringRedisTemplate
//对于key和value都是使用的是String字符串的序列化；可读性好；

RedisTemplate
//对于key和value都是经过序列化的内容;无法直接识别（默认使用jdk的序列化）
```

![image-20221121223612417](/images/image-20221121223612417.png)

### Redis序列化

**序列化：把对象转化为可传输的字节序列过程称为序列化**

**反序列化：把字节序列还原为对象的过程称为反序列化**



**为什么需要序列化：为了对象可以跨平台传输；进行网络传输。**



跨平台储存的方式网络传输IO；IO支持的格式就是字节数组。（序列化数据）

Java的序列化：将Java对象转换为Byte[ ]数组（二进制数据）

json序列化与反序列化：JSON格式和对象格式的相互转换

### 设置RedisTemplate序列化

![image-20221121225243510](/images/image-20221121225243510.png)

### JackSon（JSON序列化）

![image-20221121233237625](/images/image-20221121233237625.png)

## Spring Cache

[A Guide To Caching in Spring | Baeldung](https://www.baeldung.com/spring-cache-tutorial)

![image-20230107101628272](/images/image-20230107101628272.png)

**基于注解（annotation）的缓存（cache）技术**，它本质上不是一个具体的缓存实现方案（比如EHCache 或者 OSCache），而是一个对缓存使用的抽象，通过在既有代码中加入少量它定义的各种 annotation，即能够达到缓存方法的返回对象的效果

![image-20230107102028639](/images/image-20230107102028639.png)



![image-20230107101942722](/images/image-20230107101942722.png)

![image-20230107102236925](/images/image-20230107102236925.png)

### Spring 框架自带的CacheManager(内存层面的缓存)

**底层基于ConcurrentHashMap实现的 程序停止则缓消失**

```java
@Slf4j
@SpringBootApplication
@EnableCaching//启动Cache缓存注解
public class CacheDemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(CacheDemoApplication.class,args);
        log.info("项目启动成功...");
    }
}
```



```java
@RestController
@RequestMapping("/user")
@Slf4j
public class UserController {

    @Autowired
    private CacheManager cacheManager;//Spring 框架自带的CacheManager(内存层面的缓存)

    @Autowired
    private UserService userService;

    /**
     * CachePut：将方法返回值放入缓存
     * value：缓存的名称，每个缓存名称下面可以有多个key
     * key：缓存的key
     */
    @CachePut(value = "userCache",key = "#user.id")
    @PostMapping
    public User save(User user){
        userService.save(user);
        return user;
    }

    /**
     * CacheEvict：清理指定缓存
     * value：缓存的名称，每个缓存名称下面可以有多个key
     * key：缓存的key
     */
    @CacheEvict(value = "userCache",key = "#p0")
    //@CacheEvict(value = "userCache",key = "#root.args[0]")
    //@CacheEvict(value = "userCache",key = "#id")
    @DeleteMapping("/{id}")
    public void delete(@PathVariable Long id){
        userService.removeById(id);
    }

    //@CacheEvict(value = "userCache",key = "#p0.id")
    //@CacheEvict(value = "userCache",key = "#user.id")
    //@CacheEvict(value = "userCache",key = "#root.args[0].id")
    @CacheEvict(value = "userCache",key = "#result.id")
    @PutMapping
    public User update(User user){
        userService.updateById(user);
        return user;
    }

    /**
     * Cacheable：在方法执行前spring先查看缓存中是否有数据，如果有数据，则直接返回缓存数据；若没有数据，调用方法并将方法返回值放到缓存中
     * value：缓存的名称，每个缓存名称下面可以有多个key
     * key：缓存的key
     * condition：条件，满足条件时才缓存数据
     * unless：满足条件则不缓存
     */
    //@Cacheable(value = "userCache",key = "#id",condition = "#result != null")
    @Cacheable(value = "userCache",key = "#id",unless = "#result == null")
    @GetMapping("/{id}")
    public User getById(@PathVariable Long id){
        User user = userService.getById(id);
        return user;
    }

    @Cacheable(value = "userCache",key = "#user.id + '_' + #user.name")
    @GetMapping("/list")
    public List<User> list(User user){
        LambdaQueryWrapper<User> queryWrapper = new LambdaQueryWrapper<>();
        queryWrapper.eq(user.getId() != null,User::getId,user.getId());
        queryWrapper.eq(user.getName() != null,User::getName,user.getName());
        List<User> list = userService.list(queryWrapper);
        return list;
    }
}
```

### Spring Cache 整合Redis 进行缓存

![image-20230107105942759](/images/image-20230107105942759.png)

**application.yml**

```yaml
  #配置redis
  redis:
    host: 192.168.199.152
    port: 6379
    database: 0
   #配置spring cache
  cache:
  	type: redis
    redis:
      time-to-live: 1800000 #配置缓存存活时间(过期时间)
```

**启动类**

```java
/**
 @author EddieZhang
 @create 2023-01-01 16:18
 */
@org.springframework.boot.autoconfigure.SpringBootApplication
@Slf4j
@MapperScan("com.eddie.reggie.mapper")
@ServletComponentScan//TODO 开启Servlet组件扫描 用来扫描@WebFilter的filter
@EnableTransactionManagement//TODO 开启事务管理
@EnableCaching//TODO 开启Cache的注解
public class SpringBootApplication {
    public static void main (String [] args){
        SpringApplication.run(SpringBootApplication.class,args);
    }
}
```

**实体类**

所有涉及到缓存的实体类都要implements Serializable实现可序列化接口

![image-20230107124705835](/images/image-20230107124705835.png)



```java
/**
 * 套餐管理
 @author EddieZhang
 @create 2023-01-03 18:12
 */
@RestController
@RequestMapping("/setmeal")
@Slf4j
public class SetmealController {
    @Autowired
    private SetmealService setmealService;
    @Autowired
    private SetmealDishService setmealDishService;
    @Autowired
    private CategoryService categoryService;

    /**
     * 添加套餐
     * @param setmealDto
     * @return
     */
    @PostMapping
    @CacheEvict(cacheNames = {"SetmealCache"},allEntries = true)//清除cacheNames = "SetmealCache"这一类缓存中的所有数据
    public R<String> save(@RequestBody SetmealDto setmealDto) {
        setmealService.saveWithDish(setmealDto);
        return R.success("新增套餐操作成功");
    }

    @GetMapping("/page")
    public R<Page> page(int page, int pageSize, String name) {
        //构造page构造器
        Page<Setmeal> pageInfo = new Page<>(page, pageSize);
        Page<SetmealDto> setmealDtoPageInfo = new Page<>(page, pageSize);

        //处理Setmeal的pageInfo
        //构建queryWrapper构造器
        LambdaQueryWrapper<Setmeal> setmealLambdaQueryWrapper = new LambdaQueryWrapper<>();
        //添加查询条件
        setmealLambdaQueryWrapper.like(StringUtils.isNotEmpty(name), Setmeal::getName, name);
        //根据updateTime进行降序排序
        setmealLambdaQueryWrapper.orderByDesc(Setmeal::getUpdateTime);
        //进行分页查询
        setmealService.page(pageInfo, setmealLambdaQueryWrapper);

        List<Setmeal> records = pageInfo.getRecords();
        List<SetmealDto> list = records.stream()
                .map((item) -> {
                    SetmealDto setmealDto = new SetmealDto();
                    Category category = categoryService.getById(item.getCategoryId());
                    if (category != null) {
                        setmealDto.setCategoryName(category.getName());
                    }
                    BeanUtils.copyProperties(item, setmealDto);
                    return setmealDto;
                })
                .collect(Collectors.toList());

        //处理SetmealDto的pageInfo
        //进行对象copy 并且忽略掉records字段(不进行records字段的cp)
        BeanUtils.copyProperties(pageInfo, setmealDtoPageInfo, "records");
        setmealDtoPageInfo.setRecords(list);

        //将SetmealDto的pageInfo返回
        return R.success(setmealDtoPageInfo);
    }


    /**
     * 删除套餐
     * @param ids
     * @return
     */
    @DeleteMapping
    @CacheEvict(cacheNames = {"SetmealCache"},allEntries = true)//清除cacheNames = "SetmealCache"这一类缓存中的所有数据
    public R<String> delete(@RequestParam List<Long> ids) {
        setmealService.removeWithDish(ids);
        return R.success("套餐删除成功");
    }

    /**
     * 停售套餐
     * @param ids
     * @return
     */
    @PostMapping("/status/0")
    public R<String> statusTo0(@RequestParam List<Long> ids) {
        //构造queryWrapper
        LambdaQueryWrapper<Setmeal> setmealLambdaQueryWrapper = new LambdaQueryWrapper<>();
        setmealLambdaQueryWrapper.in(ids != null, Setmeal::getId, ids);

        //根据ids查询到setmeal集合 并使用stream()的形式将获取到的setmeal的status设置为0
        List<Setmeal> setmealList = setmealService.list(setmealLambdaQueryWrapper);
        setmealList.stream()
                .map((item) -> {
                    item.setStatus(0);
                    return item;
                })
                .collect(Collectors.toList());

        //进行数据库update操作 批量更新setmeal的status
        setmealService.updateBatchById(setmealList);

        return R.success("停售套餐成功");
    }

    /**
     * 起售套餐
     * @param ids
     * @return
     */
    @PostMapping("/status/1")
    public R<String> statusTo1(@RequestParam List<Long> ids) {
        //构造queryWrapper
        LambdaQueryWrapper<Setmeal> setmealLambdaQueryWrapper = new LambdaQueryWrapper<>();
        setmealLambdaQueryWrapper.in(ids != null, Setmeal::getId, ids);

        //根据ids查询到setmeal集合 并使用stream()的形式将获取到的setmeal的status设置为1
        List<Setmeal> setmealList = setmealService.list(setmealLambdaQueryWrapper);
        setmealList.stream()
                .map((item) -> {
                    item.setStatus(1);
                    return item;
                })
                .collect(Collectors.toList());

        //进行数据库update操作 批量更新setmeal的status
        setmealService.updateBatchById(setmealList);

        return R.success("起售套餐成功");
    }

    /**
     * 根据id进行SetmealDto查询
     * @param id
     * @return
     */
    @GetMapping("/{id}")
    public R<SetmealDto> getById(@PathVariable("id") Long id) {
        SetmealDto setmealDto = setmealService.getByIdWithSetmealDish(id);
        return R.success(setmealDto);
    }


    /**
     * 修改SetmealDto
     * @param setmealDto
     * @return
     */
    @PutMapping
    @CacheEvict(cacheNames = {"SetmealCache"},allEntries = true)//清除cacheNames = "SetmealCache"这一类缓存中的所有数据
    public R<String> putSetmealDto(@RequestBody SetmealDto setmealDto) {
        setmealService.updateSetmealWishDish(setmealDto);
        return R.success("修改套餐成功");
    }


    //TODO Redis结合Spring Cache 进行缓存
    @GetMapping("/list")
    @Cacheable(cacheNames = {"SetmealCache"}, key = "#setmeal.categoryId + '_' + #setmeal.status", unless = "#result == null")
    /*
        cacheNames = "SetmealCache" 缓存的alias（类似于一类缓存）
        ☆key = "#setmeal.categoryId + '_' + #setmeal.status" 缓存的key 类似与一类缓存中的具体一份缓存
        unless = "#result == null" 缓存的条件
    */
    public R<List<SetmealDto>> getSetmealDtoById(Setmeal setmeal) {
        //查询setmealDish数据
        LambdaQueryWrapper<SetmealDish> setmealDishLambdaQueryWrapper = new LambdaQueryWrapper<>();
        setmealDishLambdaQueryWrapper.eq(setmeal.getId() != null, SetmealDish::getSetmealId, setmeal.getId());
        List<SetmealDish> setmealDishList = setmealDishService.list(setmealDishLambdaQueryWrapper);

        //查询setmeal数据
        //构建queryWrapper
        LambdaQueryWrapper<Setmeal> setmealLambdaQueryWrapper = new LambdaQueryWrapper<>();
        setmealLambdaQueryWrapper.eq(setmeal.getCategoryId() != null, Setmeal::getCategoryId, setmeal.getCategoryId());
        setmealLambdaQueryWrapper.eq(Setmeal::getStatus, 1);
        List<Setmeal> setmeals = setmealService.list(setmealLambdaQueryWrapper);
        List<SetmealDto> setmealDtoList = setmeals.stream()
                .map((item) -> {
                    SetmealDto setmealDto = new SetmealDto();
                    BeanUtils.copyProperties(item, setmealDto);
                    setmealDto.setSetmealDishes(setmealDishList);
                    return setmealDto;
                })
                .collect(Collectors.toList());

        return R.success(setmealDtoList);
    }

}
```

![image-20230107124830306](/images/image-20230107124830306.png)

### 自定义Spring Cache配置

```java
package com.eddie.mall_goods.config;

import lombok.extern.slf4j.Slf4j;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.autoconfigure.cache.CacheProperties;
import org.springframework.boot.context.properties.EnableConfigurationProperties;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.redis.cache.RedisCacheConfiguration;
import org.springframework.data.redis.serializer.GenericJackson2JsonRedisSerializer;
import org.springframework.data.redis.serializer.RedisSerializationContext;
import org.springframework.data.redis.serializer.StringRedisSerializer;

/**
 @author EddieZhang
 @create 2023-01-31 6:52 PM
 */
@Configuration
@EnableConfigurationProperties(CacheProperties.class)
/*
    @ConfigurationProperties(prefix = "spring.cache")
    public class CacheProperties {
*/
@Slf4j
public class MySpringCacheConfig {

    @Autowired
    private CacheProperties cacheProperties;

    @Bean
    public RedisCacheConfiguration customRedisCacheConfiguration(){
        //获取默认的cache配置 后续的定制修改覆盖掉默认配置即可
        RedisCacheConfiguration defaultCacheConfig = RedisCacheConfiguration.defaultCacheConfig();
        //指定key的序列化
        defaultCacheConfig = defaultCacheConfig.serializeKeysWith(
                RedisSerializationContext.SerializationPair.fromSerializer(new StringRedisSerializer()));
        //指定value的序列化
        defaultCacheConfig = defaultCacheConfig.serializeValuesWith(
                RedisSerializationContext.SerializationPair.fromSerializer(new GenericJackson2JsonRedisSerializer()));

        CacheProperties.Redis redis = cacheProperties.getRedis();
        //指定time-to-live: 配置缓存存活时间(过期时间) 等相关配置 从yaml配置文件中获取
        //如果yaml文件中没有配置就使用defaultCacheConfig默认的配置
        
        if (redis.getTimeToLive() != null) {//配置ddl缓存的存活时间
            defaultCacheConfig = defaultCacheConfig.entryTtl(redis.getTimeToLive());
        }
        if (redis.getKeyPrefix() != null) {
            //配置key的前缀 没有配置就使用缓存的cacheNames作为前缀(推荐不配置 使用cacheNames作为前缀)
            defaultCacheConfig = defaultCacheConfig.prefixKeysWith(redis.getKeyPrefix());
        }
        if (!redis.isCacheNullValues()) {//TODO 是否缓存null值 防止缓存穿透
            defaultCacheConfig = defaultCacheConfig.disableCachingNullValues();
        }
        if (!redis.isUseKeyPrefix()) {//是否使用key前缀
            defaultCacheConfig = defaultCacheConfig.disableKeyPrefix();
        }
        return defaultCacheConfig;
    }

}

```



![image-20230131193349472](/images/image-20230131193349472.png)



![image-20230131194645236](/images/image-20230131194645236.png)



![image-20230131193247657](/images/image-20230131193247657.png)

### 常用注解

| @EnableCaching | 开启注解 在启动类上使用                                      |
| -------------- | ------------------------------------------------------------ |
| @CacheConfig   | 类上使用**指定整个类中的所有方法的cacheNames** 类中的方法可以共享相同的缓存配置 |
| @Cacheable     | 方法上使用 共用类上@CacheConfig指定的cacheNames *@Cacheable* will **skip running the method** <br />若**缓存中没有**则执行方法 **将方法的结果缓存到redis中**  **若查询到缓存中有 则不用执行方法 直接从缓存中获取结果**<br />指定参数**cacheNames(分区名)** **key（分区下细分的key名）** 以及 **sync(读模式下的同步【本地锁】)**<br />**读模式** |
| @CacheEvict    | 清除缓存 可以指定**allEntries()** default false;为**true** 表明**同时清除cacheNames分区下的所有key的缓存**<br />数据一致性之**缓存失效方式**<br />**写模式** |
| @CachePut      | 更新缓存 *@CachePut* will **actually run the method** and then put its results in the cache 不影响方法执行的更新（重写）缓存<br />数据一致性之**双写模式**<br />**写模式** |
| @Caching       | can **group multiple caching annotations** with *@Caching*, and use it to implement our own customized caching logic <br />**组合多个缓存操作** 形成一个缓存操作组<br />**写模式** |

**Spel表达式**

The SpEL expression evaluates against a dedicated context that provides the following meta-data:
**#root.method, #root.target**, and **#root.caches** for references to the method, target object, and affected cache(s) respectively.
Shortcuts for the method name (**#root.methodName**) and target class (**#root.targetClass**) are also available

### SpringCache总结

读多写少读数据一致性要求不高的直接用SpringCache (读模式要求数据一致性的可以@Cacheable（sync = true）加本地同步锁),



写数据可以加读写锁/引入Canal（模拟MySQL从库 感知更新数据库），（分布式情况下高并发 数据一致性要求高的可以加分布式锁【Redisson】）



读多写多直接查数据库



根据自己的业务需求进行设计

## &Dubbo

### Spring Boot 整合 Dubbo & Zookeeper 

![image-20221115121936603](/images/image-20221115121936603.png)

![image-20221115121951179](/images/image-20221115121951179.png)

![image-20221115121959552](/images/image-20221115121959552.png)

![image-20221115122009262](/images/image-20221115122009262.png)

![image-20221115122015949](/images/image-20221115122015949.png)

![image-20221115122025070](/images/image-20221115122025070.png)

## .war&.jar

### .jar：打包Java文件	

**内嵌有tomcat服务器 可以独立运行**

![image-20221122131720576](/images/image-20221122131720576.png)

![image-20221122132847108](/images/image-20221122132847108.png)

#### 命令行启动参数设置

![image-20221122142433911](/images/image-20221122142433911.png)

### .war：打包web项目

![image-20221122131705265](/images/image-20221122131705265.png)

**打包好的.war文件可以放到tomcat服务器中运行**

![image-20221122131745563](/images/image-20221122131745563.png)

## SpringBoot项目运行方式

### 在IDEA中直接运行SpringBoot程序的main方法（开发阶段）

### 用Maven将SpringBoot项目打包为jar包，使用Java命令（cmd）运行（上线部署阶段）

#### cmd中启动

Java -jar springboot-xxx.jar

#### 在Linux中部署启动

封装命令为shell脚本在Linux中部署运行

1）：创建shell脚本文件

```
vim run.sh
```

2）：编写shell脚本

```shell
#！/bin/sh
Java -jar 【.jar文件】
```

3）：赋权限

```
chomd 777 run.sh
```

4）：启动shell脚本

```
./run.sh
```

## Thymeleaf

https://www.thymeleaf.org/doc/tutorials/3.1/usingthymeleaf.html

**Thymeleaf：是使用Java开发的模板技术**；在**服务端运行**。把处理后的数据发送给浏览器。

模板做视图层工作的。用来显示数据的。

基于HTML语言；应用在HTML中。

### SpringBoot集成了Thymeleaf

![image-20221122151741138](/images/image-20221122151741138.png)

![image-20221122151841470](/images/image-20221122151841470.png)

![image-20221122151500438](/images/image-20221122151500438.png)

## Spring Boot 注解

[(5条消息) SpringBoot注解最全详解(整合超详细版本)_VV-酱的博客-CSDN博客](https://blog.csdn.net/weixin_40753536/article/details/81285046)

| @SpringBootApplication |      |
| ---------------------- | ---- |
| @Configuration         |      |
| @Bean                  |      |
|                        |      |



