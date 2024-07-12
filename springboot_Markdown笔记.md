SpringBoot2

- 核心技术
- 响应式编程

# 一.基础入门

- SpringBoot2的功能：能快速创建出生产级别的Spring应用

- SpringBoot2的优点：

1. 创建独立spring应用
2. 内嵌web服务器
3. 自动starter依赖，简化构建配置
4. 自动配置Spring以及第三方功能
5. 提供生产级别的监控、健康检查及外部化配置
6. 无代码生成、无需编写XML

## 1.SpringBoot2入门

- 添加Maven.xml的配置

```xml
<mirrors>
    <mirror>
        <id>alimaven</id>
        <name>aliyun maven</name>
        <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
        <mirrorOf>central</mirrorOf>
    </mirror>
</mirrors>
<profiles>
    <profile>
        <id>jdk8</id>
        <activation>
            <activeByDefault>true</activeByDefault>
            <jdk>1.8</jdk>
        </activation>
        <properties>
            <maven.compiler.source>1.8</maven.compiler.source>
            <maven.compiler.target>1.8</maven.compiler.target>
            <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>
        </properties>
    </profile>
</profiles>
```

## 2.HelloWorld

需求:浏览发送/hello请求，响应 Hello，Spring Boot 2

1. 创建Maven工程
2. 引入依赖

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.uestc</groupId>
    <artifactId>boot-01-helloworld</artifactId>
    <version>1.0-SNAPSHOT</version>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.7.18</version>
    </parent>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
</project>
```

2. 创建主程序

```java
package com.uestc.boot;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

/*
@SpringBootApplication:这是一个springBoot应用

 */
@SpringBootApplication
public class MainApplication {
    public static void main(String[] args) {
        SpringApplication.run(MainApplication.class, args);
    }
}
```

3. 编写业务

```java
package com.uestc.boot.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;
import org.springframework.web.bind.annotation.RestController;

//@ResponseBody
//@Controller
@RestController
public class HelleController {

    @RequestMapping("/hello")
    public String hello() {
        return "hello, Spring boot 2";
    }
}
```

4. 配置文件：application.properties
5. Maven打包clear -> package
6. 启动服务

```cmd
java -jar boot-01-helloworld-1.0-SNAPSHOT.jar
```

## 3.自动配置原理

### 1.SpringBoot特点

- 1.1依赖管理:查看父类的父类的配置文件

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.7.18</version>
</parent>
->父类
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-dependencies</artifactId>
    <version>2.7.18</version>
</parent>
->父类
```

- 修改版本号：

  1. 查看spring-boot-dependencies里面规定当前依赖的版本用的key
  2. 在当前项目里面重写配置

  ```xml
  <properties>
      <mysql.version>5.1.43</mysql.version>
  </properties>
  ```

- starter场景启动器：maven的特性
  1. 见到很多 spring-boot-starter-* , *表示某种场景
  2. 只要引入starter，这个场景的所有常规需要的依赖我们都自动引入
  3. 查看所有支持的starters
- 1.2自动配置
  - 自动配好Tomcat
  - 自动配好SpringMVC
  - 自动配好Web常见功能，如:字符编码问题
  - 默认的包结构
    - 无需以前的包扫描配置
    - 主程序所在包及其下面的所有子包里面的组件都会被默认扫描进来
    - @SpringBootApplication(scanBasePackages = "com.uestc") 或 @ComponentScan可以设置包的扫描范围
  - 各种配置拥有默认值
    - 各种配置都有对应的类
    - 默认配置最终都是映射到MultipartPreperties
  - 按需加载所有自动配置项
    - 被引入的场景才会开启自动配置
    - SpringBoot所有的自动配置功能都在 spring-boot-autoconfigure 包里面

### 2.容器功能

- 2.1组件添加
- @Configuration
  - 基本使用
  - Full模式(proxyBeanMethods =true)：单实例模式，每次调用都是容器里的实例
  - Lite模式(proxyBeanMethods =false)：每次创建新的实例

```java
package com.uestc.boot;

import com.uestc.boot.bean.Pet;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ConfigurableApplicationContext;

/*
@SpringBootApplication:这是一个springBoot应用

 */
@SpringBootApplication(scanBasePackages = "com.uestc")
public class MainApplication {
    public static void main(String[] args) {
        // 1. 返回我们IOC容器
        ConfigurableApplicationContext run = SpringApplication.run(MainApplication.class, args);
        // 2. 查看容器里面的组件
        String[] names = run.getBeanDefinitionNames();
        for (String name : names) {
            System.out.println(name);
        }
        // 3. 从容器中获取组件
        // 如果@configuration(proxyBeanMethods =true(默认))代理对象调用方法。
        Pet tomPet = run.getBean("tomPet", Pet.class); // 单实例
        Pet tomPet2 = run.getBean("tomPet", Pet.class);
        // 多次获取到同一个对象
        System.out.println(tomPet);
        System.out.println(tomPet2);
    }
}
```

- 声明组件：@Bean(普通组件)、@Component(普通组件)、@Controller(控制器组件)、@Service(服务器组件)、 @Repository(数据库组件)

- @Componentscan、 @lmport
  -  @lmport导入组件
  - @Import({User.class,DBHelper.class})：给容器中自动创建出这两个类型的组件，默认组件的名字就是全类名

- @Conditional：条件装配:满足Conditional指定的条件，则进行组件注入
  - @ConditionalonBean(name = "tom") ：存在tom组件时才会注册装配

- 2.2添加spring的xml配置文件
  - @ImportResource("classpath:beans.xml")：在配置类中添加xml的配置文件

- 2.3配置绑定

  - 如何使用Java读取到properties文件中的内容，并且把它封装到JavaBean中，以供随时使用;
  - @Component + @ConfigurationProperties

  ```properties
  mycar.brand = BYD
  mycar.price = 100000
  ```

  ```java
  package com.uestc.boot.bean;
  
  import org.springframework.boot.context.properties.ConfigurationProperties;
  import org.springframework.stereotype.Component;
  
  // 容器内的组件才识别springboot的注解
  @Component
  @ConfigurationProperties(prefix = "mycar")
  public class Car {
      private String brand;
      private Integer price;
  
      public Car() {
      }
  
      public Car(String brand, Integer price) {
          this.brand = brand;
          this.price = price;
      }
  // ... get set 方法 
  }
  ```

  ```java
  @RestController
  public class HelleController {
      @Autowired
      private Car car;
      @RequestMapping("/car")
      public Car car() {
          return car;
      }
  }
  ```

  

  - @EnableConfigurationProperties + @ConfigurationProperties

  ```java
  // 配置文件中声明
  @Configuration // 声明配置类
  @EnableConfigurationProperties(Car.class)
  // 1、开启Car配置绑定功能
  // 2、把这个car这个组件自动注册到容器中
  public class MyConfig {
  }
  ```

  ```java
  package com.uestc.boot.bean;
  
  import org.springframework.boot.context.properties.ConfigurationProperties;
  import org.springframework.stereotype.Component;
  
  // 容器内的组件才识别springboot的注解
  @ConfigurationProperties(prefix = "mycar")
  public class Car {
      private String brand;
      private Integer price;
  
      public Car() {
      }
  
      public Car(String brand, Integer price) {
          this.brand = brand;
          this.price = price;
      }
  // ... get set 方法 
  }
  ```

  - @ConfigurationProperties

### 3.自动配置原理

- 3.1引导加载自动配置类

  - @SpringBootConfiguration：SpringBoot的配置类
  - @ComponentScan：指定扫描哪些，Spring注解

  ```java
  @AutoConfigurationPackage
  @Import({AutoConfigurationImportSelector.class})
  public @interface EnableAutoConfiguration {
      ...
  }
  ```

  - @EnableAutoConfiguration：

  ```java
  @AutoConfigurationPackage
  @Import({AutoConfigurationImportSelector.class})
  public @interface EnableAutoConfiguration {
      ...
  }
  ```

  ```java
  // @AutoConfigurationPackage
  @Import({AutoConfigurationPackages.Registrar.class})
  // 利用Registrar给容器中导入一系列组件
  // 把某一个包下的组件批量注册
  public @interface AutoConfigurationPackage { 
      ...
  ```

  spring-boot-autoconfigure-2.3.4.RELEASE.jar包里面也有META-INF/spring.factories配置了所有需要注册的组件(127个)

- 3.2.按需开启自动配置项：根据条件配置规则按需装配

  - SpringBoot默认会在底层配好所有的组件。但是如果用户自己配置了以用户的优先

  - @ConditionalonMissingBean：底层的默认配置



- 总结：

  - SpringBoot先加载所有的自动配置类

  - 每个自动配置类按照条件进行生效，默认都会绑定配置文件指定的值。配置信息在xxxxProperties里面拿，xxxProperties和配置文件进绑定。

  - 生效的配置类就会给容器中装配很多组件

  - 只要容器中有这些组件，相当于这些功能就有了

  - 只要用户有自己配置的，就以用户的优先。

  - 定制化配置

    - 方法1：用户直接自己写@Bean类替换底层的组件
    - 方法2：用户去修改组件是获取的配置文件中的值，覆盖原来的值

    xxxxxAutoConfiguration--->组件 --->xxxxProperties里面拿值 ---->application.properties

- 3.3最佳实践
  - 引入场景依赖
  - 查看自动配置的内容
    - application.properties文件中设置debug=true，SpringBoot启动会打印开启的配置报告
    - Negative(不生效)\Positive(生效)
  - 是否需要修改
    - 参照文档修改配置项
      - 查看官方文档：[Spring Boot Reference Documentation](https://docs.spring.io/spring-boot/docs/2.7.18/reference/htmlsingle/#appendix.application-properties)
      - debug分析
    - 自定义加入或者替换组件：用户配置优先
      - @Bean、@Component.
    - 自定义器 XXXXXCustomizer;

## 4.开发技巧

### 1.LomBok的使用

- 添加依赖

```java
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    </dependency>
```

- 安装LomBok插件
- @Data:为Bean生成get/set方法
- @ToString:生成toString方法
- 构造器/方法
  - @NoArgsConstructor：无参构造器
  - @AllArgsConstructor：有参构造器

```java
@Data
@ToString
@NoArgsConstructor
@AllArgsConstructor
public class Pet {
    private String name;
}
```

- @EqualsAndHashCode：Equals方法和HashCode方法

- @slf4j:日子工具

```java
@RestController
@Slf4j
public class HelleController {
    @RequestMapping("/hello")
    public String hello() {
        log.info("日志：进入请求");
        return "hello, Spring boot 2 你好";
    }
}
```

### 2.dev-tools

- 自动重启：ctrl+F9

## 3.Spring Initializr

- IDEA直接构建SpringBoot项目

# 二.核心功能

## 1.配置文件

### 1.YAML标记语言

- 基本语法
  - key: value;kv之间有空格
  - 大小写敏感
  - 用缩进表示层级关
  - 缩进不允许使用tab，只允许空格
  - 宿进的空格数不重要，只要相同层级的元素左对齐即可
  - '#'表示注释
  - "与"表示字符串内容 会被 转义/不转义

- 数据类型

  - 字面量:单个的、不可再分的值。date、boolean、string、number、null

  ```yaml
  k: v
  ```

  - 对象：键值对的集合。map、hash、set、object

  ```yaml
  k: {k1: v1, k2: v2}
  k:
  	k1: v1
  	k2: v2
  
  ```

  - 数组：一组按次序排列的值。array、list、queue

  ```yaml
  k: [v1, v2, v3]
  k:
  - v1
  - v2
  - v3
  ```

- 使用Yaml注入JavaBean
  - properties和yaml的配置文件可以同时生效

```yaml
person:
  username: zhangsan
# 单引号会将 \n作为字符串输出 双引号会将 \n 作为换行输出 -- 有区别
  boss: true
  birth: 2019/12/9
  age: 18
  interests:
  - 篮球
  - 足球
  - 18
  animal: [阿猫,阿狗]
  score: {english: 80,math: 90}
  salary:
  - 9999.98
  - 9999.99
  pet:
    name: 阿狗
    weight: 99.99

  allPets:
    sick:
    - { name: 阿狗,weight: 99.99 }
    - name: 阿猫
    - weight: 88.88
    - name: 阿虫
    - weight: 77.77
    health:
      - { name: 阿花,weight: 19.99 }
      - { name: 阿草,weight: 29.99 }
```

```java
@ConfigurationProperties(prefix = "person")
@Component
@Data
@ToString
public class Person {
    private String username;
    private Boolean boss;
    private Date birth;
    private Integer age;
    private Pet pet;
    private String[] interests;
    private List<String> animal;
    private Map<String,Object> score;
    private Set<Double> salary;
    private Map<String,List<Pet>> allPets;
}
```

```java
@RestController
public class HelleController {
    @Autowired
    private Person person;
    @RequestMapping("/person")
    public Person person() {
        return person;
    }
}
```

- 添加提示插件：写yaml配置文件时增加提示功能

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-configuration-processor</artifactId>
</dependency>
```

```xml
<build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <configuration>
                    <excludes>
                        <dependency>
                            <groupId>org.springframework.boot</groupId>
                            <artifactId>spring-boot-configuration-processor</artifactId>
                        </dependency>
                    </excludes>
                </configuration>
            </plugin>
        </plugins>
    </build>
<!--配置不打包该配置-->
```

## 2.Web开发

![web开发知识结构](.\springboot_Markdown笔记图片\web开发知识结构.png)

### 1.SpringMVC自动配置概览

- 配置内容
  - 内容协商视图解析器和BeanName视图解析器
  - 静态资源(包括webjars)
  - 自动注册 Converter，Genericconverter，Formatter
  - 支持 HttpMessageConverters(后来我们配合内容协商理解原理)
  - 静态index.html 页支持
  - 自定义 Favicon
  - 自动使用 configurablewebBindingInitializer(DataBinder负责将请求数据绑定到JavaBean上)

### 2.简单功能分析

#### 2.1静态资源访问

1. 静态资源目录：类路径下:resources /static(or /public or /resources or /META-INF/resources)
2. 访问: 当前项目根路径/+静态资源名
3. 访问顺序：controller -> 静态资源处理器 -> 都无法处理404

##### 2.1.1设置静态资源访问前缀

- 默认为无前缀
- 修改访问路径：工程目录/res/静态文件名

```yaml
spring:
  mvc:
    static-path-pattern: /res/**
```

- 修改静态资源路径

```yaml
  web:
    resources:
      static-locations: [classpath:/haha]
```

##### 2.1.2webjars:访问依赖包内的静态资源

#### 2.2欢迎页支持

- 静态资源路径下 index.html
  - 可以配置静态资源路径
  - 但是不可以配置静态资源的访问前缀。否则导致index.html不能被默认访问

```yaml
#spring:
#  mvc:
#    static-path-pattern: /res/**
# 会导致index配置失效
```

- controller能处理/index

#### 2.3自定义favicon.ico

- favicon.ico：设置网页的默认图标，放在静态资源目录下，以favicon.ico命名

#### 2.4静态资源配置原理

- SpringBoot启动默认加载 xxxAutoConfiguration类(自动配置类)
- SpringMVC功能的自动配置类WebMvcAutoConfiguration，生效
  - 配置文件的相关属性和x进行了绑定。WebMvProperties==spring.mvc\ResourceProperties==spring.resources
- 看源码的施行流程

### 3.请求参数处理。

#### 0.请求映射

- @xxxMapping;

- Rest风格支持(使用ITTP请求方式动词来表示对资源的作)

  - 以前:/getUser 获取用户 /deleteUser删除用户 /editUser 修改用户 /saveUser 保存用户

  - 现在:/user GET-获取用户 DELETE-删除用户 PUT-修改用户 POST-保存用户

  - 核心Filter:HiddenHttpMethodFilter

    - 用法:表单method=post，隐藏域 _method=put
    - SpringBoot中手动开启

    ```yaml
    spring:
      mvc:
        hiddenmethod:
          filter:
            enabled: true
    ```

- Rest原理(表单提交要使用REST的时候)

  - 表单提交会带上 method=PUT
  - 请求过来被HiddenHttpMethodFilter拦截
  -  请求是否正常，并且是POST
    - 获取到 method的值。
    - 兼容以下请求:PUT.DELETE.PATCH
    - 原生request(post)，包装模式requesWrapper重写了getMethod方法，返回的是传入的值。
    - 过滤器链放行的时候用wrapp数r。以后的方法调用getMethod是调用requesWrapper的。

- Rest使用客户端工具
  - 如PostMan直接发送Put、delete等方式请求，无需Filter。

```java
package com.uestc.boot;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class TestController {
    // GetMapping("/user")
    @RequestMapping(value = "/user", method = RequestMethod.GET)
    public String getUser() {
        return "GET - 张三";
    }
    // PostMapping("/user")
    @RequestMapping(value = "/user", method = RequestMethod.POST)
    public String postUser() {
        return "POST - 张三";
    }
    // PutMapping("/user")
    @RequestMapping(value = "/user", method = RequestMethod.PUT)
    public String putUser() {
        return "PUT - 张三";
    }
    // DeleteMapping("/user")
    @RequestMapping(value = "/user", method = RequestMethod.DELETE)
    public String deleteUser() {
        return "DELETE - 张三";
    }
}
```

- 创建新的HiddenHttpMethodFilter对象，修改对应的参数即可

- 所有请求都会调用doDispatch()方法
- RequestMappingHandlerMapping:保存了所有@RequestMapping 和handler的映射规则。
- 所有的请求映射都在HanderMapping中。
  - SpringBoot自动配置欢迎页的HanderMapping。访问/能访问到index.html
  - 请求进来，挨个尝试所有的HanderMapping看是否有请求信息。
  - 如果有就找到这个请求对应的handler
  - 如果没有就是下一个HandrrMapping
  - 我们需要一些自定义的映射处理，我们也可以自己给容器中放HandlerMapping。自定义HandlerMapping

#### 1.普通参数与基本注解

- 注解

  - @PathVariable
  - @RequestHeader
  - @RequestParam
  - @CookieValue

  ```html
  <a href="car/3/owner/zyp1?age=18&hobbies=bs&hobbies=swim">转跳：/car/{id}/owner/{username}</a>
  ```

  ```java
  // 获取路径变量
  @RequestMapping("/car/{id}/owner/{username}")
  public Map<String, Object> getCar(@PathVariable("id") Integer id,
                                    @PathVariable("username") String name,
                                    @PathVariable Map<String, String> pv,
                                    @RequestHeader("User-Agent") String userAgent,
                                    @RequestHeader Map<String, String> header,
                                    @RequestParam("hobbies")List<String> hobbies,
                                    @RequestParam("age") Integer age,
                                    @CookieValue("apt.uid") String Cookie) {
      Map<String, Object> map = new HashMap<>();
      map.put("id", id);
      map.put("username", name);
      map.put("pv", pv);
      map.put("userAgent,", userAgent);
      map.put("header", header);
      map.put("hobbies", hobbies);
      map.put("age", age);
      map.put("Cookie", Cookie);
      return map;
  }
  ```

  - @RequestBody

  ```java
  @PostMapping("/save")
  public Map<String, Object> getCar(@RequestBody String content){
      HashMap<String, Object> map = new HashMap<>();
      map.put("content", content);
      return map;
  }
  ```

  - @RequestAttribute:获取请求域的参数

  ```java
  @Controller
  public class RequestController {
      @GetMapping("/goto")
      public String goTOPae(HttpServletRequest request) {
          request.setAttribute("msg", "成功");
          request.setAttribute("code", 200);
          return "forward:/success";
      }
      @ResponseBody
      @GetMapping("/success")
      public Map<String, Object> success(@RequestAttribute("msg") String msg,
                            @RequestAttribute("code") Integer code,
                            HttpServletRequest request) {
          Object msgAtt = request.getAttribute("msg");
          Map<String, Object> map = new HashMap<>();
          map.put("msg",msg);
          map.put("code", code);
          map.put("msgAtt", msgAtt);
          return map;
      }
  }
  ```

  - @MatrixVariable：获取矩阵变量

  1. 语法: /cars/sell;low=34;brand=byd,audi,yd

  2. SpringBoot默认是禁用了矩阵变量的功能：

     - 手动开启:原理。对于路径的处理。urlPathHelper进行解析。

     ```html
     矩阵变量测试:<br>
     <a href="cars/sell;low=34;brand=byd,audi,yd">@MatrixVariable矩阵变量</a>
     ```

     ```java
     // 需要绑定路径变量
     @GetMapping("/cars/{path}")
     public Map carsSell(@MatrixVariable("low") Integer low,
                         @MatrixVariable("brand") List<String> brand,
                         @PathVariable("path") String path) {
         Map<String, Object> map = new HashMap<>();
         map.put("low", low);
         map.put("brand", brand);
         map.put("path", path);
         return map;
     }
     ```

     - removeSemicolonContent(移除分号内容)支持矩阵变量的
     - 配置自己配置类->开启持矩阵变量

     - 开启方法1：实现WebMvcConfigurer接口

     ```java
     @Configuration(proxyBeanMethods = false)
     public class WebConfig implements WebMvcConfigurer {
         @Override
         public void configurePathMatch(PathMatchConfigurer configurer) {
             UrlPathHelper urlPathHelper = new UrlPathHelper();
             // 不移除;后面的内容。矩阵变量功能就可以生效
             urlPathHelper.setRemoveSemicolonContent(false);
             configurer.setUrlPathHelper(urlPathHelper);
         }
     }
     ```

     - 开启方法2：返回实现类

     ```java
     @Configuration(proxyBeanMethods = false)
     public class WebConfig /*implements WebMvcConfigurer*/ {
         @Bean
         public WebMvcConfigurer webMvcConfigurer() {
             return new WebMvcConfigurer() {
                 @Override
                 public void configurePathMatch(PathMatchConfigurer configurer) {
                     UrlPathHelper urlPathHelper = new UrlPathHelper();
                     urlPathHelper.setRemoveSemicolonContent(false);
                     configurer.setUrlPathHelper(urlPathHelper);
                 }
             };
         }
     }
     ```

  3. 获取同名ID

  ```html
  矩阵变量测试2:<br>
  <a href="boss/1;age=12/2;age=13">@MatrixVariable矩阵变量</a>
  ```

  ```java
  @GetMapping("/boss/{boss}/{emp}")
  public Map boss(@MatrixVariable(value = "age", pathVar = "boss") Integer bossAge,
                  @MatrixVariable(value = "age", pathVar = "emp") Integer empAge
                 ) {
      Map<String, Object> map = new HashMap<>();
      map.put("bossAge", bossAge);
      map.put("empAge", empAge);
      return map;
  }
  ```

  

- Servlet API

  - WebRequest、ServletRequest、MultipartRequest、 HttpSession、javax.servlet.http.PushBuilder、Principal、InputStream、Reader、HttpMethod、Locale、TimeZone、ZoneId
  - **ServletRequestMethodArgumentResolver  处理以上的部分参数**
    - **Map、Model类型的参数**，会返回 mavContainer.getModel（）；---> BindingAwareModelMap 是Model 也是Map
    - **mavContainer**.getModel(); 获取到值的



-  复杂参数

**Map**、**Model（map、model里面的数据会被放在request的请求域  request.setAttribute）、**Errors/BindingResult、**RedirectAttributes（ 重定向携带数据）**、**ServletResponse（response）**、SessionStatus、UriComponentsBuilder、ServletUriComponentsBuilder

- 自定义对象参数

  - 可以自动类型转换与格式化，可以级联封装。
  - POJO封装过程：**ServletModelAttributeMethodProcessor**
  - 参数处理原理
    - HandlerMapping中找到能处理请求的Handler（Controller.method()）
    - 为当前Handler 找一个适配器 HandlerAdapter； **RequestMappingHandlerAdapter**
    - 适配器执行目标方法并确定方法参数的每一个值
  - 自定义类型转换器

  ```html
  <form action="/save_user" method="post">
      姓名：<input name="name" value="ZhangSan" /> <br>
      年龄：<input name="age" value="18" /> <br>
      宠物：<input name="pet" value="猫猫,3"><br>
      <input type="submit" value="提交">
  </form>
  ```

  ```java
  @Configuration(proxyBeanMethods = false)
  public class WebConfig /*implements WebMvcConfigurer*/ {
      @Bean
      public WebMvcConfigurer webMvcConfigurer() {
          return new WebMvcConfigurer() {
             
              @Override
              public void addFormatters(FormatterRegistry registry) {
                  registry.addConverter(new Converter<String, Pet>() {
                      @Override
                      public Pet convert(String source) {
                          // 猫猫,3
                          if (StringUtils.hasText(source)) {
                              Pet pet = new Pet();
                              String[] split = source.split(",");
                              pet.setName(split[0]);
                              pet.setAge(Integer.parseInt(split[1]));
                              return pet;
                          }
                          return null;
                      }
                  });
              }
          };
      }
  ```

  

#### 2.POJO封装过程

- **ServletModelAttributeMethodProcessor**



#### 3.参数处理原理

- HandlerMapping中找到能处理请求的Handler(Controller.method())
- 为当前Handler 找一个适配器 HandlerAdapter； **RequestMappingHandlerAdapter**
- 适配器执行目标方法并确定方法参数的每一个值

- 1.HandlerAdapter
  - 支持方法上标注@RequestMapping
  - 支持函数式编程的
- 2.执行目标方法
- 3.参数解析器：不同注解对应不同的解析器
  - 解析器是否支持解析
  - 执行解析
- 4.返回值处理器：
- 5.确定目标方法每一个参数的值
  - 遍历所有参数解析器查看是否支持

#### 4.数据响应与内容协商

![数据响应与内容协商1](.\springboot_Markdown笔记图片\数据响应与内容协商1.png)

- 返回值解析器：解析各类返回参数



##### 1.响应JSON

- jackson.jar+@ResponseBody

```java
@Controller
public class ResponseControllerTest {
    @GetMapping("/test/person")
    @ResponseBody
    public User getUser() {
        User user = new User("zyp", 18, null);
        return user;
    }
}
// 给前端返回Json数据
```

- 1.返回值解析器

- 2.返回值解析器原理

  - 1.返回值处理器判断是否支持这种类型返回值 supportsReturnType
  - 2.返回值处理器调用 handleReturnValue 进行处理
  - 3.RequestResponseBodyMethodProcessor 可以处理返回值标了@ResponseBody 注解的。

  - - 利用 MessageConverters 进行处理 将数据写为json

  - - - 1.内容协商（浏览器默认会以请求头的方式告诉服务器他能接受什么样的内容类型）
      - 2.服务器最终根据自己的能力，决定服务器能生产出什么样内容类型的数据
      - 3.SpringMVC会挨个遍历所有容器底层的 HttpMessageConverter ，看谁能处理？

  - - - - 1.得到MappingJackson2HttpMessageConverter可以将对象写为json
        - 2.利用MappingJackson2HttpMessageConverter将对象转为json再写出去。

- SpringMVC到底支持哪些返回值

1. ModelAndView
2. Model
3. View
4. ResponseEntity 
5. ResponseBodyEmitter
6. StreamingResponseBody
7. HttpEntity
8. HttpHeaders
9. Callable
10. DeferredResult
11. ListenableFuture
12. CompletionStage
13. WebAsyncTask
    有 @ModelAttribute 且为对象类型的
    @ResponseBody 注解 ---> RequestResponseBodyMethodProcessor；

- HTTPMessageConverter原理

  - 默认的MessageConverter

    <img src=".\springboot_Markdown笔记图片\MessageConverter1.png" alt="MessageConverter1" style="zoom:50%;" />

  - 0 - 只支持Byte[]类型的

    1 - String

    2 - String

    3 - Resource

    4 - ResourceRegion

    5 - DOMSource.**class \** SAXSource.**class**) \ StAXSource.**class \**StreamSource.**class \**Source.**class**

    **6 -** MultiValueMap

    7 - 直接返回**true** 

    **8 - 直接返回true**

    **9 - 支持注解方式xml处理的。**

- 最终 MappingJackson2HttpMessageConverter  把对象转为JSON（利用底层的jackson的objectMapper转换的）

##### 2.内容协商

- 根据客户端接收能力不同，返回不同媒体类型的数据。

- 两种响应方式：accpet响应头/format=xxx请求参数

- 引入依赖

```xml
<dependency>
    <groupId>com.fasterxml.jackson.dataformat</groupId>
    <artifactId>jackson-dataformat-xml</artifactId>
</dependency>
```

- postman分别测试返回json和xml

  - 只需要改变请求头中Accept字段。Http协议中规定的，告诉服务器本客户端可以接收的数据类型。
    - accept/xml
    - accept/json

- 开启浏览器参数方式内容协商功能(基于参数的内容协商)

  - 开启内容协商模式

  ```yaml
  spring:
    mvc:
      contentnegotiation:
        favor-parameter: true
  ```

  - [localhost:8080/test/person?format=json](http://localhost:8080/test/person?format=json)
  - [localhost:8080/test/person?format=xml](http://localhost:8080/test/person?format=xml)

- 内容协商原理

  1. 判断当前响应头中是否已经有确定的媒体类型。MediaType
  2. 获取客户端(PostMan、浏览器)支持接收的内容类型。(获取客户端Accepte请求头字段)【application/xml】
     - contentNegotiationManager 内容协商管理器 默认使用基于请求头的策略
  3. 遍历循环所有当前系统的MessageConverter，看谁支持操作这个对象(Person)
  4. 找到支持操作Person的converter，把converter支持的媒体类型统计出来。
  5. 客户端需要【application/xml】。服务端能力【10种、json、xml】
  6. 内容协商的最佳匹配
  7. 返回最终结果：最佳结果

- 自定义MessageConverter

  - 所有MessageConverter合起来可以支持各种媒体类型数据的操作(读、写)

  - 实现多协议数据兼容。json、xml、x-guigu

  - 0.@ResponseBody 响应数据出去调用 RequestResponseBodyiethodProcessor 处理

  - 1.Processor处理方法返回值。通过MessageConverter处理

  - 2.所有MessageConverter合起来可以支持各种媒体类型数据的操作(读、写)

  - 3.内容协商找到最终的 messageConverter;

  - 自定义场景案例

    - 自定义Converter

    ```java
    package com.uestc.boot.converter;
    
    import com.uestc.boot.Bean.User;
    import org.springframework.http.HttpInputMessage;
    import org.springframework.http.HttpOutputMessage;
    import org.springframework.http.MediaType;
    import org.springframework.http.converter.HttpMessageConverter;
    import org.springframework.http.converter.HttpMessageNotReadableException;
    import org.springframework.http.converter.HttpMessageNotWritableException;
    
    import java.io.IOException;
    import java.io.OutputStream;
    import java.util.List;
    
    /**
     * 自定义Converter 处理Person类型的数据
     */
    public class UestcConverter implements HttpMessageConverter<User> {
        @Override
        public boolean canRead(Class<?> clazz, MediaType mediaType) {
            return false;
        }
        @Override
        public boolean canWrite(Class<?> clazz, MediaType mediaType) {
            return clazz.isAssignableFrom(User.class);
        }
        /*
        设置自定义类型
         */
        @Override
        public List<MediaType> getSupportedMediaTypes() {
            // 响应accpet请求头
            return MediaType.parseMediaTypes("application/x-uestc");
        }
        @Override
        public User read(Class<? extends User> clazz, HttpInputMessage inputMessage) throws IOException, HttpMessageNotReadableException {
            return null;
        }
        @Override
        public void write(User user, MediaType contentType, HttpOutputMessage outputMessage) throws IOException, HttpMessageNotWritableException {
            // 自定义协议数据写出
            String data = user.getName() + ";" + user.getAge() + ";" + user.getPet();
            // 传出
            OutputStream body = outputMessage.getBody();
            body.write(data.getBytes());
        }
    }
    ```

    - 添加Converter：WebConfig配置类中添加

    ```java
    @Configuration(proxyBeanMethods = false)
    public class WebConfig /*implements WebMvcConfigurer*/ {
        @Bean
        public WebMvcConfigurer webMvcConfigurer() {
            return new WebMvcConfigurer() {
                /*
                自定义内容协商策略
                 */
                @Override
                public void configureContentNegotiation(ContentNegotiationConfigurer configurer) {
                    Map<String, MediaType> mediaTypeMap = new HashMap<>();
                    mediaTypeMap.put("json", MediaType.APPLICATION_JSON);
                    mediaTypeMap.put("xml", MediaType.APPLICATION_XML);
                    mediaTypeMap.put("x-uestc", MediaType.parseMediaType("application/x-uestc"));
                    // 指定支持的媒体类型
                    // 基于参数
                    ParameterContentNegotiationStrategy parameterStrategy = new ParameterContentNegotiationStrategy(mediaTypeMap);
                    // 基于请求头
                    HeaderContentNegotiationStrategy headerStrategy = new HeaderContentNegotiationStrategy();
                    configurer.strategies(Arrays.asList(parameterStrategy, headerStrategy));
                }
                /*
                自定义Converter
                 */
                @Override
                public void extendMessageConverters(List<HttpMessageConverter<?>> converters) {
                    converters.add(new UestcConverter());
                }
                ...
    ```

#### 5.视图解栟与模板引擎

- 视图解析:SpringBoot默认(SpringBoot默认打包方式是Jar包，JSP不支持在jar包内解析)不支持JSP，需要引入第三方模板引擎技术实现页面渲染。

##### 1.thymeleaf:类似jsp页面

- thymeleaf基本介绍：现代化/简洁/服务端模板(性能比较弱)

###### 基本语法

1. 表达式

| 表达式名字 | 语法 | 用途                           |
| ---------- | ---- | ------------------------------ |
| 变量取值   | ${}  | 获取请求域、session域、对象等  |
| 选择变量   | *{}  | 获取上下文对象值               |
| 消息       | #{}  | 获取国际化等值                 |
| 链接       | @{}  | 生成链接                       |
| 片段表达式 | ~{}  | jsp:include 作用，引入公共页面 |

2. 字面量

   - 文本值:'one text','Another one!'.…
   - 数字:0.34，3.0，12.3
   - 布尔值: true，false
   - 空值: null
   - 变量:one，two，…变量不能有空格

3. 文本操作

   - 字符串拼接:+
   - 变量替换:|The name is ${name}|

4. 运算符 + - * / %

5. 布尔运算

   运算符:and，or
   一元运算:!，not

6. 比较运算

   - 比较:>,<= ,<=( gt ,lt,ge ,le )
   - 等式:==,!=(eq ,ne)

7. if-then: (if)? (then)
   if-then-else:(if)?(then):(else)
   Default: (value)?: (defaultvalue)

8. 设置属性值-th:attr

```html
<input type="submit" value="Subscribe" th:attr="value=#{subscribe.submit}" /> 
```

###### 使用演示

- 配置stater

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```

- thymeleaf自动配置
  1. 所有thymeleaf的配置值都在 ThymeleafProperties
  2. 配置SpringTemplateEngine
  3. 配置ThymeleafViewResolver
  4. 只需要直接开发页面

```java
@Configuration(
    proxyBeanMethods = false
)
@EnableConfigurationProperties({ThymeleafProperties.class})
@ConditionalOnClass({TemplateMode.class, SpringTemplateEngine.class})
@AutoConfigureAfter({WebMvcAutoConfiguration.class, WebFluxAutoConfiguration.class})
@Import({TemplateEngineConfigurations.ReactiveTemplateEngineConfiguration.class, TemplateEngineConfigurations.DefaultTemplateEngineConfiguration.class})
public class ThymeleafAutoConfiguration {
    ...
```

```java
public static final String DEFAULT_PREFIX ="classpath:/templates/";
public static final String DEFAULT_SUFFIX=".html";//xxx.html
```

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<h1 th:text="${msg}">成功</h1>
<a th:href="${link}">去百度1</a>
<!--@{link}把字符当作访问路径-->
<a th:href="@{link}">去百度2</a>
</body>
</html>
```

```java
@Controller
public class ViewTestController {
    @GetMapping("/uestc")
    public String uestcIdx(Model model) {
        model.addAttribute("msg", "uestc");
        model.addAttribute("link", "http://www.baidu.com");
        return "success";
    }
}
```

###### 后台管理系统

1. 构建spring initail 依赖

```
Spring Boot DevTools
Lombok
Spring Configuration Processor
Spring Web
Thymeleaf
```

2. 使用thymeleaf抽取公共页面

   - 方法2

   ```html
   <div id="commonscript">
       公共内容
   </div>
   ```

   ```html
   <div th:replace="common ::#commonscript"></div>
   ```

   

   - 方法1

```html
<footer th:fragment="copy">
	&copy; 2011 The Good Thymes Virtual Grocery
</footer>
```

```html
<body>
    footer是页面名称
<div th:insert="footer :: copy"></div>
<div th:replace="footer :: copy"></div>
<div th:include="footer :: copy"></div>
</body>
```

```html
显示效果
<body>
    <div>
        <footer>
            &copy; 2011 The Good Thymes Virtual Grocery
        </footer>
    </div>
    <footer>
        &copy; 2011 The Good Thymes Virtual Grocery
    </footer>
    <div>
        &copy; 2011 The Good Thymes Virtual Grocery
    </div>
</body>
```

###### 视图解析原理流程

1. 视图解析原理流程

   1、目标方法处理的过程中，所有数据都会被放在 **ModelAndViewContainer 里面。包括数据和视图地址**

   **2、方法的参数是一个自定义类型对象（从请求参数中确定的），把他重新放在** **ModelAndViewContainer** 

   **3、任何目标方法执行完成以后都会返回 ModelAndView（****数据和视图地址****）。**

   **4、****processDispatchResult  处理派发结果（页面改如何响应）**

   - 1、**render**(**mv**, request, response); 进行页面渲染逻辑

   - - 1、根据方法的String返回值得到 **View** 对象【定义了页面的渲染逻辑】

   - - - 1、所有的视图解析器尝试是否能根据当前返回值得到**View**对象
       - 2、得到了  **redirect:/main.html** --> Thymeleaf new **RedirectView**()
       - 3、ContentNegotiationViewResolver 里面包含了下面所有的视图解析器，内部还是利用下面所有视图解析器得到视图对象。
       - 4、view.render(mv.getModelInternal(), request, response);   视图对象调用自定义的render进行页面渲染工作

   - - - - **RedirectView 如何渲染【重定向到一个页面】**
         - **1、获取目标url地址**
         - **2、****response.sendRedirect(encodedURL);**

   

   **视图解析：**

   - - **返回值以 forward: 开始： new InternalResourceView(forwardUrl); -->  转发****request.getRequestDispatcher(path).forward(request, response);** 
     - **返回值以** **redirect: 开始：** **new RedirectView() --》 render就是重定向** 
     - **返回值是普通字符串： new ThymeleafView（）--->** 

#### 6.拦截器

- 实现登录拦截

```java
package com.uestc.admin.config;

import com.uestc.admin.interceptor.LoginInterceptor;
import org.springframework.web.servlet.config.annotation.InterceptorRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

public class AdminWebConfig implements WebMvcConfigurer {
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new LoginInterceptor())
                .addPathPatterns("/**") // 拦截所有资源包库静态资源
                .excludePathPatterns("/", "/login", "/login", "/css/*", "/fonts/**", "/js/**");
    }
}
```

```java
package com.uestc.admin.interceptor;

import org.springframework.web.servlet.HandlerInterceptor;
import org.springframework.web.servlet.ModelAndView;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

public class LoginInterceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        // 登录检测
        HttpSession session = request.getSession();
        Object user = session.getAttribute("loginUser");
        if (user != null) return true;
        // 拦截
        session.setAttribute("msg", "请先登录");
        response.sendRedirect("/");
        return false;
    }

    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        HandlerInterceptor.super.postHandle(request, response, handler, modelAndView);
    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        HandlerInterceptor.super.afterCompletion(request, response, handler, ex);
    }
}
```

- 拦截器原理

1、根据当前请求，找到**HandlerExecutionChain【**可以处理请求的handler以及handler的所有 拦截器】

2、先来**顺序执行** 所有拦截器的 preHandle方法

- 1、如果当前拦截器prehandler返回为true。则执行下一个拦截器的preHandle
- 2、如果当前拦截器返回为false。直接    倒序执行所有已经执行了的拦截器的  afterCompletion；

**3、如果任何一个拦截器返回false。直接跳出不执行目标方法**

**4、所有拦截器都返回True。执行目标方法**

**5、倒序执行所有拦截器的postHandle方法。**

**6、前面的步骤有任何异常都会直接倒序触发** afterCompletion

7、页面成功渲染完成以后，也会倒序触发 afterCompletion

#### 7.文件上传

- 修改spring.servlet.multipart的参数可以修改文件上传的大小/数量等配置

```properties
spring.servlet.multipart.max-file-size=10MB
spring.servlet.multipart.max-request-size=100MB
```

- 上传

```java
@Controller
@Slf4j
public class FormTestController {
    @GetMapping("/form_layouts")
    public String from_layouts() {
        return "form/form_layouts.html";
    }
    @PostMapping("upload")
    public String upload(@RequestParam("email") String email,
                         @RequestParam("username") String username,
                         @RequestPart("headerImg") MultipartFile headerImg,
                         @RequestPart("photos") MultipartFile[] photos) throws IOException {
        log.info("上传的信息：email={}, username={}, headerImg={}, photos={}",email, username, headerImg.getSize(), photos.length);
        if (!headerImg.isEmpty()) {
            String filename = headerImg.getOriginalFilename();
            headerImg.transferTo(new File("C:\\test\\" + filename));
        }
        for (MultipartFile photo : photos) {
            if (!photo.isEmpty()) {
                String filename = photo.getOriginalFilename();
                photo.transferTo(new File("C:\\test\\" + filename));
            }
        }
        return "main";
    }
}
```

- 自动配置原理
  - **文件上传自动配置类-MultipartAutoConfiguration-****MultipartProperties
  - **自动配置好了 **StandardServletMultipartResolver   【文件上传解析器】
  - 原理步骤
  - 1、请求进来使用文件上传解析器判断（**isMultipart**）并封装（**resolveMultipart，**返回**MultipartHttpServletRequest**）文件上传请求**
  
  - **2、参数解析器来解析请求中的文件内容封装成MultipartFile**
  - **3、将request中文件信息封装为一个Map；**MultiValueMap<String, MultipartFile>FileCopyUtils**。实现文件流的拷贝

#### 8.异常处理

- 1.默认规则

  - 默认情况下，Spring Boot提供`/error`处理所有错误的映射
  - 对于机器客户端，它将生成JSON响应，其中包含错误，HTTP状态和异常消息的详细信息。对于浏览器客户端，响应一个“ whitelabel”错误视图，以HTML格式呈现相同的数据
  
- 2.定制错误处理逻辑

  - 自定义错误页
  - - error/404.html   error/5xx.html；有精确的错误状态码页面就匹配精确，没有就找 4xx.html；如果都没有就触发白页
  - @ControllerAdvice+@ExceptionHandler处理全局异常；底层是 **ExceptionHandlerExceptionResolver 支持的**
  - @ResponseStatus+自定义异常 ；底层是 **ResponseStatusExceptionResolver ，把responsestatus注解的信息底层调用** **response.sendError(statusCode, resolvedReason)；tomcat发送的/error**
  - Spring底层的异常，如 参数类型转换异常；**DefaultHandlerExceptionResolver 处理框架底层的异常。**
  - response.sendError(HttpServletResponse.**SC_BAD_REQUEST**, ex.getMessage()); 
  - 自定义实现 HandlerExceptionResolver 处理异常；可以作为默认的全局异常处理规则(指定优先级)
  - **ErrorViewResolver**  实现自定义处理异常；
    - response.sendError 。error请求就会转给controller
    - 你的异常没有任何方法能处理。tomcat底层 response.sendError。error请求就会转给controller
    - **basicErrorController**(最底层的异常处理) 要去的页面地址是 ErrorViewResolver ；
  
- 3.异常处理自动配置原理

- **errorMvcAutoConfiguration  自动配置异常处理规则**
  
  - **容器中的组件：类型：DefaultErrorAttributes ->** **id：errorAttributes**
    - **public class** **DefaultErrorAttributes** **implements** **ErrorAttributes**, **HandlerExceptionResolver**
    - **DefaultErrorAttributes**：定义错误页面中可以包含哪些数据。
  - **容器中的组件：类型：****BasicErrorController --> id：basicErrorController（json/白页 适配响应）**
    - **处理默认** **/error 路径的请求；页面响应** **new** ModelAndView(**"error"**, model)；
    - **容器中有组件 View**->**id是error**；（响应默认错误页）
    - 容器中放组件 **BeanNameViewResolver（视图解析器）；按照返回的视图名作为组件的id去容器中找View对象。**
  - **容器中的组件：**类型：**DefaultErrorViewResolver -> id：**conventionErrorViewResolver
    - 如果发生错误，会以HTTP的状态码 作为视图页地址（viewName），找到真正的页面
    - error/404、5xx.html
  
  
    - 如果想要返回页面；就会找error视图【**StaticView**】。(默认是一个白页)

- 4.异常处理步骤流程

  - 1.执行目标方法，目标方法运行期间有任何异常都会被catch、而且标志当前请求结束；并且用 **dispatchException** 

  - 2.进入视图解析流程（页面渲染？） 

    processDispatchResult(processedRequest, response, mappedHandler, **mv**, **dispatchException**);

  - 3.**mv** = **processHandlerException**；处理handler发生的异常，处理完成返回ModelAndView；

    - 1、遍历所有的 **handlerExceptionResolvers，看谁能处理当前异常【****HandlerExceptionResolver处理器异常解析器】

    - 2、系统**默认的异常解析器**；
      - 1、DefaultErrorAttributes先来处理异常。把异常信息保存到rrequest域，并且返回null；
      
      - **2、默认没有任何人能处理异常，所以异常会被抛出**
      
        - a.如果没有任何人能处理最终底层就会发送 /error 请求。会被底层的BasicErrorController处理
        - b.解析错误视图；遍历所有的ErrorViewResolver  看谁能解析。
        - c.**默认的** **DefaultErrorViewResolver ,作用是把响应状态码作为错误页的地址，error/500.html** 
        - d.模板引擎最终响应这个页面** **error/500.html** 

- 自定义异常处理controller

```java
package com.uestc.admin.exception;

import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;

@ControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler({ArithmeticException.class, NullPointerException.class})
    public String handleArithmeticException() {
        return "login"; // 视图地址
    }
}
```

- 自定义异常

```java
@ResponseStatus(value= HttpStatus.FORBIDDEN,reason = "用户数量太多")
public class UserTooManyException extends RuntimeException {

    public  UserTooManyException(){

    }
    public  UserTooManyException(String message){
        super(message);
    }
}
```

- 自定义异常解析器

```java
package com.uestc.admin.exception;

import org.springframework.core.Ordered;
import org.springframework.core.annotation.Order;
import org.springframework.stereotype.Component;
import org.springframework.web.servlet.HandlerExceptionResolver;
import org.springframework.web.servlet.ModelAndView;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@Order(value= Ordered.HIGHEST_PRECEDENCE)  //指定优先级，数字越小优先级越高
@Component
public class CustomerHandlerExceptionResolver implements HandlerExceptionResolver {
    @Override
    public ModelAndView resolveException(HttpServletRequest request,
                                         HttpServletResponse response,
                                         Object handler, Exception ex) {

        try {
            response.sendError(511,"我喜欢的错误");
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
        return new ModelAndView();
    }
}
```

#### 9.Web原生组伴注入

- Web原生组伴注入(Servlet、Filter、Listener)

##### 1.使用Servlet API

- @ServletComponentScan(basePackages = **"com.atguigu.admin"**) :指定原生Servlet组件都放在那里
- @WebServlet(urlPatterns = **"/my"**)：效果：直接响应，**没有经过Spring的拦截器？**
- @WebFilter(urlPatterns={**"/css/\*"**,**"/images/\*"**})
- @WebListener
- 推荐可以这种方式；

```java
@ServletComponentScan(basePackages = "com.uestc") // 扫描范围
@SpringBootApplication
public class Boot05WebAdminApplication {

    public static void main(String[] args) {
        SpringApplication.run(Boot05WebAdminApplication.class, args);
    }

}
```

```java
@WebServlet("/my")
public class MyServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.getWriter().write("66666");
    }
}
```

```java
@Slf4j
@WebFilter({"/css/*", "/images/*"})
public class MyFilter implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        log.info("MyFilter");
    }
    @Override
    public void destroy() {
        log.info("destroy");
    }
    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        log.info("doFilter");
        filterChain.doFilter(servletRequest, servletResponse);
    }
}
```

```java
@Slf4j
@WebListener
public class MyServletContextListener implements ServletContextListener {
    @Override
    public void contextInitialized(ServletContextEvent sce) {
        log.info("MyServletContextListener初始化");
    }
    @Override
    public void contextDestroyed(ServletContextEvent sce) {
        log.info("MyServletContextListener销毁");
    }
}
```

##### 2.使用RegistrationBean

- 同一种filter只能对应一个FilterRegistrationBean
- 扩展：DispatchServlet 如何注册进来
  - 容器中自动配置了  DispatcherServlet  属性绑定到 WebMvcProperties；对应的配置文件配置项是 **spring.mvc。**
  - **通过** **ServletRegistrationBean**<DispatcherServlet> 把 DispatcherServlet  配置进来。
  - 默认映射的是 / 路径。(可以修改配置参数)
- Tomcat-Servlet:多个Servlet都能处理到同一层路径，精确优选原则
  - A： /my/
  - B： /my/1

```java
@Configuration(proxyBeanMethods = true) // true(默认) 保证单实例
public class MyRegisterConfig {
    @Bean
    public ServletRegistrationBean myServlet() {
        MyServlet servlet = new MyServlet();
        return new ServletRegistrationBean<>(servlet, "/my02");
    }
    @Bean
    public FilterRegistrationBean myFilter() {
        MyFilter filter = new MyFilter();
        return new FilterRegistrationBean<>(filter, myServlet());
    }
    @Bean
    public FilterRegistrationBean myFilter2() {
        MyFilter filter = new MyFilter();
        FilterRegistrationBean<MyFilter> registrationBean = new FilterRegistrationBean<>(filter);
        registrationBean.setUrlPatterns(Arrays.asList("/my", "/css/*"));
        System.out.println("filter2");
        return registrationBean;
    }
    @Bean
    public ServletListenerRegistrationBean myListener() {
        MyServletContextListener listener = new MyServletContextListener();
        return new ServletListenerRegistrationBean<>(listener);
    }
}
```

#### 10.嵌入式Servlet容器(Web服务器)

##### 1.切换嵌入式Servlet容器

- 默认支持的webServer

- - `Tomcat`, `Jetty`, or `Undertow`
  - `ServletWebServerApplicationContext 容器启动寻找ServletWebServerFactory 并引导创建服务器`

- 切换服务器

  - 默认Tomcat

  - 修改starter的配置，排除tomcat的依赖，引入其他服务器的依赖如underTo

- 原理

  - SpringBoot应用启动发现当前是Web应用。web场景包-导入tomcat

- - web应用会创建一个web版的ioc容器 ServletWebServerApplicationContext

- - ServletWebServerApplicationContext启动的时候寻找 **ServletWebServerFactory**（Servlet 的web服务器工厂---> Servlet 的web服务器）
  - SpringBoot底层默认有很多的WebServer工厂；TomcatServletWebServerFactory, JettyServletWebServerFactory or UndertowServletWebServerFactory
  - 底层直接会有一个自动配置类。ServletWebServerFactoryAutoConfiguration
  - ServletWebServerFactoryAutoConfiguration导入了ServletWebServerFactoryConfiguration（配置类）
  - ServletWebServerFactoryConfiguration 配置类 根据动态判断系统中到底导入了那个Web服务器的包。（默认是web-starter导入tomcat包），容器中就有 TomcatServletWebServerFactory
  - TomcatServletWebServerFactory 创建出Tomcat服务器并启动；TomcatWebServer 的构造器拥有初始化方法initialize---this.tomcat.start();
  - **内嵌服务器就是手动把启动服务器的代码调用**（tomcat核心jar包存在）

##### 2.定制Servlet容器

- 定制方法1：实现  **WebServerFactoryCustomizer< ConfigurableServletWebServerFactory > **

- - 把配置文件的值和**ServletWebServerFactory 进行绑定**
  - **xxxxxCustomizer**：定制化器，可以改变xxxx的默认规则**

- 定制方法2：修改配置文件 **server.xxx**
  - 推荐修改配置文件
- 定制方法3：直接自定义 **ConfigurableServletWebServerFactory** 

#### 11.定制化原理

##### 1.定制化的常见方式

- 1.修改配置文件:**xxxxxCustomizer；**
- 2.常用方法:**编写自定义的配置类   xxxConfiguration；+** **@Bean替换、增加容器中默认组件；视图解析器** 
  - **Web应用 编写一个配置类实现** **WebMvcConfigurer 即可定制化web功能；+ @Bean给容器中再扩展一些组件**
- 3.底层定制：@EnableWebMvc + WebMvcConfigurer —— @Bean  可以全面接管SpringMVC，所有规则全部自己重新配置； 实现定制和扩展功能

- - 原理
  - 1、WebMvcAutoConfiguration  默认的SpringMVC的自动配置功能类。静态资源、欢迎页.....
  - 2、一旦使用 @EnableWebMvc 、。会 @Import(DelegatingWebMvcConfiguration.**class**)
  - 3、**DelegatingWebMvcConfiguration** 的 作用，只保证SpringMVC最基本的使用

- - - 把所有系统中的 WebMvcConfigurer 拿过来。所有功能的定制都是这些 WebMvcConfigurer  合起来一起生效
    - 自动配置了一些非常底层的组件。**RequestMappingHandlerMapping**、这些组件依赖的组件都是从容器中获取
    - **public class** DelegatingWebMvcConfiguration **extends** **WebMvcConfigurationSupport**

- - 4、**WebMvcAutoConfiguration** 里面的配置要能生效 必须  @ConditionalOnMissingBean(**WebMvcConfigurationSupport**.**class**)
  - 5、@EnableWebMvc  导致了 **WebMvcAutoConfiguration  没有生效。**

- 

##### 2.原理分析套路

- **场景starter** **- xxxxAutoConfiguration - 导入xxx组件 - 绑定xxxProperties --** **绑定配置文件项** 

## 3.数据访问

### 3.1.SQL

#### 1.数据源的自动配置

- 导入JDBC场景

  - 官方配置没有导入数据库驱动：自己导入所需操作的数据库，springboot有默认的版本仲裁，但是需要匹配服务器安装的mysql版本。
  - 方法二

  ```xml
  <!--直接配置版本的参数-->
  <properties>
      <mysql.version>5.1.49</mysql.version>
  </properties>
  ```

  - 方法一

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jdbc</artifactId>
</dependency>
<!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <!--就近依赖版本，直接设置-->
    <version>5.1.49</version>
</dependency>
```

![JDBC依赖1](.\springboot_Markdown笔记图片\JDBC依赖1.png)

- 分析自动配置

  - DataSourceAutoConfiguration ： 数据源的自动配置
    - 修改数据源相关的配置：**spring.datasource**
    - 数据库连接池的配置，是自己容器中没有DataSource才自动配置的
    - **底层配置好的连接池是：**HikariDataSource**
  - DataSourceTransactionManagerAutoConfiguration： 事务管理器的自动配置
  - JdbcTemplateAutoConfiguration： **JdbcTemplate的自动配置，可以来对数据库进行crud**

  - - 可以修改这个配置项@ConfigurationProperties(prefix = **"spring.jdbc"**) 来修改JdbcTemplate
    - @Bean@Primary    JdbcTemplate；容器中有这个组件

  - JndiDataSourceAutoConfiguration： jndi的自动配置
  - XADataSourceAutoConfiguration： 分布式事务相关的

- 数据库连接配置:application.yaml

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:4306/mybatis?useSSL=false
    username: root
    password: z123456
    driver-class-name: com.mysql.jdbc.Driver
```

- 测试

```java
@SpringBootTest
class Boot05WebAdminApplicationTests {
    @Autowired
    JdbcTemplate jdbcTemplate;
    @Test
    void contextLoads() {
        Object o = jdbcTemplate.queryForObject("select count(*) from t_emp", Integer.class);
        System.out.println(o);
    }
}
```

#### 2.使用Druid数据源

- 官方文档：[首页 · alibaba/druid Wiki · GitHub](https://github.com/alibaba/druid/wiki/首页)

- 整合第三方技术的两种方式
  - 自定义
  - 找对应的starter

##### 自定义方式

1. 添加依赖

```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid</artifactId>
    <version>1.1.17</version>
</dependency>
```

- 查看基础配置:http://localhost:8080/druid

```java
package com.uestc.admin.config;

import com.alibaba.druid.pool.DruidDataSource;
import com.alibaba.druid.support.http.StatViewServlet;
import com.alibaba.druid.support.http.WebStatFilter;
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.boot.web.servlet.FilterRegistrationBean;
import org.springframework.boot.web.servlet.ServletRegistrationBean;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import javax.sql.DataSource;
import java.sql.SQLException;
import java.util.Arrays;

@Configuration
public class MyDataSourceConfig {
    // 默认的自动配置是判断容器中没有才会配@conditionalonMissingBean(DataSource.class)
    @Bean
    @ConfigurationProperties("spring.datasource") // 根据配置文件中的spring.datasource进行注入
    public DataSource dataSource() throws SQLException {
        DruidDataSource dataSource = new DruidDataSource();
        // 加入监控功能/防火墙
        dataSource.setFilters("stat, wall"); // 能使用getset配置的参数就可以使用配置文件配置
        return dataSource;
    }
    // 配置监控页面
    @Bean
    public ServletRegistrationBean statView() {
        StatViewServlet servlet = new StatViewServlet();
        ServletRegistrationBean<StatViewServlet> statViewServletServletRegistrationBean = new ServletRegistrationBean<>(servlet, "/druid/*");
        // 配置druid监控端的访问账号和密码
        statViewServletServletRegistrationBean.addInitParameter("loginUsername", "zyp005");
        statViewServletServletRegistrationBean.addInitParameter("loginPassword", "zyp005");
        return statViewServletServletRegistrationBean;
    }
    // WebstatFilter 用于采集web-jdbc关联监控的数据:
    @Bean
    public FilterRegistrationBean webStatFilter() {
        WebStatFilter webStatFilter = new WebStatFilter();
        FilterRegistrationBean<WebStatFilter> filterFilterRegistrationBean = new FilterRegistrationBean<>(webStatFilter);
        filterFilterRegistrationBean.setUrlPatterns(Arrays.asList("/*"));
        filterFilterRegistrationBean.addInitParameter("exclusions", "*.js,*.gif,*.jpg,*.png,*.css,*.ico,/druid/*");
        return filterFilterRegistrationBean;
    }
}
```

##### Starter方式

- 1.配置starter

```xml
<!-- https://mvnrepository.com/artifact/com.alibaba/druid-spring-boot-starter -->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid-spring-boot-starter</artifactId>
</dependency>
```

- 2.分析自动配置
  - 扩展配置项 **spring.datasource.druid**
  - DruidSpringAopConfiguration.**class**,   监控SpringBean的；配置项：**spring.datasource.druid.aop-patterns**
  - DruidStatViewServletConfiguration.**class**, 监控页的配置：**spring.datasource.druid.stat-view-servlet；默认开启**
  - DruidWebStatFilterConfiguration.**class**, web监控配置；**spring.datasource.druid.web-stat-filter；默认开启**
  - DruidFilterConfiguration.**class**}) 所有Druid自己filter的配置
- 3.配置参数

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:4306/mybatis?useSSL=false
    username: root
    password: z123456
    driver-class-name: com.mysql.jdbc.Driver
    druid:
      filter: # filter的配置
        stat:
          enabled: true
        wall:
          enabled: true
          config:
            drop-table-allow: false
      stat-view-servlet: # 配置监控功能
        enabled: true
        login-username: zyp005
        login-password: zyp005
        reset-enable: false

      web-stat-filter: # web功能
        enabled: true
        url-pattern: /*
        exclusions: '*.js,*.gif,*.jpg,*.png,*.css,*.ico,/druid/*'
      aop-patterns: com.uestc.admin # 监控springBean
```

#### 3.整合MyBatis操作

- 引入MyBatis的starter

```xml
<!-- https://mvnrepository.com/artifact/org.mybatis.spring.boot/mybatis-spring-boot-starter -->
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>2.1.4</version>
</dependency>
```

##### 1.配置模式

- 全局配置文件
- SqlSessionFactory: 自动配置好了
- SqlSession：自动配置了 **SqlSessionTemplate 组合了SqlSession**
- @Import(**AutoConfiguredMapperScannerRegistrar**.**class**);
- Mapper： 只要我们写的操作MyBatis的接口标准了 **@Mapper 就会被自动扫描进来**

- 使用方式
  - 导入mybatis官方starter
  - 编写mapper接口。标准@Mapper注解
  - 编写sql映射文件并绑定mapper接口
  - 在application.yaml中指定Mapper配置文件的位置，以及指定全局配置文件的信息 （建议；**配置在mybatis.configuration**）

```yaml
# application.yaml
# 配置mybatis的规则
mybatis:
#  config-location: classpath:mybatis/mybatis-config.xml # 配置文件
  # config-location 和 configuration 不能同时存在
  mapper-locations: classpath:mybatis/mapper/*.xml # 映射文件
  configuration: # 指定mybatis全局配置文件中的相关配置
    map-underscore-to-camel-case: true
```

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "https://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--配置Mapper接口-->
<mapper namespace="com.uestc.admin.Mapper.EmpMapperInter">
    <select id="getEmpById" resultType="com.uestc.admin.bean.Emp">
        select * from t-emp where id=#{id}
    </select>
</mapper>
```

```java
// mapper接口
@Mapper
public interface EmpMapperInter {
    public Emp getEmpById(Integer id);
}

```

##### 2.注解模式:不需要配置文件

```java
@Mapper
public interface UserMapper {
    @Select("select * from user where id=#{id}")
    public User getUserById(Integer id);
}
```

```java
@Service
public class UserService {
    @Autowired
    UserMapper userMapper;
    public User getUserById(Integer id) {
        return userMapper.getUserById(id);
    }
}
```

```java
@Controller
public class EmpMapperController {
    @Autowired
    UserService userService;
    @ResponseBody
    @GetMapping("/getUserById")
    public User getUserById(@RequestParam("id")Integer id) {
        User user = userService.getUserById(id);
        System.out.println(user);
        return user;
    }
}
```

- 注解实现复杂sql,可以使用@options

##### 3.混合模式：复杂的sql使用mapper.xml,简单的sql使用注解

- 实现方法：

- 引入mybatis-starter
- 配置application.yaml中，指定mapper-location位置即可
- 编写Mapper接口并标注@Mapper注解
- **简单方法**直接注解方式
- **复杂方法**编写mapper.xml进行绑定映射
- springboot配置类中使用**@MapperScan("com.atguigu.admin.mapper") 简化，其他的接口就可以不用标注@Mapper注解**

#### 4.整合MyBatisPlus

- 安装MyBatis开发插件：**MybatisX**
- 整合MyBatisPlus
  - 引入依赖

```xml
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatisplus-spring-boot-starter</artifactId>
    <version>1.0.5</version>
</dependency>
```

- 自动配置
  - MybatisPlusAutoConfiguration 配置类，MybatisPlusProperties 配置项绑定。**mybatis-plus：xxx 就是对****mybatis-plus的定制**
  - **SqlSessionFactory 自动配置好。底层是容器中默认的数据源**
  - **mapperLocations 自动配置好的。有默认值。****classpath\*:/mapper/\**/\*.xml；任意包的类路径下的所有mapper文件夹下任意路径下的所有xml都是sql映射文件。  建议以后sql映射文件，放在 mapper下**
  - **容器中也自动配置好了** **SqlSessionTemplate**
  - **@Mapper 标注的接口也会被自动扫描；建议直接** @MapperScan(**"com.atguigu.admin.mapper"**) 批量扫描就行
  - 使用@TableField(exist = false)标注Bean在Mysql中不存在字段/属性。优先查找与Bean同名的SQL表，如果名称不一致可以使用@TableName("user_tbl")注解Bean
  - **优点：**
    - 只需要我们的Mapper继承 **BaseMapper** 就可以拥有crud能力

- 分页功能

```java
// 配置分页拦截器
@Configuration
public class MyBatisConfig {
    @Bean
    public MybatisPlusInterceptor paginationInterceptor() {
        MybatisPlusInterceptor interceptor = new MybatisPlusInterceptor();
        PaginationInnerInterceptor innerInterceptor = new PaginationInnerInterceptor();
        innerInterceptor.setOverflow(true);
        innerInterceptor.setMaxLimit(500L);
        interceptor.addInnerInterceptor(innerInterceptor);
        return interceptor;
    }
}
```

- 删除修改/分页

```java
@Controller
public class TableController {
    @Autowired
    UserService userService;

    @GetMapping("/dynamic_table")
    public String dynamic_table(@RequestParam(value = "page", defaultValue = "1")Integer page, Model model) {
        List<User> list = userService.list();
        Page<User> userPage = new Page<>(page,4);
        Page<User> curPage = userService.page(userPage, null);
        model.addAttribute("page", curPage);
        return "table/dynamic_table";
    }
    @GetMapping("user/delete/{id}")
    public String deleteUser(@PathVariable("id")Integer id,
                             @RequestParam(value = "page", defaultValue = "1") Integer page,
                             RedirectAttributes ra) {
        userService.removeById(id);
        ra.addAttribute("page", page);
        return "redirect:/dynamic_table";
    }
}
```

- Mapper接口

```java
public interface UserMapperMBP extends BaseMapper<User> {
}
```

- service

```java
public interface UserService extends IService<User> {
}
```

- service实现类

```java
@Service
public class UserServiceImpl extends ServiceImpl<UserMapperMBP, User> implements UserService  {
    @Autowired
    UserMapperMBP userMapperMBP;
    public User getUserById(Integer id) {
        return userMapperMBP.selectById(id);
    }
}
```

### 3.2NoSQL



- 整合Redis

#### 1.配置stater

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

- 自动配置：
  - RedisAutoConfiguration 自动配置类。RedisProperties 属性类 --> **spring.redis.xxx是对redis的配置**
  - 连接工厂是准备好的。**Lettuce**ConnectionConfiguration、**Jedis**ConnectionConfiguration
  - **自动注入了RedisTemplate**<**Object**, **Object**> ： xxxTemplate；
  - **自动注入了StringRedisTemplate；k：v都是String**
  - **key：value**
  - **底层只要我们使用** **StringRedisTemplate、****RedisTemplate就可以操作redis**

- **redis环境搭建**

  1.阿里云按量付费redis。经典网络

  2.申请redis的公网连接地址

  3.修改白名单  允许0.0.0.0/0 访问

## 4.单元测试

### 1.Junit5

- 引入依赖

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

- SpringBoot整合Junit以后。
  - 编写测试方法：@Test标注（注意需要使用junit5版本的注解）
  - Junit类具有Spring的功能，@Autowired、比如 @Transactional 标注测试方法，测试完成后自动回滚

### 2.JUnit5常用注解

[JUnit 5 User Guide_官方文档](https://junit.org/junit5/docs/current/user-guide/#overview)

- **@Test :**表示方法是测试方法。但是与JUnit4的@Test不同，他的职责非常单一不能声明任何属性，拓展的测试将会由Jupiter提供额外测试
- **@ParameterizedTest :**表示方法是参数化测试，下方会有详细介绍
- **@RepeatedTest :**表示方法可重复执行，下方会有详细介绍
- **@DisplayName :**为测试类或者测试方法设置展示名称
- **@BeforeEach :**表示在每个单元测试之前执行
- **@AfterEach :**表示在每个单元测试之后执行
- **@BeforeAll :**表示在所有单元测试之前执行
- **@AfterAll :**表示在所有单元测试之后执行
- **@Tag :**表示单元测试类别，类似于JUnit4中的@Categories
- **@Disabled :**表示测试类或测试方法不执行，类似于JUnit4中的@Ignore
- **@Timeout :**表示测试方法运行如果超过了指定时间将会返回错误
- **@ExtendWith :**为测试类或测试方法提供扩展类引用

```java
//@TestInstance(TestInstance.Lifecycle.PER_CLASS)
@DisplayName("Junit5测试类")
@SpringBootTest // 获取springboot里面的容器
public class Junit5Test {
    @Autowired
    JdbcTemplate jdbcTemplate;
    @DisplayName("测试Displayname注解")
    @Test
    void testDisplay() {

        System.out.println();
    }
    @DisplayName("测试2方法")
    @Test
    @Disabled
    void testDisplay2() {
        System.out.println("2");
    }
    @DisplayName("测试3方法")
    @RepeatedTest(3)
    void testDisplay3() {
        System.out.println("3");
    }
    @BeforeEach
    void testBeforeEach() {
        System.out.println("测试要开始啦...");
    }
    @AfterEach
    void testAfterEach() {
        System.out.println("测试结束啦...");
    }
    @BeforeAll
    static void testBeforeAll() {
        System.out.println("所有测试要开始啦...");
    }
    @AfterAll
    static void testAfterAll() {
        System.out.println("所有测试要结束啦...");
    }
}
```

### 3.断言(assertions)

- 断言（assertions）是测试方法中的核心部分，用来对测试需要满足的条件进行验证。**这些断言方法都是 org.junit.jupiter.api.Assertions 的静态方法**。JUnit 5 内置的断言可以分成如下几个类别：
- **检查业务逻辑返回的数据是否合理。**
- *所有的测试运行结束以后，会有一个详细的测试报告；**

#### 1.简单断言

| 方法            | 说明                                 |
| --------------- | ------------------------------------ |
| assertEquals    | 判断两个对象或两个原始类型是否相等   |
| assertNotEquals | 判断两个对象或两个原始类型是否不相等 |
| assertSame      | 判断两个对象引用是否指向同一个对象   |
| assertNotSame   | 判断两个对象引用是否指向不同的对象   |
| assertTrue      | 判断给定的布尔值是否为 true          |
| assertFalse     | 判断给定的布尔值是否为 false         |
| assertNull      | 判断给定的对象引用是否为 null        |
| assertNotNull   | 判断给定的对象引用是否不为 null      |

```java
@DisplayName("测试简单断言")
    @Test
    void testSimpleAssertion() {
        // 前面的代码断言失败后面的代码不会执行
        // 数值相等
//        assertEquals(5, sum(2, 2));
//        assertEquals(5, sum(2, 2), "业务逻辑出错");
        // 相同对象
        String s1 = "abc";
        String s2 = "abc";
        String s3 = new String("abc");
        assertSame(s1, s2);
        assertSame(s1, s3);
    }
```

#### 2.数组断言

- 通过 assertArrayEquals 方法来判断两个对象或原始类型的数组是否相等

```java
@Test
    void testArray() {
        int[] arr1 = new int[2];
        arr1[0] = 1;
        arr1[1] = 2;
        int[] arr2 = new int[]{1, 2};
        int[] arr3 = {1, 2};
        int[] arr4 = {1, 2};
        assertArrayEquals(arr1, arr2); // 数组的内容是否相等
        assertSame(arr3, arr4);
    }
```

#### 3.组合断言

- assertAll 方法接受多个 org.junit.jupiter.api.Executable 函数式接口的实例作为要验证的断言，可以通过 lambda 表达式很容易的提供这些断言

```java
@Test
// 组合断言测试
void testAll() {
    int[] arr1 = new int[2];
    arr1[0] = 1;
    arr1[1] = 2;
    int[] arr2 = new int[]{1, 2};
    int[] arr3 = {1, 2};
    int[] arr4 = {1, 2};
    // 所有断言全部成功才执行后序代码
    assertAll("test",
              () -> assertArrayEquals(arr1, arr2),
              () -> assertSame(arr3, arr4)
             );
}
```

#### 4.异常断言

- 在JUnit4时期，想要测试方法的异常情况时，需要用**@Rule**注解的ExpectedException变量还是比较麻烦的。而JUnit5提供了一种新的断言方式**Assertions.assertThrows()** ,配合函数式编程就可以进行使用。

```java
@Test
void testException() {
    // 断定会出现异常 -> 出现异常则断言通过
    assertThrows(ArithmeticException.class, () -> {int i=10/0;});
}
```

#### 5.超时断言

- Junit5还提供了**Assertions.assertTimeout()** 为测试方法设置了超时时间

```java
@Test
@DisplayName("超时测试")
public void timeoutTest() {
    //如果测试方法时间超过1s将会异常
    Assertions.assertTimeout(Duration.ofMillis(1000), () -> Thread.sleep(500));
}
```

#### 6.快速失败

```java
@DisplayName("快速失败")
@Test
void testFastFail() {
    int i=1;
    if (i == 2) {
        fail("测试失败");
    }
}
int sum(int a, int b) {
    return a + b;
}
```

### 4.前置条件(assumptions)

- JUnit 5 中的前置条件（**assumptions【假设】**）类似于断言，不同之处在于**不满足的断言会使得测试方法失败**，而不满足的**前置条件只会使得测试方法的执行终止**。前置条件可以看成是测试方法执行的前提，当该前提不满足时，就没有继续执行的必要。

```java
public class AssumptionTest {
    private final String environment = "DEV";

    @Test
    @DisplayName("simple")
    public void simpleAssume() {
        assumeTrue(Objects.equals(this.environment, "DEV"));
        assumeFalse(() -> Objects.equals(this.environment, "PROD"));
    }

    @Test
    @DisplayName("assume then do")
    public void assumeThenDo() {
        assumingThat(
            Objects.equals(this.environment, "DEV"),
            () -> System.out.println("In DEV")
        );
    }

    @DisplayName("前置条件测试")
    @Test
    void testAssumption() {
        String str1 = "abc";
        Assumptions.assumeTrue(str1 instanceof String);
        System.out.println(str1);
    }
}
```

### 5.嵌套测试

- JUnit 5 可以通过 Java 中的内部类和@Nested 注解实现嵌套测试，从而可以更好的把相关的测试方法组织在一起。在内部类中可以使用@BeforeEach 和@AfterEach 注解，而且嵌套的层次没有限制。
- 外层可以驱动内层，内层不能驱动外层。

```java
package com.uestc.admin;

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Nested;
import org.junit.jupiter.api.Test;

import java.util.EmptyStackException;
import java.util.Stack;

import static org.junit.jupiter.api.Assertions.*;

@DisplayName("A stack")
class TestingAStackDemo {

    Stack<Object> stack;

    @Test
    @DisplayName("is instantiated with new Stack()")
    void isInstantiatedWithNew() {
        new Stack<>();
    }
    @BeforeEach
    void testBeforeOut() {
        System.out.println("在测试前Out");
    }

    @Nested
    @DisplayName("when new")
    class WhenNew {

        @BeforeEach
        void createNewStack() {
            stack = new Stack<>();
        }

        @Test
        @DisplayName("is empty")
        void isEmpty() {
            assertTrue(stack.isEmpty());
        }

        @Test
        @DisplayName("throws EmptyStackException when popped")
        void throwsExceptionWhenPopped() {
            assertThrows(EmptyStackException.class, stack::pop);
        }

        @Test
        @DisplayName("throws EmptyStackException when peeked")
        void throwsExceptionWhenPeeked() {
            assertThrows(EmptyStackException.class, stack::peek);
        }

        @Nested
        @DisplayName("after pushing an element")
        class AfterPushing {

            String anElement = "an element";

            @BeforeEach
            void pushAnElement() {
                stack.push(anElement);
            }

            @Test
            @DisplayName("it is no longer empty")
            void isNotEmpty() {
                assertFalse(stack.isEmpty());
            }

            @Test
            @DisplayName("returns the element when popped and is empty")
            void returnElementWhenPopped() {
                assertEquals(anElement, stack.pop());
                assertTrue(stack.isEmpty());
            }

            @Test
            @DisplayName("returns the element when peeked but remains not empty")
            void returnElementWhenPeeked() {
                assertEquals(anElement, stack.peek());
                assertFalse(stack.isEmpty());
            }
            @BeforeEach
            void testBefore() {
                System.out.println("在测试前In2");
            }
        }
    }
}
```

### 6.参数化测试

- 参数化测试是JUnit5很重要的一个新特性，使多次测试更加便利。

- 利用**@ValueSource**等注解，指定入参，我们将可以使用不同的参数进行多次单元测试，省去了很多冗余代码。
- @ValueSource: 为参数化测试指定入参来源，支持八大基础类以及String类型,Class类型
- **@NullSource**: 表示为参数化测试提供一个null的入参
- **@EnumSource**: 表示为参数化测试提供一个枚举入参
- **@CsvFileSource**：表示读取指定CSV文件内容作为参数化测试入参
- **@MethodSource**：表示读取指定方法的返回值作为参数化测试入参(注意方法返回需要是一个流)
- 注意：可以支持外部的各类入参。如:CSV,YML,JSON 文件甚至方法的返回值也可以作为入参。只需要去实现**ArgumentsProvider**接口，任何外部文件都可以作为它的入参。

```java
public class ParamTest {
    @ParameterizedTest
    @DisplayName("参数化测试")
    @ValueSource(ints = {1, 2, 3, 4, 45})
    void testParam(int i) {
        System.out.println(i);
    }

    @ParameterizedTest
    @DisplayName("参数化测试")
    @MethodSource("stringProvide") // 函数传参
    void testParamStr(String str) {
        System.out.println(str);
    }
    static Stream<String> stringProvide() {
        return Stream.of("apple", "banana", "uestc");
    }
}
```

## 5.指标监控

### 1.SpringBoot Actuator

- 简介：每一个微服务在云上部署以后，我们都需要对其进行监控、追踪、审计、控制等。SpringBoot就抽取了Actuator场景，使得我们每个微服务快速引用即可获得生产级别的应用监控、审计等功能。

#### 如何使用

- 引入依赖

```xml
<!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-actuator -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

- 测试
  - http://localhost:8080/actuator/beans
  - http://localhost:8080/actuator/configprops
  - http://localhost:8080/actuator/metrics
  - http://localhost:8080/actuator/metrics/jvm.gc.pause
  - [http://localhost:8080/actuator/endpointName/detailPath](http://localhost:8080/actuator/metrics)
- Http暴露：通过web访问

```yaml
# management 是所有actuator的配置
management:
  endpoints:
    enabled-by-default: true # 默认开启所有监控端点
    web:
      exposure:
        include: '*' # 以web方式暴露所有端点
```

### 2.Actuator Endpoint

#### 常用端点

| ID                 | 描述                                                         |
| ------------------ | ------------------------------------------------------------ |
| `auditevents`      | 暴露当前应用程序的审核事件信息。需要一个`AuditEventRepository组件`。 |
| `beans`            | 显示应用程序中所有Spring Bean的完整列表。                    |
| `caches`           | 暴露可用的缓存。                                             |
| `conditions`       | 显示自动配置的所有条件信息，包括匹配或不匹配的原因。         |
| `configprops`      | 显示所有`@ConfigurationProperties`。                         |
| `env`              | 暴露Spring的属性`ConfigurableEnvironment`                    |
| `flyway`           | 显示已应用的所有Flyway数据库迁移。 需要一个或多个`Flyway`组件。 |
| `health`           | 显示应用程序运行状况信息。                                   |
| `httptrace`        | 显示HTTP跟踪信息（默认情况下，最近100个HTTP请求-响应）。需要一个`HttpTraceRepository`组件。 |
| `info`             | 显示应用程序信息。                                           |
| `integrationgraph` | 显示Spring `integrationgraph` 。需要依赖`spring-integration-core`。 |
| `loggers`          | 显示和修改应用程序中日志的配置。                             |
| `liquibase`        | 显示已应用的所有Liquibase数据库迁移。需要一个或多个`Liquibase`组件。 |
| `metrics`          | 显示当前应用程序的“指标”信息。                               |
| `mappings`         | 显示所有`@RequestMapping`路径列表。                          |
| `scheduledtasks`   | 显示应用程序中的计划任务。                                   |
| `sessions`         | 允许从Spring Session支持的会话存储中检索和删除用户会话。需要使用Spring Session的基于Servlet的Web应用程序。 |
| `shutdown`         | 使应用程序正常关闭。默认禁用。                               |
| `startup`          | 显示由`ApplicationStartup`收集的启动步骤数据。需要使用`SpringApplication`进行配置`BufferingApplicationStartup`。 |
| `threaddump`       | 执行线程转储。                                               |

- 最常用的Endpoint
  - Health：监控状况
  - Metrics：运行时指标
  - Loggers：日志记录

```yaml
# management 是所有actuator的配置
management:
  endpoint:
    health:
      show-details: always # 显示详细信息
```

#### Health Endpoint

- 健康检查端点，我们一般用于在云平台，平台会定时的检查应用的健康状况，我们就需要Health Endpoint可以为平台返回当前应用的一系列组件健康状况的集合。

- 重要的几点：
  - health endpoint返回的结果，应该是一系列健康检查后的一个汇总报告
  - 很多的健康检查默认已经自动配置好了，比如：数据库、redis等
  - 可以很容易的添加自定义的健康检查机制

#### Metrics Endpoint



### 3.定制 Endpoint

#### 1.定制 Health 信息

```java
@Component
public class MyComHealthIndicator extends AbstractHealthIndicator {

    /**
     * 真实的检查方法
     * @param builder
     * @throws Exception
     */
    @Override
    protected void doHealthCheck(Health.Builder builder) throws Exception {
        //mongodb。  获取连接进行测试
        Map<String,Object> map = new HashMap<>();
        // 检查完成
        if(1 == 2){ // 设置判断条件
//            builder.up(); //健康
            builder.status(Status.UP);
            map.put("count",1);
            map.put("ms",100);
        }else {
//            builder.down();
            builder.status(Status.OUT_OF_SERVICE);
            map.put("err","连接超时");
            map.put("ms",3000);
        }

        builder.withDetail("code",100)
                .withDetails(map);
    }
}
```

<img src=".\springboot_Markdown笔记图片\Health信息.png" alt="Health信息" style="zoom:50%;" />

#### 2.定制info信息

- 方法1：配置文件配置信息

```yaml
# 开启配置文件的info支持
management:
  info:
    env:
      enabled: true
info:
  appName: boot-admin
  version: 2.0.1
  mavenProjectName: @project.artifactId@  #使用@@可以获取maven的pom文件值
  mavenProjectVersion: @project.version@
```

- 方法2：编写InfoContributor实现类

```java
@Component
public class AppInfoContributor implements InfoContributor {
    @Override
    public void contribute(Info.Builder builder) {
        builder.withDetail("msg", "你好")
                .withDetail("example",
                Collections.singletonMap("key", "value"));
    }
}
```



#### 3.定制Metrics信息(计数)

- SpringBoot支持自动适配的Metrics
- 增加定制Metrics

```java
class MyService{
    Counter counter;
    public MyService(MeterRegistry meterRegistry){
         counter = meterRegistry.counter("myservice.method.running.counter");
    }

    public void hello() {
        counter.increment();
    }
}


//也可以使用下面的方式
@Bean
MeterBinder queueSize(Queue queue) {
    return (registry) -> Gauge.builder("queueSize", queue::size).register(registry);
}
```



#### 4.定制 Endpoint

```java
@Component
@Endpoint(id = "container")
public class DockerEndpoint {


    @ReadOperation
    public Map getDockerInfo(){
        // 端点的读操作
        return Collections.singletonMap("info","docker started...");
    }

    @WriteOperation
    private void restartDocker(){
        System.out.println("docker restarted....");
    }
}
```

### 4.可视化

- github.com/codecentric/spring-boot-admin

## 6.原理解析

### 1.Profile功能

- 为了方便多环境适springboot简化了profile功能。

#### 1.application-profile功能

![profile-配置文件的选择](.\springboot_Markdown笔记图片\profile-配置文件的选择.png)

- 默认配置文件  application.yaml；任何时候都会加载
- 指定环境配置文件  application-{env}.yaml
- 激活指定环境

- - 配置文件激活
  - 命令行激活：java -jar xxx.jar --**spring.profiles.active=prod  --person.name=haha**

- - - **修改配置文件的任意值，命令行优先**

  - ```yaml
    spring.profiles.active=prod # 优先使用 application-prod.yaml
    ```

  - 

- 默认配置与环境配置同时生效
- 同名配置项，profile配置优先

#### 2.@Profile条件装配功能

```java
@Configuration(proxyBeanMethods = false)
@Profile("prod") // 指定配置文件
public class ProductionConfiguration {
    // ...
}
```

#### 3.profile分组

```yaml
spring.profiles.group.production[0]=proddb
spring.profiles.group.production[1]=prodmq

# 使用：--spring.profiles.active=production  激活
# 相当于把两个配置文件合并
```

### 2.外部化配置

https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-external-config

1. Default properties (specified by setting `SpringApplication.setDefaultProperties`).
2. `@PropertySource` annotations on your `@Configuration` classes. Please note that such property sources are not added to the `Environment` until the application context is being refreshed. This is too late to configure certain properties such as `logging.*` and `spring.main.*` which are read before refresh begins.
3. **Config data (such as** `**application.properties**` **files)**
4. A `RandomValuePropertySource` that has properties only in `random.*`.
5. OS environment variables.
6. Java System properties (`System.getProperties()`).
7. JNDI attributes from `java:comp/env`.
8. `ServletContext` init parameters.
9. `ServletConfig` init parameters.
10. Properties from `SPRING_APPLICATION_JSON` (inline JSON embedded in an environment variable or system property).
11. Command line arguments.
12. `properties` attribute on your tests. Available on `@SpringBootTest` and the [test annotations for testing a particular slice of your application](https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-testing-spring-boot-applications-testing-autoconfigured-tests).
13. `@TestPropertySource` annotations on your tests.
14. [Devtools global settings properties](https://docs.spring.io/spring-boot/docs/current/reference/html/using-spring-boot.html#using-boot-devtools-globalsettings) in the `$HOME/.config/spring-boot` directory when devtools is active.

- 优先规则：后面覆盖前面

#### 1.外部配置源

- 常用:Java属性文件、YAML文件、环境变量、命令行参数;

#### 2.配置文件查找位置

- (1) classpath 根路径

- (2) classpath 根路径下config目录

- (3) jar包当前目录 -- jar包的同一目录

- (4) jar包当前目录的config目录-- jar包的同一目录/config

- (5) /config子目录的直接子目录-- jar包的同一目录/config/xxx/application.yaml

- 优先规则：后面覆盖前面

#### 3.配置文件加载顺序

1. ​	当前jar包内部的application.properties和application.yml
2. 　当前jar包内部的application-{profile}.properties 和 application-{profile}.yml
3. 　引用的外部jar包的application.properties和application.yml
4. 　引用的外部jar包的application-{profile}.properties 和 application-{profile}.yml

- 优先规则：指定环境优先，外部优先，后面的可以覆盖前面的同名配置项

### 3.自定义starter

#### 1.starter启动原理

![stater原理](.\springboot_Markdown笔记图片\stater原理.png)

![stater原理2](.\springboot_Markdown笔记图片\stater原理2.png)

- autoconfigure包中配置使用 **META-INF/spring.factories** 中 **EnableAutoConfiguration** 的值，使得项目启动加载指定的自动配置类
- 编写自动配置类 xxxAutoConfiguration -> xxxxProperties

- - @Configuration
  - @Conditional
  - @EnableConfigurationProperties
  - @Bean
  - ......

引入starter --- xxxAutoConfiguration --- 容器中放入组件 ---- 绑定xxxProperties ---- 配置项

#### 2.自定义starter

- uestc-hello-spring-boot-starter（启动器）
- uestc-hello-spring-boot-starter-autoconfigure（自动配置包）

### 4.SpringBoot原理

#### SpringBoot启动过程

- 创建 SpringApplication

  - 保存一些信息。判定当前应用的类型。ClassUtils。Servlet。

  - bootstrappers：初始启动引导器（List< Bootstrapper >）：去spring.factories文件中找org.springframework.boot.Bootstrapper
  - 找 ApplicationContextInitializer：初始化器；去spring.factories找 ***ApplicationContextInitializer***
    - List<ApplicationContextInitializer<?>> initializers
  - 找 ApplicationListener ：应用监听器。去spring.factories找 ***ApplicationListener***
    - List<ApplicationListener<?>> listeners

- 运行 SpringApplication

  - StopWatch

  - 记录应用的启动时间
  - 创建引导上下文（Context环境）createBootstrapContext()
    - 获取到所有之前的 **bootstrappers** 依次执行 intitialize() 来完成对引导启动器上下文环境设
  - 让当前应用进入**headless**模式。java.awt.headless

  - 获取所有 RunListener（运行监听器）【为了方便所有Listener进行事件感知】
    - getSpringFactoriesInstances 去spring.factories找 **SpringApplicationRunListener**.
  - 遍历SpringApplicationRunListener 调用 starting 方法；
    - 相当于通知所有感兴趣系统正在启动的操作，项目正在 starting。
  - 保存命令行参数；ApplicationArguments

  - 准备环境 prepareEnvironment();
    - 返回或者创建基础环境信息对象。StandardServletEnvironment
    - 配置环境信息对象。
      - 读取所有的配置源的配置属性值。
    - 绑定环境信息
    - **监听器调用 listener.environmentPrepared()**；通知所有的监听器当前环境准备完成

- - 创建IOC容器(createApplicationContext())

- - - 根据项目类型(Servlet)创建容器，
    - 当前会创建 AnnotationConfigServletWebServerApplicationContext

- - 准备ApplicationContext IOC容器的基本信息prepareContext()

- - - 保存环境信息
    - IOC容器的后置处理流程。
    - 应用初始化器；applyInitializers；

- - - - 遍历所有的 ApplicationContextInitializer 。调用 initialize。来对ioc容器进行初始化扩展功能
      - 遍历所有的 listener 调用 contextPrepared。EventPublishRunListenr；通知所有的监听器contextPrepared

- - - 所有的**监听器调用contextLoaded**。通知所有的监听器contextLoaded；

- - **刷新IOC容器。**refreshContext

- - - 创建容器中的所有组件（Spring注解）

- - 容器刷新完成后工作？afterRefresh
  - 所有**监听器调用 listeners.started**(context); **通知所有的监听器** started
  - 调用所有runners；callRunners()

- - - 获取容器中的** **ApplicationRunner** 
    - 获取容器中的**CommandLineRunner**
    - 合并所有runner并且按照@Order进行排序
    - 遍历所有的runner。调用 run方法

- - **如果以上有异常，**

- - - 调用Listener 的 failed

- - 调用所有**监听器的 running 方法**  listeners.running(context); 通知所有的监听器running
  - running如果有问题。继续通知 failed 。调用所有 Listener 的failed；通知所有的监听器 failed

#### Application Events and Listeners

- https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-application-events-and-listeners

- **ApplicationContextInitializer**

- **ApplicationListener**

- **SpringApplicationRunListener**



#### ApplicationRunner 与 CommandLineRunner
