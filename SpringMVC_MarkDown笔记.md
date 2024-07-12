# 零.SpringMVC

![课程结构](.\SpringMVC_MarkDown笔记图片\课程结构.png)

# 一.SpringMVC简介

## 1.什么是MVC？

- MVC是一种软件架构的思想，将软件按照模型、视图、控制器来划分

1. M:Model，模型层，指工程中的JavaBean，作用是处理数据
   - JavaBean分为两类:
   - 一类称为实体类Bean:专门的数据存储业务，如Student、User等。
   - 一类称为业务处理Bean:指 Service 或 Dao 对象，专门用于处理业务逻辑和数据访问。
2. V:View，视图层，指工程中的html或jsp等页面，作用是与用户进行交互，展示数据
3. C:Controller，控制层，指工程中的servlet，作用是接收请求和响应浏览器
   - MVC的工作流程:
     用户通过视图层发送请求到服务器，在服务器中请求被Controler接收，Controller调用相应的Model层处理请求，处理完毕将结果返回到Controller，Controller再根据请求处理的结果找到相应的View视图，渲染数据后最终响应给浏览器

## 2.什么是SpringMVC

- SpringMVC 是 Spring,为表述层开发提供的一整套完备的解决方案。在表述层框架历经 Strust、WebWork、Strust2 等诸多产品的历代更迭之后，目前业界普遍选择了 SpringMVC 作为Java EE 项目表述层开发的首选方案。
- 注:三层架构分为表述层(或表示层)、业务逻辑层、数据访问层，表述层表示前台页面和后台servlet

## 3.SpringMVC的特点

- Spring 家族原生产品，与IOC容器等基础设施无缝对接
- 基于**原生的Servlet**，通过了功能强大的**前端控制器DispatcherServlet**，对请求和响应进行统一处理
- 表述层各细分领域需要解决的问题**全方位覆盖**，提供**全面解决方案**
- **代码清新简洁**，大幅度提升开发效率
- 内部组件化程度高，可插拔式组件**即插即用**，想要什么功能配置相应组件即可
- **性能卓著**，尤其适合现代大型、超大型互联网项目要求

# 二.案例演示：HelloWorld

## 1.开发环境

- 开发环境

1. IDE: idea 2023
2. 构建工具:maven3.5.4
3. 服务器:tomcat7
4. Spring版本:5.3.1

## 2.创建maven工程

1. a>添加web模块
2. b>打包方式:war
3. c>引入依赖

## 3.配置web.xml

- 注册SpringMVC的前端控制器DispatcherServlet

### a>默认配置方式

- 此配置作用下，SpringMVC的配置**文件默认位于WEB-INF**下，默认名称为< servet-name >-servlet.xml，例如，以下配置所对应SpringMVC的配置文件位于WEB-INF下，文件名为**springMVC-servlet.xml**

```xml
配置springMvc的前端控制器，对浏览器发送的请求统一进行处理
```

### b>扩展配置方式

## 4.创建请求控制器

- 创建控制器: Web.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
	version="4.0">
<!--配置springMvc的前端控制器，对浏览器发送的请求进行统一处理-->
	<servlet>
		<servlet-name>SpringMVC</servlet-name>
		<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
<!--配置springMVC配置文件的位置和名称-->
		<init-param>
			<param-name>contextConfigLocation</param-name>
<!--	文件位于resources目录下	-->
			<param-value>classpath:springMVC.xml</param-value>
		</init-param>
<!--	将前端控制器DispatcherServlet初始化时间提前至服务器启动时	-->
		<load-on-startup>1</load-on-startup>
	</servlet>
	<servlet-mapping>
		<servlet-name>SpringMVC</servlet-name>
<!--
	设置springMVC的核心控制器所能处理的请求的请求路径
	/所匹配的请求可以是/login或.htm1或.js或.css方式的请求路径
	但是/不能匹配.jsp请求路径的请求
-->
		<url-pattern>/</url-pattern>
	</servlet-mapping>
</web-app>
```

## 5.配置springMVC文件

- 配置springMVC文件：resources/springMVC.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

<!--  扫描组件  -->
    <context:component-scan base-package="com.uestc.mvc.controller" />

<!--  配置Thymeleaf视图解析器  -->
    <bean id="viewResolver" class="org.thymeleaf.spring5.view.ThymeleafViewResolver">
<!--        设置优先级-->
        <property name="order" value="1" />
        <property name="characterEncoding" value="UTF-8"/>
        <property name="templateEngine">
            <bean class="org.thymeleaf.spring5.SpringTemplateEngine">
                <property name="templateResolver">
                    <bean class="org.thymeleaf.spring5.templateresolver.SpringResourceTemplateResolver">
                        <!--                视图前缀-->
                        <property name="prefix" value="/WEB-INF/templates/"/>
                        <!--                视图后缀-->
                        <property name="suffix" value=".html"/>
<!--                        处理符号条件的视图-->
                        <property name="templateMode" value="HTML5"/>
                        <property name="characterEncoding" value="UTF-8"/>
                    </bean>
                </property>
            </bean>
        </property>
    </bean>

</beans>
```

## 6.测试HelloWorld

- Maven依赖 pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">  
  <modelVersion>4.0.0</modelVersion>  
  <groupId>com.uestc.mvc</groupId>  
  <artifactId>SpringMVC-demo1</artifactId>  
  <version>1.0-SNAPSHOT</version>  
  <packaging>war</packaging>  
  <dependencies> 
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->  
    <dependency> 
      <groupId>org.springframework</groupId>  
      <artifactId>spring-webmvc</artifactId>  
      <version>5.3.1</version> 
    </dependency>  
    <!-- https://mvnrepository.com/artifact/ch.qos.logback/logback-classic -->  
    <dependency> 
      <groupId>ch.qos.logback</groupId>  
      <artifactId>logback-classic</artifactId>  
      <version>1.2.3</version> 
    </dependency>  
    <!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api -->  
    <dependency> 
      <groupId>javax.servlet</groupId>  
      <artifactId>javax.servlet-api</artifactId>  
      <version>3.1.0</version>  
      <scope>provided</scope> 
    </dependency>  
    <!-- https://mvnrepository.com/artifact/org.thymeleaf/thymeleaf-spring5 -->  
    <!--  Spring5和Thymeleaf整合包  -->  
    <dependency> 
      <groupId>org.thymeleaf</groupId>  
      <artifactId>thymeleaf-spring5</artifactId>  
      <version>3.0.12.RELEASE</version> 
    </dependency> 
  </dependencies>  
  <properties> 
    <maven.compiler.source>8</maven.compiler.source>  
    <maven.compiler.target>8</maven.compiler.target>  
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding> 
  </properties> 
</project>
```

- 设置html的thymeleaf模板(setting/Editor/File and Code Templates)

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
  <meta charset="UTF-8">
  <title>#[[$Title$]]#</title>
</head>
<body>
#[[$END$]]#
</body>
</html>
```

### a>实现对首页的访问

- 绝对路径："/"

1. 浏览器解析：如超连接中的绝对路径，localhost：8080/
2. 服务器解析：工程项目，localhost：8080/工程项目/

### b>实现对其他页面的访问

- /webapp/WEB-INF/templates/index.html

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>title</title>
</head>
<body>
<h1>index.html</h1>
<!--thymeleaf语法-->
    <!--自动添加上下文路径-->
<a th:href="@{/target}">访问目标页面target.html</a>
</body>
</html>
```

- /webapp/WEB-INF/templates/target.html

```xml
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<h1>Target</h1>
</body>
</html>
```

- com/uestc/mvc/controller/HelloController.java

```java
package com.uestc.mvc.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class HelloController {

    // 请求映射注解
    @RequestMapping(value = "/") // 有多个属性可以进行匹配 只有value属性可以省略不写
    public String index() {
        // 访问路径 "/WEB-INF/templates/index.html"
        // 返回视图名称：路径去掉前缀和后缀(前后缀再springMVC.xml配置文件中设置)
        return "index";
    }
    @RequestMapping("/target")
    public String toTarget() {
        return "target";
    }
}
```

## 7.总结

- 浏览器发送请求，若请求地址符合前端控制器的url-pattern，该请求就会被前端控制器DispatcherServlet处理。
- 前端控制器会读取SpringMVC的核心配置文件，通过扫描组件找到控制器，将请求地址和控制器中@RequestMapping注解的value属性值进行匹配，若匹配成功，该注解所标识的控制器方法就是处理请求的方法。
- 处理请求的方法需要返回一个字符串类型的视图名称，该视图名称会被视图解析器解析，加上前缀和后缀组成视图的路径，通过Thymeleaf对视图进行渲染，最终转发到视图所对应页面

# 三.@RequestMapping注解

## 1.@RequestMapping注解的功能

- 从注解名称上我们可以看到，@RequestMapping注解的作用就是将**请求和处理请求**的控制器方法关联起来，建立映射关系。
  SpringMVC 接收到指定的请求，就会来找到在映射关系中对应的控制器方法来处理这个请求。
- 存在多个控制器时，需要保证**请求地址和对应方法是唯一**的。

## 2.@RequestMapping注解的位置

- @RequestMapping标识一个类：设置映射请求的请求路径的初始信息
- @RequestMapping标识一个方法：设置映射请求请求路径的具体信息

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>title</title>
</head>
<body>
<h1>index.html</h1>
<a th:href="@{/method}">测试method</a><!--不能访问-->
<a th:href="@{/class/method}">测试class/method</a><!--能访问-->
</body>
</html>
```

```java
package com.uestc.mvc.controller;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
@Controller
@RequestMapping("/class")
public class RequestMappingController {
    @RequestMapping("/method")
    public String success() {
        return "success";
    }
}
```

## 3.@RequestMapping注解的value属性

- @RequestMapping注解的value属性通过请求的**请求地址匹配**请求映射
- @RequestMapping注解的value属性是一个字符串类型的**数组**，表示该请求映射能够**匹配多个请求地址**所对应的请求
- @RequestMapping注解的value属性**必须设置**(默认值)，至少通过请求地址匹配请求映射
- value属性不匹配--404错误

```java
package com.uestc.mvc.controller;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
@Controller
//@RequestMapping("/class")
public class RequestMappingController {
    @RequestMapping(
            value = {"/method", "/test"}
    )
    public String success() {
        return "success";
    }
}
```

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>title</title>
</head>
<body>
<h1>index.html</h1>
<!--thymeleaf语法-->
<a th:href="@{/test}">测试test</a>
<a th:href="@{/method}">测试method</a>
</body>
</html>
```

## 4.@RequestMapping注解的method属性

- @RequestMapping注解的method属性通过请求的**请求方式**(get或post)匹配请求映射
  - get请求：参数放在请求头中，地址/?name=value&name1=value1；数据量有效
  - post请求：参数放在请求体中，name1=value1；数据量大
- @RequestMapping注解的method属性是一个RequestMethod类型的数组，表示该请求映射能够匹配多种请求方式的请求
- 再满足value的条件下判断method属性是否满足
- 若当前请求的请求地址满足请求映射的vaue属性，但是请求方式不满足method属性，则**浏览器报错405**:
  Request method 'POST' not supported

```java
package com.uestc.mvc.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;

@Controller
//@RequestMapping("/class")
public class RequestMappingController {
    @RequestMapping(
            value = {"/method", "/test"},
            method = {RequestMethod.GET, RequestMethod.POST}
    )
    public String success() {
        return "success";
    }
}
```

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>title</title>
</head>
<body>
<h1>index.html</h1>

<a th:href="@{/test}">测试method属性get</a>

<form th:action="@{/test}" method="post">
    <input type="submit" value="测试method属性post">
</form>
</body>
</html>
```

> 注意：
>
> 1.对于处理指定请求方式的控制器方法，SpringMVC中提供了@RequestMapping的派生注解--**使用该注解可以不在使用method属性**，再注解()内直接加入value值即可
> 处理get请求的映射-->@GetMapping
> 处理post请求的映射-->@PostMapping
> 处理put请求的映射-->@PutMapping
> 处理delete请求的映射-->@DeleteMapping
> 2.常用的请求方式有get，post，put，delete--**不同请求方式表示不同的请求功能**
> 但是目前浏览器只支持get和post，若在form表单提交时，为method设置了其他请求方式的字符串(put或delete)，则按照**默认的请求方式get处理**
> 若要发送put和delete请求，则需要通过spring提供的过滤器HiddenHttpMethodfilter，在restful部分会讲到

```ja
@GetMapping("/testGetMapping")
public String testGetMapping(){
	return "success";
}
```

## 5.@RequestMapping注解的params属性(了解)

- @RequestMapping注解的params属性通过请求的请求参数匹配请求映射 -- **必须所有参数同时满足**

  - 请求params参数不匹配报错400

- @RequestMapping注解的params属性是一个字符串类型的数组，可以通过四种表达式设置请求参数和请求映射的匹配关系

  - "param":要求请求映射所匹配的请求必须携带param请求参数

    ```java
    @RequestMapping(
                value = {"/method", "/test"},
                method = {RequestMethod.GET, RequestMethod.POST},
                params = {"username"}
        )
    // 必须有username参数 -- 其他同理
    ```

  - "!param":要求请求映射所匹配的请求必须不能携带param请求参数

  - "param=value":要求请求映射所匹配的请求必须携带param请求参数目param=value

  - "param!=value":要求请求映射所匹配的请求必须携带param请求参数但是param!=value

```xml
必须所有参数同时满足
<a th:href="@{/test(username='admin', password=123456)">测试@RequestMapping的params属性-->/test</a><br>
```

```html
<!--thymeleaf单引号表示字符-->
<a th:href="@{/testParams(username='zyp001')}">测试params属性</a>
```

## 6.@RequestMapping注解的headers属性(了解)

- @RequestMapping注解的headers属性通过请求的请求头信息匹配请求映射
- @RequestMapping注解的headers属性是一个字符串类型的数组，可以通过四种表达式设置请求头信息和请求映射的匹配关系
  - "header":要求请求映射所匹配的请求必须携带header请求头信息
  - "!header":要求请求映射所匹配的请求必须不能携带header请求头信息
  - "header=value":要求请求映射所匹配的请求必须携带header请求头信息且header=value
  - "header!=value":要求请求映射所匹配的请求必须携带header请求头信息目headerl=value
  - 若当前请求满足@RequestMapping注解的value和method属性，但是不满足headers属性，此时页面显示**404错**
    **误**，即资源未找到

## 7.SpringMVC支持ant风格的路径

- 模糊匹配风格

1. ?：表示任意的单个字符(? 和 / 不可以)
2. *：表示任意的0个或多个字符。
3. **：表示任意的一层或多层目录**
   - 注意：在使用 ** 时，只能使用/ ** / xxx的方式
   - /a**a/ xxx会被解析为两个单 * 号

- 案例演示

```xml
<a th:href="@{/testPath}">测试path匹配1Path</a>
<a th:href="@{/testPaah}">测试path匹配2Paah</a>
```

```java
@RequestMapping(value = "/testP??h")
public String testPath(){
    return "success";
}
```

## 8.SpringMVC支持路径中的占位符(重点)

- 原始方式:/deleteUser?id=1
- rest方式:/deleteUser/1
  - 使用地址表示操作的资源
  - 使用请求方式表示具体的操作
- SpringMVC路径中的占位符常用于**restful风格**中，当请求路径中将某些数据通过路径的方式传输到服务器中，就可以在相应的@RequestMapping注解的value属性中通过占位符(xxx)表示传输的数据，在通过@PathVariable注解，将占位符所表示的数据赋值给控制器方法的形参
- 案例

```java
// 通过@PathVariable注解赋值
@RequestMapping(value = "/testPath/{id}") // 请求地址也必须包含{}占位符对呀的地址
public String testPosit(@PathVariable("id") Integer id){ // 赋值给形参
    System.out.println("id=" + id);
    return "success";
}
```

# 四.SpringMVC获取请求参数

## 1.通过ServletAPI获取

- 将HttpServletRequest作为控制器方法的形参，此时HttpServetRequest类型的参数表示封装了当前请求的请求报文的对象
- 使用通常SpringMVC不使用原生方法获取参数

```java
@Controller
public class ParamController {
    @RequestMapping("/testServletAPI")
    public String testServletAPI(HttpServletRequest request) { // 请求方法中添加HttpServletRequest的参数，会自动注入当前请求的reques实例
        String username = request.getParameter("username");
        String password = request.getParameter("password");
        System.out.println("username=" + username + "::::password=" + password);
        return "success";
    }
}
```

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>测试请求参数</title>
</head>
<body>
<h1>测试请求参数</h1>
<a th:href="@{/testServletAPI(username='admin', password='z123456')}">测试request获取参数</a>
</body>
</html>
```

## 2.通过控制器方法的形参获取请求参数

- 在控制器方法的形参位置，设置和请求参数**同名的形参**，当浏览器发送请求，匹配到请求映射时，在DispatcherServlet中就会将请求参数赋值给相应的形参

```java
@RequestMapping("/testMethodParam")
public String testMethodParam(String username, String password, String hobbyAll) { // 形参名 与 参数名一致会自动注入
    //多值参数(同名参数)有两种获取方式
    // 1. 单个字符， 多个参数用，分割 String hobbyAll
    // 2. 字符数组[] 数组方式保存 String[] hobby
        System.out.println("username=" + username + "::::password=" + password);
        System.out.println("hobby=" + Arrays.toString(hobby));
        System.out.println("hobbyAll=" + hobbyAll);
        return "success";
    }
```

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>测试请求参数</title>
</head>
<body>
<h1>测试请求参数</h1>
<a th:href="@{/testServletAPI(username='admin', password='z123456')}">测试request获取参数</a>
<a th:href="@{/testMethodParam(username='admin', password='z123456')}">测试控制器获取参数</a>
<form th:action="@{/testMethodParam}" method="post">
    用户名：<input type="text" name="username"><br/>
    密码：<input type="password" name="password"><br/>
    爱好：<input type="checkbox" name="hobby" value="a">a<br/>
<input type="checkbox" name="hobby" value="b">b<br/>
<input type="checkbox" name="hobby" value="c">c<br/>
    <input type="submit" value="提交">
</form>
</body>
</html>
```

- 注意

> 1.若请求所传输的请求参数中有**多个同名的请求参数**，此时可以在控制器方法的形参中设置字符串数组或者字符串类型的形参接收此请求参数
> 2.若使用字符串数组类型的形参，此参数的数组中包含了每一个数据
> 3.若使用字符串类型的形参，此参数的值为每个数据中间使用**逗号拼接**的结果

- 通过@RequestParam()注解指定形参(可以不同名)
  - required参数：使用@RequestParam()的参数默认(required=true)必须传输，@RequestParam(value = "hobby", required = false)
    - required 设置为false可以改为不必须传输
  - defaultValue参数：defaultValue = "hehe" 设置不传递参数的默认值

```java
@RequestMapping("/testMethodParam")
    public String testMethodParam(String username, String password, String[] hobby, @RequestParam("hobby") String hobbyAll) {
        System.out.println("username=" + username + "::::password=" + password);
        System.out.println("hobby=" + Arrays.toString(hobby));
        System.out.println("hobbyAll=" + hobbyAll);
        return "success";
    }
```

## 3.@RequestParam

- @RequestParam是将请求参数和控制器方法的形参创建映射关系
- @RequestParam注解一共有三个属性:
  - value:指定为形参赋值的请求参数的参数名
  - required:设置是否必须传输此请求参数，默认值为true
    - 若设置为true时，则当前请求必须传输value所指定的请求参数，若没有传输该请求参数，且没有设置defaultValue属性，则页面报错400:Required String parameter'xxx'is not present;
    - 若设置为false，则当前请求不是必须传输value所指定的请求参数，若没有传输，则注解所标识的形参的值为null
  - defaultValue:不管required属性值为true或false，当value所指定的请求参数没有传输或为"空字符串"时，则使用默认值为形参赋值

## 4.@RequestHeader

- @RequestHeader是将请求头信息和控制器方法的形参创建映射关系
- @RequestHeader注解一共有三个属性:value、required、defaultValue，用法同@RequestParam

```java
@RequestMapping("/testMethodParam")
public String testMethodParam(String username, String password, String[] hobby, @RequestParam("hobby") String hobbyAll,
                              @RequestHeader("Host") String host) { // 形参名 与 参数名一致会自动注入
    System.out.println("username=" + username + "::::password=" + password);
    System.out.println("hobby=" + Arrays.toString(hobby));
    System.out.println("hobbyAll=" + hobbyAll);
    System.out.println("Host=" + host);
    return "success";
}
```



## 5.@CookieValue

- @CookieValue是将cookie数据和控制器方法的形参创建映射关系
  - session依赖cookie
  - cookie是客户端的会话技术
  - session是服务器端的会话技术
- @CookieValue注解一共有三个属性:value、required、defaultValue，用法同@RequestParam

```java
@Controller
public class ParamController {
    @RequestMapping("/testServletAPI")
    public String testServletAPI(HttpServletRequest request) { // 请求方法中添加HttpServletRequest的参数，会自动注入当前请求的reques实例
        HttpSession session = request.getSession();
        String username = request.getParameter("username");
        String password = request.getParameter("password");
        System.out.println("username=" + username + "::::password=" + password);
        return "success";
    }
    @RequestMapping("/testMethodParam")
    public String testMethodParam(String username, String password, String[] hobby, @RequestParam("hobby") String hobbyAll,
                                  @RequestHeader("Host") String host,
                                  @CookieValue("JSESSIONID") String JSESSIONID

    ) { // 形参名 与 参数名一致会自动注入
        System.out.println("username=" + username + "::::password=" + password);
        System.out.println("hobby=" + Arrays.toString(hobby));
        System.out.println("hobbyAll=" + hobbyAll);
        System.out.println("Host=" + host);
        System.out.println("JSESSIONID=" + JSESSIONID); // 需要先创建session HttpSession session = request.getSession();
        return "success";
    }
}
```

## 6.通过POJO获取请求参数

- 可以在控制器方法的形参位置设置一个实体类类型的形参，此时若浏览器传输的请求参数的参数名和实体类中的属性名一致，那么请求参数就会为此属性赋值

```html
<form th:action="@{/testBean}" method="post">
    用户名：<input type="text" name="username"><br/>
    密码：<input type="password" name="password"><br/>
    性别：<input type="checkbox" name="sex" value="男">男<br/>
    <input type="checkbox" name="sex" value="女">女<br/>
    年龄：<input type="text" name="age"><br/>
    邮箱：<input type="text" name="email"><br/>
    <input type="submit" value="使用实体类接收请求参数">
</form>
```

```java
@RequestMapping("/testBean")
public String testBean(User user) { // 强求参数越多，不利于用参数注入请求信息
    // 若存在多个满足条件的Bean形参都会被赋值
    System.out.println(user);
    return "success";
}
```

## 7.解决获取请求参数的乱码问题

- Get请求的乱码是由TomCat造成的。

  - TomCat/conf/server.xml：添加URIEncoding="utf-8"

    ```xml
    <Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443"
               maxParameterCount="1000"
               URIEncoding="utf-8"
               />
    ```

- Post请求的乱码是服务器获取参数是造成的。

  - 使用过滤器解决。web.xml文件中配置过滤器。

    ```xml
    <filter>
        <filter-name>CharacterEncodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <!--			对过滤器的encoding属性赋值-->
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
        <init-param>
            <!--			响应编码赋值-->
            <param-name>forceResponseEncoding</param-name>
            <param-value>ture</param-value>
        </init-param>
    </filter>
    ```

# 五.域对象共享数据

## 1.使用servletAPl向request域对象共享数据

```java
@RequestMapping("/testRequestByServletAPI")
public String testRequestByServletAPI(HttpServletRequest request) {
    request.setAttribute("testScope", "hello, ServletRequest");
    return "success";
}
```

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>成功</title>
</head>
<body>
<h1>
    成功
</h1>
<p th:text="${testRequestScope}"></p>
</body>
</html>
```

```html
<a th:href="@{/testRequestByServletAPI}">通过servletAPI向request域对象共享数据</a>
```

## 2.使用ModelAndView向request域对象共享数据

```java
@RequestMapping("/testModelAndView")
public ModelAndView testModelAndView() {
    // ModelAndview有Mode1和View的功能
    // Mode1主要用于向请求域共享数据
    // view主要用于设置视图，实现页面跳转
    ModelAndView mav = new ModelAndView();
    // 处理模型数据，即向请求域request共享数据
    mav.addObject("testScope", "hello, ModelAndView");
    // 设置视图名称
    mav.setViewName("success"); // 相当于 return "success";
    return mav;
}
```

## 3.使用Model向request域对象共享数据

```java
@RequestMapping("/testModel")
public String testModel(Model model) {
    model.addAttribute("testScope", "hello, testModel");
    return "success";
}
```

## 4.使用map向request域对象共享数据

```java
@RequestMapping("/testMap")
public String testModel(Map<String, Object> map) {
    map.put("testScope", "hello, testMap");
    return "success";
}
```

## 5.使用ModelMap向request域对象共享数据

```java
@RequestMapping("/testModelMap")
public String testModelMap(ModelMap modelMap) {
    modelMap.addAttribute("testScope", "hello, testModelMap");
    return "success";
}
```

## 6.Model、ModelMap、Map的关系

- Model、ModelMap、Map类型的参数其实本质上都是 BindingAwareModelMap 类型

```java
System.out.println(model.getClass().getName());
System.out.println(map.getClass().getName());
System.out.println(modelMap.getClass().getName());
```

```java
public interface Model{}
public class ModelMap extends LinkedHashMap<string, object> {}
public class ExtendedModelMap extends ModelMap implements Model {}
public class BindingAwareModelMap extends ExtendedModelMap {}
```

## 7.向session域共享数据

- MVC提供注解将请求域的数据复制到session域
- 推荐使用原生的Httpsession(ServletAPI)

```java
@RequestMapping("/testApplication")
public String testApplication(HttpSession session) {
    ServletContext application = session.getServletContext();
    application.setAttribute("testApplication", "hello, testApplication");
    return "success";
}
```

# 六.springMVC的视图

- SpringMVC中的视图是View接口，视图的作用渲染数据，将模型Model中的数据展示给用户
- SpringMVC视图的种类很多，默认有转发视图lnternalResourceView和重定向视图RedirectView
- 当工程引入jstl的依赖，转发视图会自动转换为JstlView
- 若使用的视图技术为Thymeleaf，在SpringMVC的配置文件中配置了Thymeleaf的视图解析器，由此视图解析器解析之后所得到的是ThymeleafView

## 1.ThymeleafView

当控制器方法中所设置的视图名称没有任何前缀时，此时的视图名称会被SpringMVC配置文件中所配置的视图解析器解析，视图名称拼接视图前缀和视图后缀所得到的最终路径，会通过**转发**(lnternalResourceView)的方式实现跳转

```java
@RequestMapping("/testHello")
public String testHello() {
    return "hello";
}
```

## 2.转发视图

- SpringMVC中默认的转发视图是InternalResourceView
- SpringMVC中创建转发视图的情况:
- 当控制器方法中所设置的视图名称以"forward:"为前缀时，创建InternalResourceView视图，此时的视图名称不会被SpringMVC配置文件中所配置的视图解析器解析，而是会将前缀"forward:"去掉，剩余部分作为最终路径通过转发的方式实现跳转
  例如"forward:/","forward:/employee"

```java
@RequestMapping("/testForward")
public String testForward() { // 转发到页面 或 请求
    return "forward:/testThymeleafView";
}
```

## 3.重定向视图

- SpringMVC中默认的重定向视图是RedirectView
- 当控制器方法中所设置的视图名称以"redirect:"为前缀时，创建RedirectView视图，此时的视图名称不会被SpringMVC配置文件中所配置的视图解析器解析，而是会将前缀"redirect:"去掉，剩余部分作为最终路径通过定向的方式实现跳转
  例如"redirect:/","redirect:/employee"

- 转发和重定向的区别

1. 转发浏览器发送一次请求(地址不变服务器转发到新的地址)，重定向发送两次(servlet地址和重定向地址，地址改变：重定向的地址)
2. 转发保留request域的数据，重定向不保留request域的数据
3. 转发只能访问服务器内部资源，重定向可以访问任何资源

## 4.视图控制器view-controller

- springMVC.xml配置文件中，被ThymeleafView视图解析器解析，加前缀加后缀，但无法处理请求
  - 没有控制请求，只有视图名称时可以使用
  - 使用该方法时，控制器中的所有请求处理方法都会**失效**，需要添加< mvc:annotation-driven / >标签

```xml
<mvc:view-controller path="/" view-name="index"></mvc:view-controller>
<!--  开启MVC的注解驱动  -->
    <mvc:annotation-driven/>
```

## 5.JSP页面的转发和重定向

- 视图解析器不同，其他与html页面的基本一致

```xml
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/templates/"/>
        <property name="suffix" value=".jsp"/>
    </bean>
```

# 七.RESTFUI

## 1.RESTFuI简介

- REST:Representational State Transfer，表现层资源状态转移。

1. 资源：资源是一种看待服务器的方式，即，将服务器看作是由很多离散的资源组成。每个资源是服务器上一个可命名的抽象概念。因为资源是一个抽象的概念，所以它不仅仅能代表服务器文件系统中的一个文件、数据库中的一张表等等具体的东西，可以将资源设计的要多抽象有多抽象，只要想象力允许而且客户端应用开发者能够解。与面向对象设计类似，**资源是以名词为核心来组织的**，首先关注的是名词。一个资源可以由一个或多个URI来标识。URI既是资源的名称，也是资源在Web上的地址。对某个资源感兴趣的客户端应用，可以通过资源的URI与其进行交互。
2. 资源的表述：资源的表述是一段对于资源在某个特定时刻的状态的描述。可以在客户端-服务器端之间转移(交换)。资源的表述可以有多种格式，例如HTML/XML/JSON/纯文本/图片/视频/音频等等。资源的表述格式可以通过协商机制来确定。请求-响应方向的表述通常使用不同的格式。
3. 状态转移：状态转移说的是:在客户端和服务器端之间转移(transfer)表资源状态的表述。通过转移和操作资源的表述来间接实现操作资源的目的。

## 2.RESTFuI的实现

- 具体说，就是 HTTP 协议里面，四个表示操作方式的动词:GET、POST、PUT、DELETE。
- 它们分别对应四种基本操作:GET 用来获取资源，POST用来新建资源，PUT用来更新资源，DELETE 用来删除资源。
- REST 风格提倡 URL地址使用统一的风格设计，从前到后各个单词使用**斜杠**分开，不使用问号键值对方式携带请求参数，而是将要发送给服务器的数据作为 URL 地址的一部分，以保证整体风格的一致性。

| 操作     | 传统方式         | REST风格                |
| -------- | ---------------- | ----------------------- |
| 查询操作 | getUserByld?id=1 | user/1-->get请求方式    |
| 保存操作 | saveUser         | user-->post请求方式     |
| 删除操作 | deleteUser?id=1  | user/1-->delete请求方式 |
| 更新操作 | updateUser       | user-->put请求方式      |

- 演示案例

1. post/get请求：正常使用html的表单/超连接即可
2. put/delete请求：需要使用过滤器
   - 原始请求方式必须为post
   - 设置请求参数"_method"记录实际的请求方式

```xml
<!--编码过滤器需要放在前面否则会失效。设置编码前不能获取请求参数，否则失效。HiddenHttpMethodFilter会使用请求参数-->
<!--web.xml配置过滤器-->
<!--配置HiddenHttpMethodFilter-->
	<filter>
		<filter-name>HiddenHttpMethodFilter</filter-name>
		<filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>
	</filter>
	<filter-mapping>
		<filter-name>HiddenHttpMethodFilter</filter-name>
		<url-pattern>/*</url-pattern>
	</filter-mapping>
```

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<a th:href="@{/user}">查询所有用户信息</a><br/>
<a th:href="@{/user/1}">根据id查询用户信息</a><br/>
<form th:action="@{/user}" method="post">
    用户名：<input type="text" name="username"><br>
    密码：<input type="password" name="password"><br>
    <input type="submit" value="提交">
</form>
<!--请求方式不是get/post时默认按照get-->
<form th:action="@{/user}" method="post">
    <input type="hidden" name="_method" value="PUT">
    用户名：<input type="text" name="username"><br>
    密码：<input type="password" name="password"><br>
    <input type="submit" value="修改">
</form>
</body>
</html>
```

```java
package com.uestc.mvc.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
@Controller
public class UserController {
    /**
     * 使用RESTFUL模拟用户资源的增删改查
     * /user GET 查询所有用户信息
     * /user/1 GET 根据用id查询用户信息
     * /user POST 添加用户信息
     * /user/1 DELETE 删除用户信息
     * /user PUT 修改用户信息
     */
    @RequestMapping(value = "/user", method = RequestMethod.GET)
    public String getAllUser() {
        System.out.println("查询所有用户信息");
        return "success";
    }
    @RequestMapping(value = "/user/{id}", method = RequestMethod.GET)
    public String getUserById(@PathVariable("id") Integer id) {
        System.out.println("根据id=" + id + "查询用户信息");
        return "success";
    }
    @RequestMapping(value = "/user", method = RequestMethod.POST)
    public String insertUser(String username, String password) {
        System.out.println("添加用户名：" + username + "|密码=" + password);
        return "success";
    }
    @RequestMapping(value = "/user", method = RequestMethod.PUT)
    public String updateUser(String username, String password) {
        System.out.println("修改用户名：" + username + "|密码=" + password);
        return "success";
    }
}
```

# 八.演示案例

## 1.准备工作

- springMVC-rest项目文件下

- web.xml配置文件：两个过滤器，一个servlet前端控制器

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
<!--编码过滤器-->
    <filter>
        <filter-name>CharacterEncodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
        <init-param>
            <param-name>forceResponseEncoding</param-name>
            <param-value>true</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>CharacterEncodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
<!--配置请求过滤器-->
    <filter>
        <filter-name>HiddenHttpMethodFilter</filter-name>
        <filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>HiddenHttpMethodFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
<!--配置前端控制器DispatcherServlet-->
    <servlet>
        <servlet-name>DispatcherServlet</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:springMVC.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>DispatcherServlet</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
</web-app>
```

- springMVC.xml配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">
<!--开启组件扫描-->
    <context:component-scan base-package="com.uestc.mvc"/>
<!--配置Thymeleaf视图解析器-->
    <bean id="viewResolver" class="org.thymeleaf.spring5.view.ThymeleafViewResolver">
        <!--        设置优先级-->
        <property name="order" value="1" />
        <property name="characterEncoding" value="UTF-8"/>
        <property name="templateEngine">
            <bean class="org.thymeleaf.spring5.SpringTemplateEngine">
                <property name="templateResolver">
                    <bean class="org.thymeleaf.spring5.templateresolver.SpringResourceTemplateResolver">
                        <!--                视图前缀-->
                        <property name="prefix" value="/WEB-INF/templates/"/>
                        <!--                视图后缀-->
                        <property name="suffix" value=".html"/>
                        <!--                        处理符号条件的视图-->
                        <property name="templateMode" value="HTML5"/>
                        <property name="characterEncoding" value="UTF-8"/>
                    </bean>
                </property>
            </bean>
        </property>
    </bean>
</beans>
```

- Bean类

```java
package com.uestc.mvc.bean;

public class Employee {
    private Integer id;
    private String lastName;
    private String email;
    private Integer gender;
    public Employee(Integer id, String lastName, String email, Integer gender) {
        this.id = id;
        this.lastName = lastName;
        this.email = email;
        this.gender = gender;
    }
    public Employee() {
    }
    @Override
    public String toString() {
        return "Employee{" +
                "id=" + id +
                ", lastName='" + lastName + '\'' +
                ", email='" + email + '\'' +
                ", gender=" + gender +
                '}';
    }
    public Integer getId() {
        return id;
    }
    public void setId(Integer id) {
        this.id = id;
    }
    public String getLastName() {
        return lastName;
    }
    public void setLastName(String lastName) {
        this.lastName = lastName;
    }
    public String getEmail() {
        return email;
    }
    public void setEmail(String email) {
        this.email = email;
    }
    public Integer getGender() {
        return gender;
    }
    public void setGender(Integer gender) {
        this.gender = gender;
    }
}
```

- 持久层

```java
package com.uestc.mvc.Dao;

import com.uestc.mvc.bean.Employee;
import org.springframework.stereotype.Repository;

import java.util.Collection;
import java.util.HashMap;
import java.util.Map;
// 添加持久层组件的注解
@Repository
public class EmployeeDao {
    private static Map<Integer, Employee> employees = new HashMap<>();
    static {
        employees.put(1001,new Employee(1001,"E-AA", "aaG163.com", 1));
        employees.put(1002,new Employee(1002,"E-BB","bb@163.com", 1));
        employees.put(1003,new Employee(1003,"E-CC", "cc@163.com", 0));
        employees.put(1004,new Employee(1004, "E-DD","dd163.com", 0));
        employees.put(1005,new Employee(1005,"E-EE","ee@163.com", 1));
    }
    private static Integer initId = 1006;
    public void save(Employee employee) { // 添加和更新
        if (employee.getEmail() == null) {
            employee.setId(initId++);
        }
        employees.put(employee.getId(), employee);
    }
    public Collection<Employee> getAll() {
        return employees.values();
    }
    public Employee get(Integer id) {
        return employees.get(id);
    }
    public void delete(Integer id) {
        employees.remove(id);
    }
}
```

## 2.功能清单

| 功能               | URL地址     | 请求方式 |
| ------------------ | ----------- | -------- |
| 访问首页           | /           | GET      |
| 查询全部数据       | /employee   | GET      |
| 删除               | /employee/2 | DELETE   |
| 跳转到添加数据页面 | /toAdd      | GET      |
| 执行保存           | /employee   | POST     |
| 跳转到更新数据页面 | /employee/2 | GET      |
| 执行更新           | /employee   | PUT      |

- 设置初始页面：修改配置文件或创建控制器类

  ```xml
  <!--修改配置文件：springMVC.xml文件中添加-->
  <!--配置视图控制器-->
  <mvc:view-controller path="/" view-name="index"/>
  <!--开启注解驱动-->
  <mvc:annotation-driven/>
  ```

- 查询全部数据

  1. 转发请求

  ```html
  <a th:href="@{/employee}">查看所有员工信息</a>
  ```

  2. 处理请求并转发

  ```java
  @RequestMapping(value = "/employee", method = RequestMethod.GET)
  public String getAllEmployee(Model model) {
      Collection<Employee> allEmp = employeeDao.getAll();
      model.addAttribute("employees", allEmp);
      return "employee_list";
  }
  ```

  3. 转发的页面

  ```html
  <!DOCTYPE html>
  <html lang="en" xmlns:th="http://www.thymeleaf.org">
  <head>
      <meta charset="UTF-8">
      <title>employee_list</title>
  </head>
  <body>
  <table border="1" style="text-align: center">
      <tr><th colspan="5">Employee Info</th></tr>
      <tr>
          <th>id</th>
          <th>lastName</th>
          <th>email</th>
          <th>gender</th>
          <th>options</th>
      </tr>
      <tr th:each="employee: ${employees}">
          <td th:text="${employee.id}"></td>
          <td th:text="${employee.lastName}"></td>
          <td th:text="${employee.email}"></td>
          <td th:text="${employee.gender}"></td>
          <td>
              <a href="">update</a>
              <a href="">delete</a>
          </td>
      </tr>
  </table>
  </body>
  </html>
  ```

- 删除

  0. 1Maven工程重新打包package，将static/vue.js导入包内 | 2修改springMVC .xml配置文件

  ```xml
  <!--开放访问静态资源-->
  <mvc:default-servlet-handler />
  <!--先把请求交给MVC处理，找不到资源再交给默认servlet处理-->
  ```

  1. 发起请求

  ```html
  <!DOCTYPE html>
  <html lang="en" xmlns:th="http://www.thymeleaf.org">
  <head>
      <meta charset="UTF-8">
      <title>employee_list</title>
  </head>
  <body>
  <table id="dataTable" border="1" style="text-align: center">
      <tr><th colspan="5">Employee Info</th></tr>
      <tr>
          <th>id</th>
          <th>lastName</th>
          <th>email</th>
          <th>gender</th>
          <th>options</th>
      </tr>
      <tr th:each="employee: ${employees}">
          <td th:text="${employee.id}"></td>
          <td th:text="${employee.lastName}"></td>
          <td th:text="${employee.email}"></td>
          <td th:text="${employee.gender}"></td>
          <td>
  <!--            两种拼接方式-->
              <a @click="deleteEmployee" th:href="@{/employee/} + ${employee.id}">delete1</a>
  <!--            <a th:href="@{'/employee/' + ${employee.id}}">udelete2</a>-->
              <a href="">update</a>
          </td>
      </tr>
  </table>
  <form id="deleteForm" method="post">
      <input type="hidden" name="_method" value="delete">
  </form>
  <script type="text/javascript" th:src="@{/static/js/vue.js}"></script>
  <script type="text/javascript">
      var vue = new Vue({
          el:"#dataTable",
          methods:{
              deleteEmployee:function (event) {
                  var deleteForm = document.getElementById("deleteForm");
                  // 将触发点击事件的超链接的href属性赋值给表单的action
                  deleteForm.action = event.target.href;
                  deleteForm.submit();
                  // 取消超链接的默认行为
                  event.preventDefault();
  
              }
          }
      })
  </script>
  </body>
  </html>
  ```

  - 处理请求

  ```java
  @RequestMapping(value = "/employee/{id}", method = RequestMethod.DELETE)
  public String deleteEmpployee(@PathVariable("id") Integer id) {
      employeeDao.delete(id);
      return "redirect:/employee";
  }
  ```

- 添加

  1. 增加添加表单的视图

  ```xml
  <!--springMVC中添加-->
  <mvc:view-controller path="/toAdd" view-name="employee_add"/>
  ```

  ```html
  <!--创建新的添加页面employee_add.html-->
  <!DOCTYPE html>
  <html lang="en" xmlns:th="http://www.thymeleaf.org">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
  </head>
  <body>
  <form th:action="@{/employee}" method="post">
      lastName:<input type="text" name="lastName"><br>
      email:<input type="text" name="email"><br>
      gender:<input type="radio" name="gender" value="1">male
      <input type="radio" name="gender" value="1">female<br>
      <input type="submit" value="add"><br>
  </form>
  </body>
  </html>
  ```

  2. 请求处理

  ```java
  @RequestMapping(value = "/employee", method = RequestMethod.POST)
  public String addEmployee(Employee employee) {
      employeeDao.save(employee);
      System.out.println("add:" + employee);
      return "redirect:/employee";
  }
  ```

- 查询

  1. 添加请求

  ```xml
  <a th:href="@{'/employee/' + ${employee.id}}">update</a>
  ```

  2. 表单回显

  ```xml
  <!DOCTYPE html>
  <html lang="en" xmlns:th="http://www.thymeleaf.org">
  <head>
      <meta charset="UTF-8">
      <title>update</title>
  </head>
  <body>
  <form th:action="@{/employee}" method="post">
      <input type="hidden" name="_method" value="put">
      <input type="hidden" name="id" th:value="${employee.id}"><br>
      lastName:<input type="text" name="lastName" th:value="${employee.lastName}"><br>
      email:<input type="text" name="email" th:value="${employee.email}"><br>
      gender:<input type="radio" name="gender" value="1" th:field="${employee.gender}">male
      <input type="radio" name="gender" value="0" th:field="${employee.gender}">female<br>
      <input type="submit" value="update"><br>
  </form>
  </body>
  </html>
  ```

  3. 处理请求

  ```java
  @RequestMapping(value = "/employee", method = RequestMethod.PUT)
  public String updateEmployee(Employee employee) {
      employeeDao.save(employee);
      return "redirect:/employee";
  }
  ```

# 九. HttpMessageconverter

- HttpMessageConverter,报文信息转换器,将请求报文转换为]ava对象，或将]ava对象转换为响应报文
- HttpMessageConverter提供了两个注解和两个类型:
  - @RequestBody,@ResponseBody
  - RequestEntity,ResponseEntity

## 1.@RequestBody

- @RequestBody可以**获取请求体**，需要在控制器方法设置一个形参，使用@RequestBody进行标识，当前请求的请求体就会为当前注解所标识的形参赋值

```html
<form th:action="@{/testRequestBody}" method="post">
    username:<input type="text" name="username"><br>
    password:<input type="password" name="password"><br>
    <input type="submit" value="测试@RequestBody"><br>
</form>
```

```java
@RequestMapping("/testRequestBody")
public String testRequestBody(@RequestBody String requestBody) {
    System.out.println("requestBody:" + requestBody);
    return "success";
}
```

## 2.RequestEntity

- RequestEntity封装**请求报文**的**一种类型**，需要在控制器方法的形参中设置该类型的形参，当前请求的请求报文就会赋值给该形参，可以通过getHeaders()获取请求头信息，通过getBody()获取请求体信息

```java
@RequestMapping("/testRequestEntity")
public String testRequestEntity(RequestEntity<String> requestEntity) {
    // 当前requestEntity表示整个请求报文的信息
    System.out.println("请求头：" + requestEntity.getHeaders());
    System.out.println("请求体：" + requestEntity.getBody());
    return "success";
}
```

## 3.@ResponseBody

- @ResponseBody用于标识一个控制器方法，可以将该方法的返回值直接作为响应报文的响应体响应到浏览器

```java
// 原生的servlet响应请求
@RequestMapping("/testResponse")
public void testResponse(HttpServletResponse response) throws IOException {
    response.getWriter().print("hello,response");
}
```

```java
// @ResponseBody 返回值为响应体的内容
@RequestMapping("/testResponseBody")
@ResponseBody
public String testResponseBody() {
    return "success-test"; // 返回响应体
}
```

## 4.@ResponseBody处理json

- @ResponseBody处理json的4个步骤

1. 导从jackson的依赖

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.12.1</version>
</dependency>
```

2. 在SpringMVC的核心配置文件中开启mvc的注解驱动，此时在HandlerAdaptor中会自动装配一个消息转换器:
   Mappinelackson2HttoMessageConverter.可以将响应到浏览器的Java对象转换为Json格式的字符串

```xml
<!--开启注解驱动-->
<mvc:annotation-driven/>
```

3. 在处理器方法上使用@ResponseBody注解进行标识
4. 将]ava对象直接作为控制器方法的返回值返回，就会自动转换为**Json格式的字符串**
   - 最外面是{}时，是Json对象
   - 最外面是[]时，是Json数组

```java
@RequestMapping("/testResponseBodyUser")
@ResponseBody
public User testResponseBodyUse() {
    return new User(1001, "zyp", "z123456", 18, "男"); // 浏览器无法解析Java语言的对象，可以解析Json文件
}
```

## 5.SpringMVC处理ajax

1. 请求超链接
2. 通过vue和axios处理点击事件

```html
<a th:href="@{/testResponseBodyUser}">通过@ResponseBodyUser响应浏览器User对象</a><br>
<div id="app">
    <a @click="testAxios" th:href="@{/testAxios}">SpringMVC处理Ajax</a>
</div>
<script type="text/javascript" th:src="@{/static/js/vue.js}"></script>
<script type="text/javascript" th:src="@{/static/js/axios.min.js}"></script>
<script type="text/javascript">
    new Vue({
        el:"#app",
        methods:{
            testAxios:function (event) {
                axios({
                    method:"post",
                    url:event.target.href,
                    params:{
                        username:"admin",
                        password:"123456"
                    }
                }).then(function (response) {
                    alert(response.data);
                });
                event.preventDefault();
            }
        }
    });
</script>
```

3. 控制器方法

```java
@RequestMapping("/testAxios")
@ResponseBody
public String testAxios(String username, String password) {
    System.out.println("username:" + username + "|password:" + password);
    return "hello,Axios";
}
```

## 6.@RestController注解

- @RestController注解是springMVC提供的一个复合注解，标识在控制器的类上，就相当于为类添加了@Controller注解，并且为其中的每个方法添加了@ResponseBody注解

## 7.ResponseEntity

- ResponseEntity用于控制器方法的**返回值类型**，该控制器方法的返回值就是响应到浏览器的响应报文
  - 可以实现文件下载功能

# 九.文件上传和下载

## 1.下载功能

- 发送下载请求

```html
<a th:href="@{/testDown}">下载BossX.jsp</a>
```

- 处理请求

```java
@RequestMapping("/testDown")
public ResponseEntity<byte[]> testResponseEntity(HttpSession session) throws IOException {
    // 获取ServletContext对象
    ServletContext servletContext = session.getServletContext();
    // 获取服务器中文件的真实路径
    String realPath = servletContext.getRealPath("/static/img/BossX.jpg");
    System.out.println(realPath);
    //创建输入流
    FileInputStream inputStream = new FileInputStream(realPath);
    // 创建字节数组
    byte[] bytes = new byte[inputStream.available()];
    // 将流读到字节数组中
    inputStream.read(bytes);
    // 创建HttpHeaders对象设置响应头信息
    MultiValueMap<String, String> headers = new HttpHeaders();
    // 设置要下载方式以及下载文件的名字
    headers.add("Content-Disposition", "attachment;filename=BossX.jpg"); // 默认名称
    // 设置响应状态码
    HttpStatus statusCode = HttpStatus.OK;
    // 创建ResponseEntity对象
    // 设置响应头/响应体/响应状态码
    ResponseEntity<byte[]> responseEntity = new ResponseEntity<>(bytes, headers, statusCode);
    // 关闭输入流
    inputStream.close();
    return responseEntity;
}
```

## 2.文件上传

- 文件上传要求form表单的请求方式必须为post，并且添加属性enctype="multipart/form-data"
  SpringMVC中将上传的文件封装到MultipartFile对象中，通过此对象可以获取文件相关信息
- 上传步骤

1. 添加依赖

```xml
<!-- https://mvnrepository.com/artifact/commons-fileupload/commons-fileupload -->
<dependency>
    <groupId>commons-fileupload</groupId>
    <artifactId>commons-fileupload</artifactId>
    <version>1.3.1</version>
</dependency>
```

2. 在SpringMVC的配置文件中添加配置:文件上传解析器

```xml
<!--配置文件上传解析器，将上传的文件封装为MultipartFile
根据id获取/id必须为multipartResolver
-->
    <bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver"></bean>
```

3. 发送上传请求

```html
<!--enctype:设置请求体以二进制的形式传输-->
<form th:action="@{/testUp}" method="post" enctype="multipart/form-data">
    头像：<input type="file" name="photo"><br>
    <input type="submit" value="提交">
</form>
```

4. 处理下载请求

```java
@RequestMapping("/testUp")
// MultipartFile 文件的接收类
public String testUp(MultipartFile photo, HttpSession session) throws IOException {
    String filename = photo.getOriginalFilename();
    ServletContext servletContext = session.getServletContext();
    String realPath = servletContext.getRealPath("photo");
    File file = new File(realPath);
    // 判断路径是否存在
    if (!file.exists()) {
        file.mkdir();
    }
    // File.separator 文件分隔符合
    String finalPath = realPath + File.separator + filename;
    photo.transferTo(new File(finalPath));
    return "success";
}
```

## 3.文件重名问题

使用UUID当作文件名

```java
@RequestMapping("/testUp")
// MultipartFile 文件的接收类
public String testUp(MultipartFile photo, HttpSession session) throws IOException {
    // 获取上传的文件的文件名
    String filename = photo.getOriginalFilename();
    // 获取文件后缀
    String suffixName = filename.substring(filename.lastIndexOf("."));
    // 将UUID作为文件名
    String uUid = UUID.randomUUID().toString();
    // 将uuid和后缀名拼接后的结果作为最终的文件名
    filename = uUid + suffixName;
    // 通过ServletContext获取服务器中photo日录的路径
    ServletContext servletContext = session.getServletContext();
    String realPath = servletContext.getRealPath("photo");
    File file = new File(realPath);
    // 判断路径是否存在
    if (!file.exists()) {
        file.mkdir();
    }
    // File.separator 文件分隔符合
    String finalPath = realPath + File.separator + filename;
    photo.transferTo(new File(finalPath));
    return "success";
}
```

# 十.拦截器

## 1.拦截器的配置

- SpringMVC中的拦截器用于**拦截控制器方法**的执行
  - 请求->filter-> DispatcherServlet->拦截器->Controller控制器方法
  - 拦截器三个重要方法执行时间，控制器方法执行前/控制器方法执行后/视图渲染后
    - preHandle
    - postHandle
    - afterCompletion
- SpringMVC中的拦截器需要实现Handlerinterceptor接口或者继承HandlerinterceptorAdapter类
- SpringMVC的拦截器必须在SpringMVC的配置文件中进行配置:

1. 再springMVC.xml中配置拦截器

   1. 方法1:所有控制器方法都会拦截

   ```xml
   <!--配置拦截器-->
   <mvc:interceptors>
       <bean class="com.uestc.mvc.interceptors.FirstInterceptor"></bean>
   </mvc:interceptors>
   ```

   ```java
   package com.uestc.mvc.interceptors;
   import org.springframework.web.servlet.HandlerInterceptor;
   import org.springframework.web.servlet.ModelAndView;
   import javax.servlet.http.HttpServletRequest;
   import javax.servlet.http.HttpServletResponse;
   
   public class FirstInterceptor implements HandlerInterceptor {
       @Override
       public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
           System.out.println("FirstInterceptor-->preHandle");
           // 返回ture表示放行/ false表示拦截
           return HandlerInterceptor.super.preHandle(request, response, handler);
       }
       @Override
       public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
           System.out.println("FirstInterceptor-->postHandle");
           HandlerInterceptor.super.postHandle(request, response, handler, modelAndView);
       }
       @Override
       public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
           System.out.println("FirstInterceptor-->afterCompletion");
           HandlerInterceptor.super.afterCompletion(request, response, handler, ex);
       }
   }
   ```

   2. 方法2:所有控制器方法都会拦截

   ```xml
   <!--配置拦截器-->
   <mvc:interceptors>
    <ref bean="firstInterceptor"/>
   </mvc:interceptors>
   ```

   ```java
   
   ```java
   package com.uestc.mvc.interceptors;
   import org.springframework.stereotype.Component;
   import org.springframework.web.servlet.HandlerInterceptor;
   import org.springframework.web.servlet.ModelAndView;
   import javax.servlet.http.HttpServletRequest;
   import javax.servlet.http.HttpServletResponse;
   
   @Component
   public class FirstInterceptor implements HandlerInterceptor {
       @Override
       public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
           System.out.println("FirstInterceptor-->preHandle");
           // 返回ture表示放行/ false表示拦截
           return HandlerInterceptor.super.preHandle(request, response, handler);
       }
       @Override
       public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
           System.out.println("FirstInterceptor-->postHandle");
           HandlerInterceptor.super.postHandle(request, response, handler, modelAndView);
       }
       @Override
       public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
           System.out.println("FirstInterceptor-->afterCompletion");
           HandlerInterceptor.super.afterCompletion(request, response, handler, ex);
       }
   }
   ```

   3. 方法3：指定拦截内容

   ```xml
   <!--配置拦截器-->
   <mvc:interceptors>
       <!--单独设置拦截规则-->
       <mvc:interceptor>
           <!--/*表示上下文路径下的一层目录-->
           <!--/**表示上下文路径下的所有目录-->
           <mvc:mapping path="/**"/>
           <!--不包括-->
           <mvc:exclude-mapping path="/"/>
           <ref bean="firstInterceptor"/>
       </mvc:interceptor>
   </mvc:interceptors>
   ```

## 2.拦截器的三个抽象方法

- SpringMVC中的拦截器有三个抽象方法:

1. preHandle:控制器方法执行之前执行preHandle()，其boolean类型的返回值表示是否拦截或放行，返回true为放行，即调用控制器方法;返回false表示拦截，即不调用控制器方法
2. postHandle:控制器方法执行之后执行postHandle()
3. afterComplation:处理完视图和模型数据，渲染视图完毕之后执行afterComplation()

## 3.多个拦截器的执行顺序

1. 若每个拦截器的preHandle()都返回true。

   - 此时多个拦截器的执行顺序和拦截器在SpringMVC的配置文件的**配置顺序**有关:

   - preHandle()会按照配置的顺序执行，而postHandle()和afterComplation()会按照配置的**反序执行**

2. 若某个拦截器的preHandle()返回了false。

   - preHandle()返回false和它之前的拦截器的preHandle()都会执行，postHandle()都不执行，返回false的拦截器之前的拦截器的afterComplation()会执行

- 案例

```xml
<mvc:interceptors>
    <ref bean="firstInterceptor"/>
    <ref bean="secondInterceptor"/>
</mvc:interceptors>
```

执行顺序：

FirstInterceptor-->preHandle
SecondInterceptor-->preHandle
SecondInterceptor-->postHandle
FirstInterceptor-->postHandle
SecondInterceptor-->afterCompletion
FirstInterceptor-->afterCompletion

执行顺序：SecondInterceptor返回false

FirstInterceptor-->preHandle
SecondInterceptor-->preHandle
FirstInterceptor-->afterCompletion

# 十一.异常处理器

## 1.基于配置的异常处理

- SpringMVC提供了一个处理控制器方法执行过程中所出现的异常的接口:HandlerExceptionResolver接口

- HandlerExceptionResolver接囗的实现类有:DefaultHandlerExceptionResolver和SimpleMappingExceptionResolver

- SpringMVC提供了**自定义的异常处理器**SimpleMappingExceptionResolver，使用方式:

  1. 在springMVC中配置异常处理器：

  ```xml
  <!--配置异常处理-->
      <bean class="org.springframework.web.servlet.handler.SimpleMappingExceptionResolver">
          <property name="exceptionMappings">
              <props>
  <!--                properties的键表示处理器方法执行过程中出现的异常
  properties的值表示若出现指定异常时，设置一个新的视图名称，跳转到指定页面
  -->
                  <prop key="java.lang.ArithmeticException">error</prop>
              </props>
          </property>
  <!--        设置将异常信息共享在请求域中的键-->
          <property name="exceptionAttribute" value="ex"></property>
      </bean>
  ```

  2. 发送请求

  ```html
  <a th:href="@{/testExceptionHandler}">异常处理测试</a><br>
  ```

  3. 处理请求

  ```java
  @RequestMapping("/testExceptionHandler")
  public String testExceptionHandler() {
      System.out.println(1/0); // 产生异常-->异常处理器处理异常
      return "success";
  }
  ```

## 2.基于注解的异常处理

- 创建异常处理控制器@ControllerAdvice

```java
@ControllerAdvice
public class ExceptionController {
    @ExceptionHandler(value = {ArithmeticException.class, NullPointerException.class})
    public String testException(Exception ex, Model model) {
        model.addAttribute("ex", ex);
        return "error";
    }
}
```

- 转发/处理请求方式与前面一致

# 十二.注解配置SpringMVC

使用配置类和注解代替web.xml和SpringMVC配置文件的功能

## 1.创建初始化类，代替web.xml

- 在Servlet3.0环境中，容器会在类路径中査找实现javax.servlet.ServletContainerinitializer接口的类，如果找到的
  话就用它来配置Servlet容器。
- Spring提供了这个接口的实现，名为SpringServletContainerinitializer，这个类反过来又会查找实现WebApplicationlnitializer的类并将配置的任务交给它们来完成。
- Spring3.2引入了一个便利的WebApplicationlnitializer基础实现，名为AbstractAnnotationConfigDispatcherServletinitializer，当我们的类
  扩展了AbstractAnnotationConfigDispatcherServletinitializer并将其部署到Servlet3.0容器的时候，容器会自动
  发现它，并用它来配置Servlet上下文。



```java
// Web工程的初始化类，代替web.xml
public class WebInit extends AbstractAnnotationConfigDispatcherServletInitializer {
    /*
    指定spring的配置类
     */
    @Override
    protected Class<?>[] getRootConfigClasses() {
        return new Class[]{SpringConfig.class};
    }
    /*
        指定springMVC的配置类
         */
    @Override
    protected Class<?>[] getServletConfigClasses() {
        return new Class[]{WebConfig.class};
    }
    // 指定DispatcherServlet的路径 url-pattern
    @Override
    protected String[] getServletMappings() {
        return new String[]{"/"};
    }
// 配置过滤器
    @Override
    protected Filter[] getServletFilters() {
        CharacterEncodingFilter characterEncodingFilter = new CharacterEncodingFilter();
        characterEncodingFilter.setEncoding("UTF-8");
        characterEncodingFilter.setForceResponseEncoding(true);
        HiddenHttpMethodFilter hiddenHttpMethodFilter = new HiddenHttpMethodFilter();
        return new Filter[]{characterEncodingFilter, hiddenHttpMethodFilter};
    }
}
```

## 2.创建SpringConfig配置类，代替spring的配置文件

## 3.创建WebConfig配置类，代替SpringMVC的配置文件

```java
// 代替springMCV配置文件
package com.uestc.mvc.config;

import com.uestc.mvc.interceptor.TestInterceptor;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.context.ContextLoader;
import org.springframework.web.context.WebApplicationContext;
import org.springframework.web.multipart.MultipartResolver;
import org.springframework.web.multipart.commons.CommonsMultipartResolver;
import org.springframework.web.servlet.HandlerExceptionResolver;
import org.springframework.web.servlet.ViewResolver;
import org.springframework.web.servlet.config.annotation.*;
import org.springframework.web.servlet.handler.SimpleMappingExceptionResolver;
import org.thymeleaf.spring5.SpringTemplateEngine;
import org.thymeleaf.spring5.view.ThymeleafViewResolver;
import org.thymeleaf.templatemode.TemplateMode;
import org.thymeleaf.templateresolver.ITemplateResolver;
import org.thymeleaf.templateresolver.ServletContextTemplateResolver;

import java.util.List;
import java.util.Properties;

/* 代替SpringMVC配置文件
1.扫描组件 2.视图解析器 3.view-controller 4.default-servlet-handler
5.mvc注解驱动 6.文件上传解析器 7.异常处理  8.拦截器
 */
// 表示为配置类
@Configuration
// 1.扫描组件
@ComponentScan("com.uestc.mvc.Controller")
// 5.mvc注解驱动
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer { // WebMvcConfigurer 包含springMVC配置文件的相关设置

    // 4.default-servlet-handler
    @Override
    public void configureDefaultServletHandling(DefaultServletHandlerConfigurer configurer) {
        configurer.enable(); // 启用默认的servlet
    }

    // 8.拦截器
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        TestInterceptor testInterceptor = new TestInterceptor();
        // 设置拦截列表和不拦截的列表
        registry.addInterceptor(testInterceptor).addPathPatterns("/**");
    }

    // 3.view-controller
    @Override
    public void addViewControllers(ViewControllerRegistry registry) {
        registry.addViewController("/hello").setViewName("hello");
    }
    // 6.文件上传解析器
    @Bean
    public MultipartResolver multipartResolver() {
        CommonsMultipartResolver commonsMultipartResolver = new CommonsMultipartResolver();
        return commonsMultipartResolver;
    }
    // 7.异常处理
    @Override
    public void configureHandlerExceptionResolvers(List<HandlerExceptionResolver> resolvers) {
        SimpleMappingExceptionResolver exceptionResolver = new SimpleMappingExceptionResolver();
        Properties properties = new Properties();
        properties.setProperty("java.lang.ArithmeticException", "error");
        exceptionResolver.setExceptionMappings(properties);
        exceptionResolver.setExceptionAttribute("exception"); // 设置请求域中共享的异常的键
        resolvers.add(exceptionResolver);
    }

    // 2.配置视图解析器--创建顺序与springMVC.xml的Bean顺序相反
    // 配置生成模板解析器
    @Bean
    public ITemplateResolver templateResolver() {
        WebApplicationContext webApplicationContext = ContextLoader.getCurrentWebApplicationContext();
        ServletContextTemplateResolver templateResolver = new ServletContextTemplateResolver(
                webApplicationContext.getServletContext());
        templateResolver.setPrefix("/WEB-INF/templates/");
        templateResolver.setSuffix(".html");
        templateResolver.setCharacterEncoding("UTF-8");
        templateResolver.setTemplateMode(TemplateMode.HTML);
        return templateResolver;
    }
    // 生成模板引擎并为模板引擎注入模板解析器
    @Bean
    public SpringTemplateEngine templateEngine(ITemplateResolver templateResolver) { // IOC容器会自动装配
        SpringTemplateEngine templateEngine = new SpringTemplateEngine();
        templateEngine.setTemplateResolver(templateResolver);
        return templateEngine;
    }
    // 生成视图解析器并未解析器注入模板引擎
    @Bean
    public ViewResolver viewResolver(SpringTemplateEngine templateEngine) {
        ThymeleafViewResolver viewResolver = new ThymeleafViewResolver();
        viewResolver.setCharacterEncoding("UTF-8");
        viewResolver.setTemplateEngine(templateEngine);
        return viewResolver;
    }
}
```

# 十三.SpringMVC执行流程

## 1.SpringMVC常用组件

- DispatcherServlet:前端控制器，不需要工程师开发，由框架提供
  作用:统一处理请求和响应，整个流程控制的中心，由它调用其它组件处理用户的请求。
- HandlerMapping:处理器映射器：查找，不需要工程师开发，由框架提供
  作用:根据请求的ur、method等信息查找Handler/Controller，即控制器方法
- Handler/Controller:处理器@Controller，需要工程师开发
  作用:在DispatcherServlet的控制下Handler对具体的用户请求进行处理。
- HandlerAdapter:处理器适配器：执行，不需要工程师开发，由框架提供
  作用:通过HandlerAdapter对处理器(**控制器方法**)进行执行。
- ViewResolver:视图解析器，不需要工程师开发，由框架提供
  作用:进行视图解析，得到相应的视图，例如:ThymeleafView、InternalResourceView、RedirectView
- View:视图，不需要工程师开发，由框架或视图技术提供
  作用:将模型数据通过页面展示给用户

## 2.Dispatcherservlet初始化过程

DispatcherServlet 本质上是一个 Servlet，所以天然的遵循 Servlet 的生命周期。所以宏观上是 Servlet 生命周期来进行调度。

### a>初始化:WebApplicationContext

### b>创建:WebApplicationContext

### c>DispatcherServlet:初始化策略

- FrameworkServet创建WebApplicationContext后，刷新容器，调用onRefresh(wac)，此方法在DispatcherServlet中进行了重写，调用了initStrategies(context)方法，初始化策略，即初始化DispatcherServlet的各个组件
- 所在类:org.springframework.web.servlet.DispatcherServlet

```java
profected void initstrategies(Applicationcontext context) {
    initMultipartResolver(context);
    initLocaleResolver(context);
    initThemeResolver(context);
    initHandlerMappings(context);
    initHandlerAdapters(context);
    initHandlerExceptionResolvers(context);
    initRequestToViewNameTranslator(context);
    initViewResolvers(context);
    initFlashMapManager(context);
}
```

## 3.DispatcherServlet调用组件处理请求

### a>processRequest()

- FrameworkServlet重写HttpServlet中的service()和doXxx()，这些方法中调用了processRequest(request,
  response)
- 所在类:org.springframework.web.servlet.FrameworkServlet

### b>doService()

- processRequest()调用doService()
- 所在类:org.springframework.web.servlet.DispatcherServlet

### c>doDispatch()

- doService()调用doDispatch()
- 所在类:org.springframework.web.servlet.DispatcherServlet
- 关键点

1. mappedHandler调用链：
   - 包含handler、interceptorList、interceptorIndex
     hand1er:浏览器发送的请求所匹配的控制器方法
     interceptorList:处理控制器方法的所有拦截器集合
     interceptorIndex:拦截器索引，控制拦截器aftercompletion()的执行
2. 调用拦截器的preHandle()
3. ha.handle()由处理器适配器调用具体的控制器方法，最终获得ModelAndview对象
4. 调用拦截器的postHandle()
5. processDispatchResult()后续处理:处理模型数据和渲染视图

### d>processDispatchResult()

- doDispatch()调用processDispatchResult()

- 关键点

1. render():处理模型数据和渲染视图
2. mappedHandler.triggerAfterCompletion()调用拦截器的aftercompletion()

## 4.SpringMVC的执行流程

1. 用户向服务器发送请求，请求被SpringMVC 前端控制器 DispatcherServlet捕获

2) DispatcherServlet对请求URL进行解析，得到请求资源标识符(URI)，判断请求URI对应的映射:
   1. 不存在
      1. 再判断是否配置了mvc:defaut-servlet-handler
      2. 如果没配置，则控制台报映射查找不到，客户端展示404错误
      3. 如果有配置，则访问目标资源(一般为静态资源，如:JS,CSS,HTML)，找不到客户端也会展示404错误
   2. 存在
      1. 根据该URI，调用HandlerMapping获得该Handler配置的所有相关的对象(包括Handler对象以及Handler对象对应的拦截器)，最后以HandlerExecutionChain执行链对象的形式返回。
      2. DispatcherServlet 根据获得的Handler，选择一个合适的HandlerAdapter。
      3. 如果成功获得HandlerAdapter，此时将开始执行拦截器的preHandler(...)方法【正向】
      4. 提取Request中的模型数据，填充Handler入参，开始执行Handler(Controller)方法，处理请求。在填充Handler的入参过程中，根据你的配置，Spring将帮你做一些额外的工作:
         a.  HttpMessageConveter: 将请求消息(如|son、xml等数据)转换成一个对象，将对象转换为指定的响应信息
         b.数据转换:对请求消息进行数据转换。如String转换成Integer、Double等
         c.数据格式化:对请求消息进行数据格式化。如将字符串转换成格式化数字或格式化日期等
         d.数据验证: 验证数据的有效性(长度、格式等)，验证结果存储到BindingResult或Error中
      5. Handler执行完成后，向DispatcherServlet 返回-个ModelAndView对象。
      6. 此时将开始执行拦截器的postHandle(..)方法【逆向】
      7. 根据返回的ModelAndView(此时会判断是否存在异常:如果存在异常，则执行HandlerExceptionResolver进行异常处理)选择一个适合的ViewResolver进行视图解析，根据Model和View，来渲染视图，
      8. 渲染视图完毕执行拦截器的afterCompletion(...)方法【逆向】。
      9. 将渲染结果返回给客户端。
