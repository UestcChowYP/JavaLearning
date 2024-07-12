# Spring5 框架基本介绍

- 基本内容

1. Spring 概念
2. IOC容器
3. Aop
4. JdbcTemplate
5. 事务管理
6. Spring5 新特性

- Spring 框架概述

1. Spring 是轻量级的开源的 JavaEE 框架
2. Spring 可以解决企业应用开发的复杂性。
3. Spring有两个核心部分:IOC 和 Aop
   - IOC：控制反转，把创建对象过程交给 Spring进行管理
   - Aop：面向切面，不修改源代码进行功能增强
4. Spring的特点
   - 方便解耦，简化开发
   - Aop 编程支持
   - 方便程序测试.
   - 方便和其他框架进行整合
   - 方便进行事务操作。
   - 降低 API开发难度:

- 入门案例

![Spring框架结构](.\Spring框架markdown笔记图片\Spring框架结构.png)

1. 下载spring
2. 导入需要的jar包
   - 现阶段需要的：Beans/Core/Context/Expression
     - beans
     - context
     - core
     - expression
     - logging
3. 创建普通类
4. 创建 Spring 配置文件，在配置文件配置创建的对象
   - Spring 配置文件使用 xml格式
5. 代码测试
   - 加载 spring 配置文件
   - 获取配置创建的对象

# IoC介绍

- IoC介绍：(Inversion of Control，缩写为loC)

1. IoC底层原理
2. IoC接口(BeanFactory)
3. IoC操作 Bean 管理(基于 xml)
4. IoC操作 Bean 管理(基于注解)

- 什么是IoC

1. 控制反转，把对象创建和对象之间的调用过程，交给Spring 进行管理。
2. 使用 IOC 目的:为了耦合度降低。
3. 做入门案例就是 IOC实现。

- IOC底层原理：xml解析、工厂模式、反射

1. 使用工厂模式解耦合

![工厂模式](.\Spring框架markdown笔记图片\工厂模式.png)

2. xml解析、工厂模式、反射配合工作 -> 耦合度进一步降低

- IoC实现过程

1. xml配置文件，配置创建的对象

   ```xml
   <bean id="dao" class"com.uestc.UserDao"></bean>
   ```

2. 创建工厂类：包含service类和dao类

   ```java
   class UserFactory {
       public static UserDao getDao(){
               String classValue =class属性值;// xml解析
               Class clazz=Class.forName(classValue);//2 通过反射创建对象
           return(UserDao)clazz.newInstance();
       }
   }
   ```

- IoC接口

1. IOC思想基于 IOC容器完成，IOC容器底层就是对象工厂
2. Spring 提供 IOC容器实现两种方式：(两个接口)。
   - BeanFactory：IOC容器基本实现，是 Spring 内部的使用接口，不提供开发人员进行使用
     - 加载配置文件件时候不会创建对象，在获取对象(使用)才去创建对象
   - ApplicationContext：BeanFactory,接口的子接口，提供更多更强大的功能，一般由开发人员进行使用
     - 加载配置文件时候就会把在配置文件对象进行创建；服务器启动时完成。

3. ApplicationContext接口有实现类

- IoC操作：Bean 管理

1. 什么是 Bean 管理

   - Spring 创建对象
   - Spirng 注入属性

## Bean 管理操作有两种方式

- 基于 xml 配置文件方式实现

  - 1. 在 spring 配置文件中，使用 bean 标签添加对应属性实现对象创建

  - bean标签的属性

    - id属性：类的标识/别名
    - class属性：类的全路径
    - 创建对象时，默认执行**无参数构造方法**

  - 2. 基于 xml方式注入属性

    - **DI：依赖注入**，就是注入属性
      - set方法注入
      - 有参构造器注入 

    ```java
    ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
            Book book = context.getBean("book", Book.class);
            book.testDemo();
    ```

    ```xml
    <!-- set 方式 -> 无参构造器 -->
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.springframework.org/schema/beans
            http://www.springframework.org/schema/beans/spring-beans.xsd">
        <bean id="book" class="com.uestc.spring5.Book">
    <!--
        使用property完成属性注入
        name:类里面属性名称
        value:向属性注入的值
    -->
            <property name="bname" value="三国演义"></property>
            <property name="bauthor" value="罗贯中"></property>
        </bean>
    </beans>
    ```

    ```xml
    <!-- 有参构造器 -->
    <bean id="orders" class="com.uestc.spring5.Orders">
            <constructor-arg name="name" value="abc"></constructor-arg>
            <constructor-arg name="address" value="China"></constructor-arg>
        </bean>
    ```

  - 注入其他类型的属性

    1. 字面量：a.null值 b.属性值包含特殊符号

    ```xml
    <!-- null值 -->
    <property name="address">
        <null /> <!-- 设置空值 -->
    </property>
    <!--    特殊符号
            1.转义符号 &lt;&gt;
            2.特殊符号写到写到CDATA中
    -->
            <property name="address" value="&lt;&gt;+转义符号"></property>
    
            <property name="address">
                <value><![CDATA[<成><都>]]></value>
            </property>
    ```

    

- p名称空间注入(了解)：可以简化基于 xml 配置方式

  1. 在配置文件中，添加 p名称空间

     ```xml
     <beans xmlns="http://www.springframework.org/schema/beans"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xmlns:p="http://www.springframework.org/schema/p"  <!-- 1.添加p空间 -->
            xsi:schemaLocation="http://www.springframework.org/schema/beans
             http://www.springframework.org/schema/beans/spring-beans.xsd">
     <!-- 2.属性注入 -->
     	<bean id="book" class="com.uestc.spring5.Book" p:bname="西游记" p:bauthor="吴承恩"></bean>
     </beans>
     ```

  2. 在bean 标签内注入属性

     - 外部 bean：service层调用DAO层的过程，引入外部bean

       - 创建两个类 service 类和dao类

       - 在 service 调用dao里面的方法

         ```java
         public class UserService {
             private UserDao userDao;
             public void add() {
                 System.out.println("service add...");
                 userDao.updata();
         
             }
         
             public void setUserDao(UserDaoImpl userDao) {
                 this.userDao = userDao;
             }
         }
         ```

         ```java
         public interface UserDao {
             public void updata();
         }
         ```

         ```java
         public class UserDaoImpl implements UserDao {
             @Override
             public void updata() {
                 System.out.println("dao updata...");
             }
         }
         ```

         ```xml
         <beans xmlns="http://www.springframework.org/schema/beans"
                xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                xmlns:p="http://www.springframework.org/schema/p"
                xsi:schemaLocation="http://www.springframework.org/schema/beans
                 http://www.springframework.org/schema/beans/spring-beans.xsd">
         <!--  1service和dao对象创建  -->
             <bean id="userService" class="com.uestc.spring5.service.UserService">
         <!--    注入userDao对象
                 name属性:类里面属性名称
                 ref属性:创建userDao对象bean标签id值
              -->
                 <property name="userDao" ref="userDaoImpl"></property>
             </bean>
             <bean id="userDaoImpl" class="com.uestc.spring5.DAO.DaoImpl.UserDaoImpl"></bean>
         </beans>
         ```

         ```java
         public class testBean {
             @Test
             public void testAdd() {
                 ApplicationContext context = new ClassPathXmlApplicationContext("bean2.xml");
                 UserService userService = context.getBean("userService", UserService.class);
                 System.out.println(userService);
                 userService.add();
             }
         }
         ```

     - 内部 bean 

       - 一对多关系：部门和员工

       - 在实体类之间表示一对多关系，员工表示所属部门，使用对象类型属性进行表示

       - 在 spring 配置文件中进行配置

         ```java
         public class Dept {
             private String dname;
             public void setDname(String dname) {
                 this.dname = dname;
             }
             @Override
             public String toString() {
                 return "Dept{" +
                         "dname='" + dname + '\'' +
                         '}';
             }
         }
         ```

         ```java
         public class Emp {
             private String ename;
             private String gender;
             private Dept dept;
             public void setEname(String ename) {
                 this.ename = ename;
             }
             public void setGender(String gender) {
                 this.gender = gender;
             }
             public void setDept(Dept dept) {
                 this.dept = dept;
             }
             public void add() {
                 System.out.println(ename + "::::" + gender + "::::" + dept);
             }
         }
         ```

         ```xml
         <beans xmlns="http://www.springframework.org/schema/beans"
                xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                xsi:schemaLocation="http://www.springframework.org/schema/beans
                 http://www.springframework.org/schema/beans/spring-beans.xsd">
         <!-- 内部bean -->
             <bean id="emp" class="com.uestc.spring5.bean.Emp">
                 <property name="ename" value="Meez"></property>
                 <property name="gender" value="Man"></property>
                 <property name="dept">
                     <bean id="dept" class="com.uestc.spring5.bean.Dept">
                         <property name="dname" value="保安处"></property>
                     </bean>
                 </property>
             </bean>
         </beans>
         ```

         ```java
         @Test
         public void test2() {
             ApplicationContext context = new ClassPathXmlApplicationContext("bean3.xml");
             Emp emp = context.getBean("emp", Emp.class);
             System.out.println(emp);
             emp.add();
         }
         ```

       - 级联赋值

         ```xml
         <beans xmlns="http://www.springframework.org/schema/beans"
                xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                xsi:schemaLocation="http://www.springframework.org/schema/beans
                 http://www.springframework.org/schema/beans/spring-beans.xsd">
         <!--级联赋值-->
             <bean id="emp" class="com.uestc.spring5.bean.Emp">
                 <property name="ename" value="Meez"></property>
                 <property name="gender" value="Man"></property>
                 <property name="dept" ref="dept"></property>
             </bean>
             <bean id="dept" class="com.uestc.spring5.bean.Dept">
                 <property name="dname" value="财务部"></property>
             </bean>
         </beans>
         ```

         ```xml
         <beans xmlns="http://www.springframework.org/schema/beans"
                xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                xsi:schemaLocation="http://www.springframework.org/schema/beans
                 http://www.springframework.org/schema/beans/spring-beans.xsd">
         <!--级联赋值-->
             <bean id="emp" class="com.uestc.spring5.bean.Emp">
                 <property name="ename" value="Meez"></property>
                 <property name="gender" value="Man"></property>
                 <property name="dept" ref="dept"></property>
                 <property name="dept.dname" value="技术部"></property>
             </bean>
             <bean id="dept" class="com.uestc.spring5.bean.Dept">
                 <property name="dname" value="财务部"></property>
             </bean>
         </beans>
         ```

     - 注入集合属性

       - 注入数组类型属性
       - 注入 List 集合类型属性
       - 注入 Map 集合类型属性
       - 注入 Set 集合类型属性

       ```java
       public class Stu {
           private String[] courses;
           private List<String> list;
           private Map<String, String> map;
           private Set<String> set;
           public void setSet(Set<String> set) {
               this.set = set;
           }
           public void setCourses(String[] courses) {
               this.courses = courses;
           }
           public void setList(List<String> list) {
               this.list = list;
           }
           public void setMap(Map<String, String> map) {
               this.map = map;
           }
           public void test() {
               System.out.println(Arrays.toString(courses));
               System.out.println(list);
               System.out.println(map);
               System.out.println(set);
           }
       }
       ```

       ```xml
       <beans xmlns="http://www.springframework.org/schema/beans"
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xsi:schemaLocation="http://www.springframework.org/schema/beans
               http://www.springframework.org/schema/beans/spring-beans.xsd">
       <bean id="stu" class="com.uestc.spring5.collectionType.Stu">
           <property name="courses">
               <array>
                   <value>Java</value>
                   <value>数据库</value>
                   <value>算法</value>
               </array>
           </property>
           <property name="list">
               <list>
                   <value>Java</value>
                   <value>数据库</value>
               </list>
           </property>
           <property name="map">
               <map>
                   <entry key="key1" value="val1"></entry>
                   <entry key="key2" value="val2"></entry>
               </map>
           </property>
           <property name="set">
               <set>
                   <value>SQL</value>
                   <value>Mybatis</value>
               </set>
           </property>
       </bean>
       </beans>
       ```

       ```java
       @Test
       public void test3() {
           ApplicationContext context = new ClassPathXmlApplicationContext("bean5.xml");
           Stu stu = context.getBean("stu", Stu.class);
           System.out.println(stu);
           stu.test();
       }
       ```

     - 提取 集合 作为公共部分

       1. 在 spring 配置文件中引入名称空间 util

       ```xml
       <!--外部注入bean：引用类型-->
       <bean id="stu" class="com.uestc.spring5.collectionType.Stu">
           <property name="courseList">
               <list>
                   <ref bean="course1"></ref>
                   <ref bean="course2"></ref>
               </list>
           </property>
       </bean>
       <bean id="course1" class="com.uestc.spring5.collectionType.Course">
           <property name="cname" value="Spring5框架"></property>
       </bean>
       <bean id="course2" class="com.uestc.spring5.collectionType.Course">
           <property name="cname" value="Spring5框架"></property>
       </bean>
       ```

       ```java
       public class BookCur {
           private List<String> list;
           public void setList(List<String> list) {
               this.list = list;
           }
           public void test() {
               System.out.println(list);
           }
       }
       ```

       ```xml
       <!--1.在 spring 配置文件中引入名称空间 util-->
       <beans xmlns="http://www.springframework.org/schema/beans"
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xmlns:util="http://www.springframework.org/schema/util"
              xsi:schemaLocation="http://www.springframework.org/schema/beans
               http://www.springframework.org/schema/beans/spring-beans.xsd
               http://www.springframework.org/schema/util
               http://www.springframework.org/schema/util/spring-util.xsd">
       <!--2.使用 util 标签完成 list 集合注入提取-->
           <util:list id="bookList">
               <value>三国演义</value>
               <value>西游记</value>
               <value>水浒传</value>
           </util:list>
           <!--2.提取list集合类型属性注入使用-->
           <bean id="book" class="com.uestc.spring5.collectionType.BookCur">
               <property name="list" ref="bookList"></property>
           </bean>
       </beans>
       ```

       ```java
       @Test
       public void test4() {
           ApplicationContext context = new ClassPathXmlApplicationContext("bean7.xml");
           BookCur book = context.getBean("book", BookCur.class);
           System.out.println(book);
           book.test();
       }
       ```

       

- 基于注解方式实现：见后序内容



## Bean管理

1. Spring 有两种类型 bean，一种**普通 bean**，另外一种**工厂bean**(FactoryBean)
2. 普通 bean:在配置文件中定义 bean 类型就是返回类型
3. 工厂 bean:在配置文件定义 bean 类型可以和返回类型不一样 （配置文件定义的返回类型，和通过context获取的类型不一样）
   - 第一步 创建类，让这个类作为工厂 bean，实现接口 FactoryBean
   - 第二步 实现接口里面的方法，在实现的方法中定义返回的 bean 类型

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="MyBean" class="com.uestc.spring5.factoryBean.MyBean">
    </bean>
</beans>
```

```java
public class MyBean implements FactoryBean<Course> {
    @Override
    public boolean isSingleton() {
        return FactoryBean.super.isSingleton();
    }
    @Override
    public Course getObject() throws Exception {
        Course course = new Course();
        course.setCname("abc");
        return course;
    }
    @Override
    public Class<?> getObjectType() {
        return null;
    }
}
```

```java
@Test
public void test5() {
    ApplicationContext context = new ClassPathXmlApplicationContext("bean8.xml");
    Course course = context.getBean("MyBean", Course.class);
    System.out.println(course);
}
```

- bean的作用域

1. 在 Spring 里面，设置创建 bean 实例是单实例还是多实例？
2. 在 Spring 里面，默认情况下，bean 是单实例对象
3. 设置单实例/多实例：
   - bean的scope属性：scope="prototype"/"singleton"
   - 默认值，singleton，表示是单实例对象
   - prototype，表示是多实例对象
   - singleton 和 prototype 区别:
     - singleton：加载 spring 配置文件时候就会**创建单实例对象**
     - prototype：调用getBean方法的时候创建实例对象

## bean的生命周期

- bean的生命周期

1. 生命周期的基本概念：从对象创建到对象销毁的过程
2. bean的生命周期：
   - 通过构造器创建 bean 实例(无参数构造)
   - 为 bean 的属性设置值和对其他 bean 引用(调用 set方法)
   - 调用 bean 的初始化的方法(需要进行配置初始化的方法)
   - 使用bean (获取bean对象)
   - 当容器关闭时候，调用 bean 的销毁的方法(需要进行配置销毁的方法)

```java
public class OrdersCur {
    public OrdersCur() {
        System.out.println("step1:无参构造器");
    }
    private String name;
    public void setName(String name) {
        this.name = name;
        System.out.println("step2:set方法");
    }
    // 初始化方法
    public void initMethod() {
        System.out.println("step3:init方法");
    }
    // 销毁方法
    public void destroyMethod() {
        System.out.println("step5:destroy方法");
    }
}
```

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="orders" class="com.uestc.spring5.bean.OrdersCur" init-method="initMethod" destroy-method="destroyMethod">
        <property name="name" value="zzyp"></property>
    </bean>
</beans>
```

```java
@Test
public void test6() {
    ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("bean9.xml");
    OrdersCur order = context.getBean("orders", OrdersCur.class);
    System.out.println("strp4:获取对象-" + order);
    context.close(); // 执行销毁方法
}
```

- bean 的后置处理器

1. 通过构造器创建 bean 实例(无参数构造)
2. 为 bean 的属性设置值和对其他 bean 引用(调用 set方法)
3. bean 实例传递 bean 后置处理器的方法(初始化前)。
4. 调用 bean 的初始化的方法(需要进行配置初始化的方法)
5. 把 bean 实例传递 bean 后置处理器的方法(初始化后)。
6. 使用bean (获取bean对象)
7. 当容器关闭时候，调用 bean 的销毁的方法(需要进行配置销毁的方法)

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="orders" class="com.uestc.spring5.bean.OrdersCur" init-method="initMethod" destroy-method="destroyMethod">
        <property name="name" value="zzyp"></property>
    </bean>
<!--  配置后置处理器：配置文件会为所有bean添加后置处理器  -->
    <bean id="myBeanPost" class="com.uestc.spring5.bean.MyBeanPost"></bean>
</beans>
```

```java
public class MyBeanPost implements BeanPostProcessor {
    @Override
    public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("初始化前置处理器");
        return bean;
    }

    @Override
    public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("初始化后置处理器");
        return bean;
    }
}
```

```java
@Test
public void test6() {
    ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("bean9.xml");
    OrdersCur order = context.getBean("orders", OrdersCur.class);
    System.out.println("strp4:获取对象-" + order);
    context.close(); // 执行销毁方法
}
/*
输出：
step1:无参构造器
step2:set方法
初始化前置处理器
step3:init方法
初始化后置处理器
strp4:获取对象-com.uestc.spring5.bean.OrdersCur@23fe1d71
step5:destroy方法
*/
```

## xml方式

### 自动装配

- 基本概念：

1. 手动装配：在配置文件内手动为bean设置初始值
2. 自动装配：根据指定装配规则(属性名称或者属性类型)，Spring 自动将匹配的属性值进行注入。

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">
<!--自动装配
bean标签属性autowire，配置自动装配
autowire属性常用两个值:
byName根据属性名称注入，注入值bean的id值和类属性名称一样
byType根据属性类型注入，存在多个相同类型的值会报错
-->
    <bean id="emp" class="com.uestc.spring5.autowrite.Emp" autowire="byType">
<!--    手动装配    -->
<!--        <property name="dept" ref="dept"></property>-->
    </bean>
    <bean id="dept2" class="com.uestc.spring5.autowrite.Dept"></bean>
<!--    <bean id="dept1" class="com.uestc.spring5.autowrite.Dept"></bean>-->
</beans>
```

```java
public class Emp {
    private Dept dept;

    public void setDept(Dept dept) {
        this.dept = dept;
    }
    @Override
    public String toString() {
        return "Emp{" +
                "dept=" + dept +
                '}';
    }
    public void test() {
        System.out.println(dept);
    }
}
```

```java
public class Dept {
    @Override
    public String toString() {
        return "Dept{}";
    }
}
```

```java
@Test
public void test7() {
    ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("bean10.xml");
    Emp emp = context.getBean("emp", Emp.class);
    System.out.println(emp);
}
```

### 外部属性文件

- 操作外部属性文件

1. 直接配置数据库信息
   - 配置德鲁伊连接池
   - 引入德鲁伊连接池依赖 jar 包

```xml
<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="com.mysql.jdbc.Driver"></property>
        <property name="url" value="jdbc:mysql://localhost:3406/userDb"></property>
        <property name="username" value="root"></property>
        <property name="password" value="z123456"></property>
    </bean>
```

2. 引入外部属性文件配置数据库连接池

```pro
prop.username=root
prop.password=z123456
prop.url=jdbc:mysql://localhost:4306/userDb
prop.driverClassName=com.mysql.jdbc.Driver
prop.initialSize=5
prop.maxActive=10
```

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
">
<!--直接配置连接池-->
<!--    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">-->
<!--        <property name="driverClassName" value="com.mysql.jdbc.Driver"></property>-->
<!--        <property name="url" value="jdbc:mysql://localhost:3406/userDb"></property>-->
<!--        <property name="username" value="root"></property>-->
<!--        <property name="password" value="z123456"></property>-->
<!--    </bean>-->
<!--  引入外部属性文件  -->
    <context:property-placeholder location="classpath:jdbc.properties"/>
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="${prop.driverClassName}"></property>
        <property name="url" value="${prop.url}"></property>
        <property name="username" value="${prop.username}"></property>
        <property name="password" value="${prop.password}"></property>
    </bean>
</beans>
```

## 注解方式

- 注解

1. 注解是代码特殊标记，格式:@注解名称(属性名称=属性值,属性名称=属性值..)
2. 使用注解，注解作用在类上面，方法上面，属性上面
3. 使用注解目的：简化xml配置

- Spring 针对 **Bean 管理**中创建对象提供**注解**

1. @Component：普通组件
2. @Service：业务层组件
3. @Controller：web层组件
4. @Repository：持久层组件
5. 没有严格限制注解使用的位置，都可以用于创建对象实例

- 基于注解方式实现对象创建

1. 引入依赖：spring-aop-5.2.5.RELEASE.jar
2. 开启组件扫描
3. 创建类，在类上面添加创建对象注解

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
">
<!--开启组件扫描
1.如果扫描多个包，多个包使用逗号隔开
2.或者 写多个包的上层目录
-->
<!--    <context:component-scan base-package="com.uestc.spring5.DAO, com.uestc.spring5.service"></context:component-scan>-->
    <context:component-scan base-package="com.uestc"></context:component-scan>
</beans>
```

```java
@Component(value = "userService") // 相当于<bean id="userService" class="..." />
public class UserService3 {

    public void add() {
        System.out.println("service add...");
    }
}
```

```java
@Test
public void testService() {
    ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("bean31.xml");
    UserService3 userService = context.getBean("userService", UserService3.class);
    System.out.println(userService);
    userService.add();
}
```

- 开启组件扫描细节配置

```java
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
">
<!--示例1
use-default-filters="false”表示现在不使用默认filter，自己配置filter
context:include-filter，设置扫描哪些内容
-->
    <context:component-scan base-package="com.uestc" use-default-filters="false">
<!--   扫描 包含 带 Controller 注解的类    -->
        <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
    </context:component-scan>
    <!--示例2
context:exclude-filter，设置不扫描哪些内容
-->
    <context:component-scan base-package="com.uestc" use-default-filters="false">
        <!--   扫描 包含 带 Controller 注解的类    -->
        <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
    </context:component-scan>
</beans>
```

- 基于注解方式实现属性注入

1. @AutoWired：根据属性类型进行自动装配
   - 第一步：把 service 和 dao对象创建，在 service 和 dao类添加创建对象注解
   - 第二步：在 service 注入 dao对象，在 service 类添加 dao类型属性，在属性上面使用注解

```java
//在注解里面value属性值可以省略不写
//默认值是类名称，首字母小写
@Service // 相当于<bean id="userService" class="..." />
public class UserService3 {
    // 定义dao类型属性
    // 不需要添加set方法
    @Autowired
    private UserDao3 userDao;
    public void add() {
        System.out.println("service add...");
        userDao.add();
    }
}
```

```java
@Repository
public class UserDaoImpl3 implements UserDao3 {
    @Override
    public void add() {
        System.out.println("dao add ...");
    }
}
```

```java
@Test
public void testService2() {
    ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("bean31.xml");
    UserService3 userService = context.getBean("userService3", UserService3.class);
    System.out.println(userService);
    userService.add();
}
```

2. @Qualifier：根据属性名称进行注入
   - 这个@Qualifier注解的使用，和上面**@Autowired一起使用**

```java
@Service // 相当于<bean id="userService" class="..." />
public class UserService3 {
    // 定义dao类型属性
    // 不需要添加set方法
    @Autowired
    @Qualifier(value = "userDao2")
    private UserDao3 userDao;
    public void add() {
        System.out.println("service add...");
        userDao.add();
    }
}
```

```java
@Repository(value = "userDao2")
public class UserDaoImpl3 implements UserDao3 {
    @Override
    public void add() {
        System.out.println("dao add ...");
    }
}
```

3. @Resource：可以根据类型注入，可以根据名称注入

```java
//    @Resource // 根据类型注入
@Resource(name = "userDao2")
private UserDao3 userDao;
public void add() {
    System.out.println("service add...");
    userDao.add();
}
```

4. @Value：注入普通类型属性

```java
@Value(value = "abc")
private String name;
```

### 纯注解开发

- 完全注解开发/纯注解开发

1. 创建配置类，替代 xml 配置文件
2. 编写测试类

```java
package com.uestc.spring5.config;

import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration // 作为配置类，替代xml配置文件
@ComponentScan(basePackages = {"com.uestc"})
public class SpringConfig {
}
```

```java
@Test
public void testService3() {
    AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(SpringConfig.class);
    UserService3 userService = context.getBean("userService3", UserService3.class);
    System.out.println(userService);
    userService.add();
}
```

# AOP

- 基本概念：

1. 面向切面编程(方面)，利用 AOP 可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，同时提高了开发的效率。
2. 通俗描述：不通过修改源代码方式，在主干功能里面添加新功能。

![AOP_基本思路](.\Spring框架markdown笔记图片\AOP_基本思路.png)

- AOP底层原理：AOP 底层使用动态代理

1. 第一种 **有接口**情况，使用 JDK 动态代理

![AOP_有接口_JDK代理模式](.\Spring框架markdown笔记图片\AOP_有接口_JDK代理模式.png)

2. 第二种 **没有接口**情况，使用 CGLIB 动态代理

![AOP_无接口_CGLIB代理模式](.\Spring框架markdown笔记图片\AOP_无接口_CGLIB代理模式.png)

- AOP(JDK动态代理)

1. 使用 JDK动态代理，使用 Proxy 类里面的方法创建代理对象
   - java.lang.reflect.Proxy
   - 调用 newProxyInstance 方法：三个参数
     - 参数1：类加载器。
     - 参数2：增强方法所在的类，这个类实现的接口，支持多个接口
     - 参数3：实现这个接口 InvocationHandler，创建代理对象，写增强的方法
2. 代码实现
   - 创建接口，定义方法
   - 创建接口实现类，实现方法
   - 使用 Proxy 类创建接口代理对象

```java
public interface UserDao {
    public int add(int a, int b);
    public String update(String id);
}
```

```java
package com.uestc.spring5;

public class UserDaoImpl implements UserDao{
    @Override
    public int add(int a, int b) {
        System.out.println("add方法执行");
        return a+b;
    }
    @Override
    public String update(String id) {
        System.out.println("update方法执行");
        return id;
    }
}
```

```java
public class JDKProxy {
    public static void main(String[] args) {
        // 创建接口实现类代理对象
        Class[] interfaces = {UserDao.class};
        UserDaoImpl userDao = new UserDaoImpl();
        UserDao dao = (UserDao) Proxy.newProxyInstance(JDKProxy.class.getClassLoader(), interfaces, new UserDaoProsy(userDao));
        int res = dao.add(1, 2);
        System.out.println(res);
        String updateRes = dao.update("update方法参数");
        System.out.println(updateRes);
    }
}
class UserDaoProsy implements InvocationHandler {
    // 需要传入 代理对象的 类
    private Object obj;
    // 有参构造器创建
    public UserDaoProsy(Object obj) {
        this.obj = obj;
    }
    // 增强的业务逻辑
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        // 执行方法前
        System.out.println("方法执行前..." + method.getName() + "传递的参数" + Arrays.toString(args));
        // 需要增强的方法
        Object res = method.invoke(obj, args);
        // 执行方法后
        System.out.println("方法执行后..." + obj);
        return res;
    }
}
```

- AOP的常用术语

1. 连接点：类里面哪些方法可以被增强，这些方法称为连接点
2. 切入点：实际被真正增强的方法，称为切入点
3. 通知(增强)：
   - 实际增强/增加的逻辑部分称为通知(增强)
   - 通知有多种类型
     - 前置通知
     - 后置通知/返回通知
     - 环绕通知
     - 异常通知
     - 最终通知：类似finally
4. 切面：
   - 把通知应用到切入点过程

- AOP操作：准备工作

1. Spring 框架一般都是基于 AspectJ 实现 AOP 操作.
   - AspectJ不是 Spring 组成部分，是独立 AOP 框架，一般把 Aspect和 Spring框架一起使用，进行 AOP 操作。
2. 基于 AspectJ实现 AOP 操作
   - 基于 xml 配置文件
   - 基于注解方式实现(常用方法)
3. 在项目工程里面引入 AOP 相关依赖
4. 切入点表达式
   - 切入点表达式作用：知道对哪个类里面的哪个方法进行增强
   - 语法：execution( [ 权限修饰符 ] [ 返回类型 ] [ 类全路径] [ 方法名称 ] ( [ 参数列表 ] ))
   - 案例：
     - 对 com.uestc.dao.BookDao类里面的 add 进行增强。execution(*com.uestc.dao.BookDao.add(..)) *表示所有修饰符
     - 对 com.uestc.dao.BookDao类里面的 所有方法 进行增强。execution(*com.uestc.dao.BookDao. * (..)) 
     - 对 com.uestc.dao包里所有类里面的 所有方法 进行增强。execution(*com.uestc.dao. * . * (..)) 

## AOP操作(AspectJ注解)

- 1.创建类，在类里面定义方法
- 2.创建增强类(编写增强逻辑)、
  - 在增强类里面，创建方法，让不同方法代表不同通知类型

- 3.进行通知的配置

1. 在 spring 配置文件中，开启注解扫描

2. 使用注解创建 User 和 UserProxy 对象

3. 在增强类上面添加注解 @Aspect

   ```java
   @Component
   @Aspect // 生成代理对象
   public class UserProxy {
   ```

4. 在 spring 配置文件中开启生成代理对象

   ```java
   <!--开启Aspect生成代理象: 存在Aspect注解就生成代理对象-->
       <aop:aspectj-autoproxy></aop:aspectj-autoproxy>
   ```

- 4.配置不同类型的通知

1. 在增强类的里面，在作为通知方法上面添加通知类型注解，使用切入点表达式配置

```java
@Component
public class User {
    public void add() {
//        int i = 1/0;
        System.out.println("add...");
    }
}
```

```java
@Component
@Aspect // 生成代理对象
public class UserProxy {
    //前置通知
    //@Before注解表示作为前置通知
    @Before(value = "execution(* com.uestc.spring5.aopanno.User.add(..))")
    public void before() {
        System.out.println("before...");
    }
    @After(value = "execution(* com.uestc.spring5.aopanno.User.add(..))")
    // 最终通知
    public void after() {
        System.out.println("after...再增强方法执行后执行");
    }
    @AfterReturning(value = "execution(* com.uestc.spring5.aopanno.User.add(..))")
    // 后置通知/返回通知
    public void afterReturning() {
        System.out.println("afterReturning...再增强方法返回值之后执行");
    }
    // 异常通知
    @AfterThrowing(value = "execution(* com.uestc.spring5.aopanno.User.add(..))")
    public void afterThrowing() {
        System.out.println("afterThrowing...异常通知");
    }
    @Around(value = "execution(* com.uestc.spring5.aopanno.User.add(..))")
    public void around(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {
        System.out.println("环绕之前...");
        proceedingJoinPoint.proceed();
        System.out.println("环绕之后...");
    }
}
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd
">
<!--  开启注解扫描  -->
<context:component-scan base-package="com.uestc.spring5.aopanno"></context:component-scan>
<!--开启Aspect生成代理象: 存在Aspect注解就生成代理对象-->
    <aop:aspectj-autoproxy></aop:aspectj-autoproxy>
</beans>
```

- 5.提取公共切入点表达式

```java
// 相同切入点
@Pointcut(value = "execution(* com.uestc.spring5.aopanno.User.add(..))")
public void pointDemo(){

}
//前置通知
//@Before注解表示作为前置通知
@Before(value = "pointDemo()")
public void before() {
    System.out.println("before...");
}
```

- 6.设置增强类优先级，有多个增强类多同一个方法进行增强时
  - @Order(1)数字小的优先执行

```java
@Component
@Aspect // 生成代理对象
@Order(1)
public class UserProxy {}
```

```java
@Component
@Aspect
@Order(2)
public class PersonProxy {}
```

- 7.完全注解开发

```java
// 注解类
@Configuration
@ComponentScan(basePackages = {"com.uestc"})
@EnableAspectJAutoProxy(proxyTargetClass = true) // 默认false
public class ConfigAop {
}
```

```java
@Test
public void testAopAllAnno() {
    AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(ConfigAop.class);
    User user = context.getBean("user", User.class);
    user.add();
}
```



## AOP操作(AspectJ配置文件)

- 1.创建两个类，增强类和被增强类，创建方法
- 2.在 spring 配置文件中创建两个类对象

```xml
<!--  创建对象  -->
    <bean id="book" class="com.uestc.spring5.aopxml.Book"></bean>
    <bean id="bookProxy" class="com.uestc.spring5.aopxml.BookProxy"></bean>
```

- 3.在 spring 配置文件中配置切入点

```java
public class Book {
    public void buy() {
        System.out.println("buy...");
    }
}
```

```java
public class BookProxy {
    public void before() {
        System.out.println("before...");
    }
}
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd
">
<!--  创建对象  -->
    <bean id="book" class="com.uestc.spring5.aopxml.Book"></bean>
    <bean id="bookProxy" class="com.uestc.spring5.aopxml.BookProxy"></bean>
    <!--  配置增强  -->
    <aop:config>
        <aop:pointcut id="p" expression="execution(* com.uestc.spring5.aopxml.Book.buy(..))"/>
<!--    配置切面    -->
        <aop:aspect ref="bookProxy">
<!--     增强作用在具体的方法上
       aop:before 前置通知
       method 指定增强方法
       pointcut-ref 指定切入点表达式
       -->
        <aop:before method="before" pointcut-ref="p"/>
        </aop:aspect>
    </aop:config>
</beans>
```

```java
@Test
public void testAopXml() {
    ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("bean2.xml");
    Book book = context.getBean("book", Book.class);
    book .buy();
}
```

# JdbcTemplate

- 基本概念

1. 什么是JdbcTemplate.

   - Spring 框架对 JDBC 进行封装，使用 jdbcTemplate,方便实现对数据库操作

2. 准备工作

   - 引入相关的jar包

     - druid-1.1.10.jar
     - mysql-connector-java-5.1.37.jar
     - spring-tx-5.2.5.RELEASE.jar
     - spring-orm-5.2.5.RELEASE.jar
     - spring-jdbc-5.2.5.RELEASE.jar

   - 在 spring 配置文件配置数据库连接池

     ```xml
     <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource" destroy-method="close">
         <property name="driverClassName" value="com.mysql.jdbc.Driver"></property>
         <property name="url" value="jdbc:mysql://localhost:3406/user_db"></property>
         <property name="username" value="root"></property>
         <property name="password" value="z123456"></property>
     </bean>
     ```

   - 配置 JdbcTemplate 对象，注入 DataSource

     ```xml
     <!-- JdbcTemplate对象   -->
     <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
         <!--    注入dataSource：set方法注入    -->
         <property name="dataSource" ref="dataSource"></property>
     </bean>
     ```

   - 创建 service 类，创建 dao 类，在 dao注入jdbcTemplate 对象

     ```xml
     <!--  开启扫描  -->
         <context:component-scan base-package="com.uestc"></context:component-scan>
     ```

     

- JdbcTemplate操作数据库：添加

1. 对应数据库创建实体类

```java
package com.uestc.spring5.entity;

public class Book {
    private String Id;
    private String name;
    private String ustatus;
    public Book() {
    }
    public Book(String id, String name, String ustatus) {
        Id = id;
        this.name = name;
        this.ustatus = ustatus;
    }
    public String getId() {
        return Id;
    }
    public void setId(String id) {
        Id = id;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public String getUstatus() {
        return ustatus;
    }
    public void setUstatus(String ustatus) {
        this.ustatus = ustatus;
    }
}
```

2. 编写 service 和 dao:

   - 在 dao 进行数据库添加操作

   - 调用 JdbcTemplate 对象里面 update 方法实现添加操作
     - 第一个参数：sql语句
     - 第二个参数：可变参数，设置 sql语句值

```java
@Service
public class BookService {
    @Autowired
    private BookDao bookDao;
    // 添加
    public void addBook(Book book){
        bookDao.add(book);
    }
}
```

```java
public interface BookDao {
    public void add(Book book);
}
```

```java
@Repository
public class BookDaoImpl implements BookDao{
    // 注入JdbcTemplate
    @Autowired
    private JdbcTemplate jdbcTemplate;

    @Override
    public void add(Book book) {
        // 1.sql语句
        String sql = "insert into t_book values(?,?,?)";
        int update = jdbcTemplate.update(sql, book.getId(), book.getName(), book.getUstatus());
        System.out.println(update);
    }
}
```

```java
@Test
public void testJdbcTemplate(){
    ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
    BookService bookService = context.getBean("bookService", BookService.class);
    Book book = new Book("1", "java", "abc");
    bookService.addBook(book);
}
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd
">
<!--  开启扫描  -->
    <context:component-scan base-package="com.uestc"></context:component-scan>
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource" destroy-method="close">
        <property name="driverClassName" value="com.mysql.jdbc.Driver" />
        <property name="url" value="jdbc:mysql://localhost:4306/user_db?useSSL=false"/>
        <property name="username" value="root" />
        <property name="password" value="z123456" />
    </bean>
<!-- JdbcTemplate对象   -->
    <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
<!--    注入dataSource：set方法注入    -->
        <property name="dataSource" ref="dataSource" />
    </bean>
</beans>
```

- JdbcTemplate操作数据库：修改/删除

```java
@Test
public void testJdbcTemplateUpdate(){
    ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
    BookService bookService = context.getBean("bookService", BookService.class);
    Book book = new Book("1", "数据结构", "abc数据结构");
    bookService.update(book);
}
@Test
public void testJdbcTemplateDelete(){
    ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
    BookService bookService = context.getBean("bookService", BookService.class);
    Book book = new Book("1", "数据结构", "abc数据结构");
    bookService.delete(book);
}
```

- JdbcTemplate操作数据库：查询

1. 查询返回某个值(查询记录条目数)
   - queryForObject(String sql, Class< T > requiredType) 参数列表(sql语句, 返回类型的class)

```java
@Override
public int queryCount() {
    String sql = "SELECT COUNT(*) FROM t_book";
    int count = jdbcTemplate.queryForObject(sql, Integer.class);
    return count;
}
```

2. 查询返回对象
   - queryForObject(String sql, RowMapper< T >rowMapper, Object... args) 参数列表(sql语句, rowMapper,  sql语句的值)
   - rowMapper：是接口，返回不同类型数据，使用这个接口里面实现类完成数据封装

3. 查询返回集合
   - query(String sql, RowMapper< T >rowMapper, Object...args) 参数列表(sql语句, rowMapper,  sql语句的值)

- JdbcTemplate操作数据库：批量操作

1. 批量操作:操作表里面多条记录
2. JdbcTemplate 实现批量添加操作
   - batchUpdate(String sql, List<0bject]> batchArgs) 参数列表(sql语句, batchArgs)
   - batchArgs：List 集合，添加多条记录数据
3. JdbcTemplate 实现批量修改操作
4. JdbcTemplate 实现批量删除操作



- 演示案例

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd
">
<!--  开启扫描  -->
    <context:component-scan base-package="com.uestc"></context:component-scan>
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource" destroy-method="close">
        <property name="driverClassName" value="com.mysql.jdbc.Driver" />
        <property name="url" value="jdbc:mysql://localhost:4306/user_db?useSSL=false"/>
        <property name="username" value="root" />
        <property name="password" value="z123456" />
    </bean>
<!-- JdbcTemplate对象   -->
    <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
<!--    注入dataSource：set方法注入    -->
        <property name="dataSource" ref="dataSource" />
    </bean>
</beans>
```

```java
package com.uestc.spring5.service;

import com.uestc.spring5.dao.BookDao;
import com.uestc.spring5.entity.Book;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class BookService {
    @Autowired
    private BookDao bookDao;
    // 添加
    public void addBook(Book book){
        bookDao.add(book);
    }
    public void update(Book book){
        bookDao.update(book);
    }
    public void delete(Book book){
        bookDao.delete(book);
    }
    public int queryCount() {
        return bookDao.queryCount();
    }
    public Book queryOneById(String id) {
        return bookDao.queryOneById(id);
    }
    public List<Book> queryAll() {
        return bookDao.queryAll();
    }
    public void batchAdd(List<Object[]> batchArgs) {
        bookDao.batchAdd(batchArgs);
    }
    public void batchUpdate(List<Object[]> batchArgs) {
        bookDao.batchUpdate(batchArgs);
    }
    public void batchDelete(List<Object[]> batchArgs) {
        bookDao.batchDelete(batchArgs);
    }
}
```

```java
package com.uestc.spring5.dao;

import com.uestc.spring5.entity.Book;

import java.util.List;

public interface BookDao {
    public void add(Book book);
    public void update(Book book);
    public void delete(Book book);

    public int queryCount();

    Book queryOneById(String id);

    List<Book> queryAll();

    void batchAdd(List<Object[]> batchArgs);

    void batchUpdate(List<Object[]> batchArgs);

    void batchDelete(List<Object[]> batchArgs);
}
```

```java
package com.uestc.spring5.dao;

import com.uestc.spring5.entity.Book;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.BeanPropertyRowMapper;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.stereotype.Repository;

import java.util.Arrays;
import java.util.List;

@Repository
public class BookDaoImpl implements BookDao{
    // 注入JdbcTemplate
    @Autowired
    private JdbcTemplate jdbcTemplate;

    @Override
    public void add(Book book) {
        // 1.sql语句
        String sql = "insert into t_book values(?,?,?)";
        int update = jdbcTemplate.update(sql, book.getId(), book.getName(), book.getUstatus());
        System.out.println(update);
    }

    @Override
    public void update(Book book) {
        String sql = "update t_book set name=?, ustatus=? where id=?";
        int update = jdbcTemplate.update(sql, book.getName(), book.getUstatus(), book.getId());
        System.out.println(update);
    }

    @Override
    public void delete(Book book) {
        String sql = "delete from t_book where id=?";
        int update = jdbcTemplate.update(sql, book.getId());
        System.out.println(update);
    }

    @Override
    public int queryCount() {
        String sql = "SELECT COUNT(*) FROM t_book";
        int count = jdbcTemplate.queryForObject(sql, Integer.class);
        return count;
    }

    @Override
    public Book queryOneById(String id) {
        String sql = "SELECT * FROM t_book where id=?";
        Book book = jdbcTemplate.queryForObject(sql, new BeanPropertyRowMapper<Book>(Book.class), id);
        return book;
    }

    @Override
    public List<Book> queryAll() {
        String sql = "SELECT * FROM t_book";
        List<Book> books = jdbcTemplate.query(sql, new BeanPropertyRowMapper<Book>(Book.class));
        return books;
    }

    @Override
    public void batchAdd(List<Object[]> batchArgs) {
        String sql = "insert into t_book values(?,?,?)";
        int[] add = jdbcTemplate.batchUpdate(sql, batchArgs);
        System.out.println(Arrays.toString(add));
    }

    @Override
    public void batchUpdate(List<Object[]> batchArgs) {
        String sql = "update t_book set name=?, ustatus=? where id=?";
        int[] update = jdbcTemplate.batchUpdate(sql, batchArgs);
        System.out.println(Arrays.toString(update));
    }

    @Override
    public void batchDelete(List<Object[]> batchArgs) {
        String sql = "delete from t_book where id=?";
        int[] delete = jdbcTemplate.batchUpdate(sql, batchArgs);
        System.out.println(Arrays.toString(delete));
    }
}
```

```java
package com.uestc.spring5.test;

import com.uestc.spring5.entity.Book;
import com.uestc.spring5.service.BookService;
import org.junit.Test;
import org.springframework.context.support.ClassPathXmlApplicationContext;

import java.util.ArrayList;
import java.util.List;

public class testBook {
    @Test
    public void testJdbcTemplateAdd(){
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
        BookService bookService = context.getBean("bookService", BookService.class);
        Book book = new Book("1", "java", "abc");
//        Book book = new Book("2", "数据结构", "abc数据结构");
        bookService.addBook(book);
    }
    @Test
    public void testJdbcTemplateUpdate(){
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
        BookService bookService = context.getBean("bookService", BookService.class);
        Book book = new Book("1", "数据结构", "abc数据结构");
        bookService.update(book);
    }
    @Test
    public void testJdbcTemplateDelete(){
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
        BookService bookService = context.getBean("bookService", BookService.class);
        Book book = new Book("1", "数据结构", "abc数据结构");
        bookService.delete(book);
    }
    @Test
    public void testJdbcTemplateQueryForInt(){
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
        BookService bookService = context.getBean("bookService", BookService.class);
        int count = bookService.queryCount();
        System.out.println(count);
    }
    @Test
    public void testJdbcTemplateQueryOneById(){
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
        BookService bookService = context.getBean("bookService", BookService.class);
        Book book = bookService.queryOneById("1");
        System.out.println(book);
    }
    @Test
    public void testJdbcTemplateQueryAll(){
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
        BookService bookService = context.getBean("bookService", BookService.class);
        List<Book> books = bookService.queryAll();
        for (Book book: books) {
            System.out.println(book);
        }
    }
    @Test
    public void testJdbcTemplateBatchAdd(){
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
        BookService bookService = context.getBean("bookService", BookService.class);
        List<Object[]> books = new ArrayList<>();
        Object[] o1 = {"31", "Java31", "Java3Status1"};
        Object[] o2 = {"41", "Java41", "Java4Status1"};
        Object[] o3 = {"51", "Java51", "Java5Status1"};
        books.add(o1);
        books.add(o2);
        books.add(o3);
        bookService.batchAdd(books);
    }
    @Test
    public void testJdbcTemplateBatchUpdate(){
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
        BookService bookService = context.getBean("bookService", BookService.class);
        List<Object[]> books = new ArrayList<>();
        // 注意参数输入的顺序
        Object[] o1 = {"Java311", "Java3Status11", "3"};
        Object[] o2 = {"Java411", "Java4Status11", "4"};
        Object[] o3 = {"Java511", "Java5Status11", "5"};
        books.add(o1);
        books.add(o2);
        books.add(o3);
        bookService.batchUpdate(books);
    }
    @Test
    public void testJdbcTemplateBatchDelete(){
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
        BookService bookService = context.getBean("bookService", BookService.class);
        List<Object[]> books = new ArrayList<>();
        // 注意参数输入的顺序
        Object[] o1 = {"3"};
        Object[] o2 = {"4"};
        Object[] o3 = {"5"};
        books.add(o1);
        books.add(o2);
        books.add(o3);
        bookService.batchDelete(books);
    }
}
```

```java
package com.uestc.spring5.entity;

public class Book {
    private String Id;
    private String name;
    private String ustatus;

    public Book() {
    }

    public Book(String id, String name, String ustatus) {
        Id = id;
        this.name = name;
        this.ustatus = ustatus;
    }

    public String getId() {
        return Id;
    }

    public void setId(String id) {
        Id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getUstatus() {
        return ustatus;
    }

    public void setUstatus(String ustatus) {
        this.ustatus = ustatus;
    }

    @Override
    public String toString() {
        return "Book{" +
                "Id='" + Id + '\'' +
                ", name='" + name + '\'' +
                ", ustatus='" + ustatus + '\'' +
                '}';
    }
}
```

# 事务

- 基本概念

1. 事务是数据库操作最基本单元，逻辑上一组操作，要么都成功，如果有一个失败所有操作都失败。
2. 事务四个特性(ACID特性)
   - 原子性：不可分割
   - 一致性：总量不变
   - 隔离性：多事务操作互不影响
   - 持久性：提交事务，数据库内容发生改变

- 转账事务演示

![事务_转账](.\Spring框架markdown笔记图片\事务_转账.png)

1. 创建数据库

```mysql
CREATE TABLE `t_account`(
`id` BIGINT(20) PRIMARY KEY,
`username` VARCHAR(50),
`money` INT
);
```

2. 创建 service，搭建 dao，完成对象创建和注入

   - service注入dao，在dao注入JdbcTemplate，在JdbcTemlate注入 DataSource

     ```java
     @Repository
     public class UserDaoImpl implements UserDao{
         @Autowired
         private JdbcTemplate jdbcTemplate;
     }
     ```

     ```java
     @Service
     public class UserService {
         @Autowired
         private UserDao userDao;
     }
     ```

3. 在 dao创建两个方法:多钱和少钱的方法，在service 创建方法(转账的方法)

## Spring事务管理介绍

1. 事务添加到 JavaEE 三层结构里面 **Service 层**(业务逻辑层)
2. 在 Spring 进行事务管理操作
   - 有两种方式:编程式事务管理和**声明式事务管理(使用)**
3. 声明式事务管理
   - **基于注解方式**
   - 基于 xml 配置文件方式
4. 在 Spring 进行声明式事务管理，底层使用 AOP 原理
5. Spring 事务管理 API
   - 提供一个接口，代表事务管理器，这个接口针对不同的框架提供不同的实现类
   - PlatformTransactionManager 接口
   - DataSourceTransactionManager JDBC模板的管理类

- 注解声明式事务管理

1. 在 spring 配置文件配置事务管理器

   ```java
   <!--  创建事务管理器  -->
       <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
           <property name="dataSource" ref="dataSource"></property>
   	</bean>
   ```

2. 在 spring 配置文件，开启事务注解

   ```java
   <!--  开启事务注解  -->
       <tx:annotation-driven transaction-manager="transactionManager"></tx:annotation-driven>
   ```

3. 在 service 类上面(获取 service 类里面方法上面)添加事务注解
   - @Transactional，这个注解添加到类上面，也可以添加方法上面
   - 如果把这个注解添加类上面，这个类里面所有的方法都添加事务，
   - 如果把这个注解添加方法上面，为这个方法添加事务

## 参数：声明式事务管理参数配置

1. propagation：事务传播行为，当一个事务方法被另外一个事务方法调用时候，这个事务方法如何进行

   <img src=".\Spring框架markdown笔记图片\事务_传播行为1.png" alt="事务_传播行为1" style="zoom: 67%;" />

   - REQUIRED:

     <img src=".\Spring框架markdown笔记图片\事务_required.png" alt="事务_required" style="zoom: 67%;" />

   - REQUIRED_NEW:

     ![事务_required_new](.\Spring框架markdown笔记图片\事务_required_new.png)

   - SUPPORTS:

![事务_supports](.\Spring框架markdown笔记图片\事务_supports.png)

## 参数：事务隔离级别

- 事务隔离级别

1. 事务有特性成为隔离性，多事务操作之间不会产生影响。不考虑隔离性产生很多问题
2. 有三个读问题：脏读、不可重复读、虚(幻)读
   - 脏读：一个未提交事务读取到另一个未提交事务的数据
   - 不可重复读：一个未提交事务读取到另一个已经提交事务的数据
   - 虚读/幻读：一个未提交事务读取到另一提交事务添加数据
3. 通过设置事务隔离性，解决读问题

![事务_隔离级别](.\Spring框架markdown笔记图片\事务_隔离级别.png)

## 其他参数：

- timeout：超时时间

1. 事务需要在一定时间内进行提交，如果不提交进行回滚
2. 默认值是-1(没有超时时间)，设置时间以秒为单位进行计算

- readOnly:是否只读

1. 读:查询操作，写:添加修改删除操作
2. readOnly 默认值 false，表示可以查询，可以添加修改删除操作
3. 设置 readOnly 值是true，设置成 true 之后，只能查询

- rolbackFor:回滚

1. 设置出现哪些异常进行事务回滚

- noRollbackFor:不回滚

1. 设置出现哪些异常不进行事务回滚

```java
// 注解形式的声明式事务管理
```

##  xml 配置形式事务管理

-  xml 配置形式事务管理

1. 在 spring 配置文件中进行配置：
   - 第一步 配置事务管理器
   - 第二步 配置通知(通知：程序增强的部分)
   - 第三步 配置切入点和切面

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd
       http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd
">
<!--  开启扫描  -->
    <context:component-scan base-package="com.uestc"></context:component-scan>
<!--  数据库连接池  -->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource" destroy-method="close">
        <property name="driverClassName" value="com.mysql.jdbc.Driver" />
        <property name="url" value="jdbc:mysql://localhost:4306/user_db?useSSL=false"/>
        <property name="username" value="root" />
        <property name="password" value="z123456" />
    </bean>
<!-- JdbcTemplate对象   -->
    <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
<!--    注入dataSource：set方法注入    -->
        <property name="dataSource" ref="dataSource" />
    </bean>
<!--  1 创建事务管理器  -->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"></property>
    </bean>
<!--  2 配置通知：配置事务  -->
    <tx:advice id="txdvice">
<!--   配置事务参数     -->
        <tx:attributes>
<!--            指定哪种规则的方法上面添加事务-->
            <tx:method name="accountMoney" propagation="REQUIRED"/>
            <tx:method name="account*"/><!--account开头的所有方法添加事务-->

        </tx:attributes>
    </tx:advice>
    <!--3 配置切入点和切面-->
    <aop:config>
<!--    配置切入点    -->
        <aop:pointcut id="pt" expression="execution(* com.uestc.spring5.service.UserService.*(..))"/>
<!--    配置切面    -->
        <aop:advisor advice-ref="txdvice" pointcut-ref="pt"/>
    </aop:config>
</beans>
```

## 完全注解开发

- 写配置类

```java
package com.uestc.spring5.Config;

import com.alibaba.druid.pool.DruidDataSource;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.jdbc.datasource.DataSourceTransactionManager;
import org.springframework.transaction.annotation.EnableTransactionManagement;

import javax.sql.DataSource;

@Configuration // 配置类
@ComponentScan(basePackages = "com.uestc") // 开启组件扫描
@EnableTransactionManagement // 开启事务
public class TxConfige {
    // 创数据库连接池
    @Bean
    public DruidDataSource getDruidDataSource(){
        DruidDataSource dataSource = new DruidDataSource();
        dataSource.setDriverClassName("com.mysql.jdbc.Driver");
        dataSource.setUrl("jdbc:mysql://localhost:4306/user_db?useSSL=false");
        dataSource.setUsername("root");
        dataSource.setPassword("z123456");
        return dataSource;
    }
    @Bean
    public JdbcTemplate getJdbcTemplate(DataSource dataSource) {
        JdbcTemplate jdbcTemplate = new JdbcTemplate();
        // IOC容器中已经存在dataSource 可以直接注入，不用get方法获取
//        jdbcTemplate.setDataSource(getDruidDataSource());
        jdbcTemplate.setDataSource(dataSource);
        return jdbcTemplate;
    }
    // 创建事务管理器
    @Bean
    public DataSourceTransactionManager getDataSourceTransactionManager(DataSource dataSource) {
        DataSourceTransactionManager transactionManager = new DataSourceTransactionManager();
        transactionManager.setDataSource(dataSource);
        return transactionManager;
    }
}
```

# Spring5 框架新功能

- 基本介绍

1. 整个 Spring5 框架的代码基于 Java8，运行时兼容 JDK9，许多不建议使用的类和方法在代码库中删除
2. Spring5.0 框架自带了通用的日志封装
   - Spring5 框架整合 Log4j2
   - Spring5 已经移除 Log4jConfigListener，官方建议使用 Log4j2

- Log4j2的使用

1. 引入jar 包
   - log4j-api-2.11.2jar
   - log4j-core-2.11.2jar
   - log4j-slf4j-impl-2.11.2jar
   - slf4j-api-1.7.30jar

2. 创建 log4j2.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!--日志级别以及优先级排序:OFF > FATAL > ERROR > WARN >INFO > DEBUG > TRACE > ALL-->
<Configuration status="info">
    <Appenders>
        <Console name="Console" target="SYSTEM_OUT">
            <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
        </Console>
    </Appenders>
    <Loggers>
        <Root level="info">
            <AppenderRef ref="Console"/>
        </Root>
    </Loggers>
</Configuration>
```

```java
package com.uestc.spring5.test;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
public class UserLog {
    private static final Logger log = LoggerFactory.getLogger(Object.class);

    public static void main(String[] args) {
        log.info("hello log4j2");
        log.warn("hello log4j2");
        System.out.println("!");
    }
}
```



## Spring5 框架核心容器

- 支持@Nullable 注解

1. @Nullabje注解可以使用在**方法**/**属性**/**参数**上面，表示方法返回可以为空，属性值可以为空，参数值可以为空。

- 支持函数式风格(lambda表达式)

0. 手动new的对象无法受到IoC容器的管理，为了解决该问题
1. 函数式风格创建对象，交给spring进行管理

- 测试：Spring5 支持整合 JUnit4

1. 引入jar包
   - spring-test-5.2.5.RELEASE
2. 创建测试类使用注解方式完成

```java
@RunWith(SpringJUnit4ClassRunner.class) // 指定测试框架的版本
// 加载配置文件：相当于 ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
@ContextConfiguration("classpath:bean2.xml") //
public class Jtest {
    @Autowired
    private UserService userService; // 自动注入
    @Test // Juint4
    public void test() {
        userService.accountMoney();
    }
}
```

- 测试：Spring5 支持整合 JUnit5

```java
// 1.普通注解
//@ExtendWith(SpringExtension.class)
//@ContextConfiguration("classpath:bean2.xml")
// 2.复合注解-简化普通注解
@SpringJUnitConfig(locations = "classpath:bean2.xml")
public class Jtest {
    @Autowired
    private UserService userService; // 自动注入
    @Test
    public void test() {
        userService.accountMoney();
    }
}
```

## SpringWebFlux

- 基本介绍

![spring5_新功能_webflux](.\Spring框架markdown笔记图片\spring5_新功能_webflux.png)

1. 是 Spring5 添加新的模块，用于 web 开发的，功能和SpringMVC类似的，Webflux使用当前一种比较流程响应式编程出现的框架。
2. 使用传统 web 框架，比如 SpringMVC，这些基于 Servlet容器，Webflux是一种异步非阻塞的框架，异步非阻塞的框架在 Servlet3.1 以后才支持，核心是基于 Reactor 的相关 API 实现的。

3. 异步非阻塞

   - **异步和同步**/**非阻塞和阻塞**都是针对对象不一样
   - **异步和同步**针对调用者，**调用者**发送请求，如果等着对方回应之后才去做其他事情就是同步。如果发送请求之后不等着对方回应就去做其他事情就是异步。
   - **阻塞和非阻塞**针对被调用者，被调用者受到请求之后，做完请求任务之后才给出反馈就是阻塞，受到请求之后马上给出反馈然后再去做事情就是非阻塞。

4. Webflux特点:

   - 异步非阻塞式：在有限资源下，提高系统吞吐量和伸缩性，以Reactor 为基础实现响应式编程
   - Spring5 框架基于 java8，Webflux 使用 Java8 函数式编程方式实现路由请求

5. Webflux与SpringMVC

   ![spring5_新功能_webflux与SpringMVC](.\Spring框架markdown笔记图片\spring5_新功能_webflux与SpringMVC.png)

   - 第一 两个框架都可以使用注解方式，都运行在 Tomet 等容器中
   - 第二 SpringMVC采用命令式编程，Webflux采用异步响应式编程

- 响应式编程（Reactive Programming）

1. 什么是响应式编程

   - 响应式编程是一种面向数据流和变化传播的编程范式。这意味着可以在编程语言中很方便地表达静态或动态的数据流，而相关的计算模型会自动将变化的值通过数据流进行传播。

2. Java8 及其之前版本

   - 提供的观察者模式两个类 Observer 和 Observable

   - 演示案例

     ```java
     package com.uestc.demoreactor.reactor8;
     
     import java.util.Observable;
     
     public class ObserverDemo extends Observable {
         public static void main(String[] args) {
             ObserverDemo observer = new ObserverDemo();
             observer.addObserver((o, arg)->{
                 System.out.println("发生变化");
             });
             observer.addObserver((o, arg)->{
                 System.out.println("手动被观察者通知，准备改变");
             });
             observer.setChanged(); // 数据变化
             observer.notifyObservers(); // 通知
         }
     }
     ```

3. Java9及以后的版本

   - Flow类

- 响应式编程：Reactor 实现

1. 响应式编程操作中，Reactor 是满足 Reactive 规范框架
2. Reactor有两个**核心类**，**Mono 和Flux**，这两个类实现接口 Publisher，提供丰富操作符。Flux 对象实现发布者，返回N 个元素；Mono 实现翻发布者，返回0或者1个元素。
3. Flux 和 Mono 都是数据流的发布者，使用 Flux 和 Mono 都可以发出三种数据信号:
   - 元素值
   - 错误信号
   - 完成信号
   - 错误信号和完成信号都代表**终止信号**，终止信号用于告诉订阅者数据流的结束。

![spring5_新功能_flux和mono的特点](.\Spring框架markdown笔记图片\spring5_新功能_flux和mono的特点.png)

4. 代码演示

   - 引入依赖

     ```xml
     <dependency>
                 <groupId>io.projectreactor</groupId>
                 <artifactId>reactor-core</artifactId>
                 <version>3.1.5.RELEASE</version>
             </dependency>
     ```

   - 编写代码

     ```java
     public class testReactor {
         public static void main(String[] args) {
             // just方法直接声明
             Flux.just(1, 2, 3, 4);
             Mono.just(1);
             // 其他方法
             Integer[] array = {1, 2, 3, 4};
             Flux.fromArray(array);
     
             List<Integer> list = Arrays.asList(array);
             Flux.fromIterable(list);
             Stream<Integer> stream = list.stream();
             Flux.fromStream(stream);
         }
     }
     ```

5. 三种信号**特点**
   - 错误信号和完成信号都是终止信号，不能共存的。
   - 如果没有发送任何元素值，而是直接发送错误或者完成信号，表示是空数据流。
   - 如果没有错误信号，没有完成信号，表示是无限数据流。
6. 调用 just 或者其他方法只是声明数据流，数据流并没有发出，只有进行订阅之后才会触发数据流，不订阅什么都不会发生的。

```java
Flux.just(1, 2, 3, 4).subscribe(System.out::print); // subscribe使用订阅方法才触发数据量
Mono.just(1).subscribe(System.out::print);
```

7. 操作符

   - 对数据流进行一道道操作，成为操作符，比如工厂流水线

     - 第一 map 元素映射为新元素

       ![spring5_新功能_操作符](.\Spring框架markdown笔记图片\spring5_新功能_操作符.png)

     - 第二 flatMap 元素映射为流：把每个元素转换流，把转换之后多个流合并大的流

       ![spring5_新功能_操作符2](.\Spring框架markdown笔记图片\spring5_新功能_操作符2.png)

## Webflux执行流程和核心 API

- SpringWebflux基于 Reactor，默认使用容器是 Netty，Netty 是高性能的 NIO 框架，异步非阻
  塞的框架

1. 异步非阻塞和NIO

2. SpringWebfux执行过程和 SpringMVC 相似的

   - SpringWebflux核心控制器 DispatchHandler,实现接口 WebHandler

   - 接口 WebHandler 有一个方法。

     ![spring5_新功能_核心API](.\Spring框架markdown笔记图片\spring5_新功能_核心API.png)

   - SpringWebfux 里面 DispatcherHandler，负责请求的处理

3. SpringWebfux里面 DispatcherHandler负责请求的处理
   - HandlerMapping.请求查询到处理的方法
   - HandlerAdapter.真正负责请求处理
   - HandlerResultHandler.响应结果处理

4. SpringWebfux实现函数式编程，两个接口:RouterFunction(路由处理) 和 HandlerFunction(函数处理)

## SpringWebflux(基于注解编程模型)

- 使用注解编程模型方式，和之前 SpringMVC 使用相似的，只需要把相关依赖配置到项目中。SpringBoot 自动配置相关运行容器，默认情况下使用 Netty 服务器。

1. 创建springboot工程，引入相关依赖

   ```xml
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-webflux</artifactId>
   </dependency>
   ```

2. 配置启动端口号

   - resources/application.properties配置

     ```properties
     server.port=8081
     ```

3. 创建包和相关类

```java
package com.uestc.demowebflux.entity;

public class User {
    private String name;
    private String gender;
    private Integer age;

    public User(String name, String gender, Integer age) {
        this.name = name;
        this.gender = gender;
        this.age = age;
    }

    public User() {
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getGender() {
        return gender;
    }

    public void setGender(String gender) {
        this.gender = gender;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }
}
```

```java
package com.uestc.demowebflux.controller;

import com.uestc.demowebflux.entity.User;
import com.uestc.demowebflux.service.UserService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;
import reactor.core.publisher.Flux;
import reactor.core.publisher.Mono;

@RestController
public class UserController {
    @Autowired
    private UserService userService;
    // id 查询
    @GetMapping("/user/{id}")
    public Mono<User> getUserById(@PathVariable int id) {
        return userService.getUserById(id);
    }
    // 查询所有
    @GetMapping("/user")
    public Flux<User> getUsers() {
        return userService.getAllUser();
    }
    // 添加
    @PatchMapping("/saveuser")
    public Mono<Void> saveUser(@RequestBody User user) {
        Mono<User> userMono = Mono.just(user);
        return userService.saveUserInfo(userMono);
    }
}
```

```java
package com.uestc.demowebflux.service.impl;

import com.uestc.demowebflux.entity.User;
import com.uestc.demowebflux.service.UserService;
import org.springframework.stereotype.Repository;
import reactor.core.publisher.Flux;
import reactor.core.publisher.Mono;

import java.util.HashMap;
import java.util.Map;

@Repository
public class UserServiceImpl implements UserService {
    // 创建map集合存储数据
    private final Map<Integer, User> users =  new HashMap<>();

    public UserServiceImpl() {
        this.users.put(1, new User("Meez", "man", 20));
        this.users.put(2, new User("Jack", "man", 18));
        this.users.put(3, new User("Joe", "man", 22));
    }

    @Override
    public Mono<User> getUserById(int id) {
        return Mono.justOrEmpty(this.users.get(id));
    }

    @Override
    public Flux<User> getAllUser() {
        return Flux.fromIterable(this.users.values());
    }

    @Override
    public Mono<Void> saveUserInfo(Mono<User> userMono) {
        return userMono.doOnNext(person -> {
            int id = users.size() + 1;
            users.put(id, person);
        }).thenEmpty(Mono.empty());
    }
}
```

```java
package com.uestc.demowebflux.service;

import com.uestc.demowebflux.entity.User;
import reactor.core.publisher.Flux;
import reactor.core.publisher.Mono;

public interface UserService {
    // 根据id查询用户
    Mono<User> getUserById(int id);
    // 查询所有用户
    Flux<User> getAllUser();
    // 添加用户
    Mono<Void> saveUserInfo(Mono<User> userMono);
}
```



- 说明：

1. SpringMVC方式实现，同步阻塞的方式，基于SpringMVC+Servlet+Tomcat
2. SpringWebflux,方式实现，异步非阻塞方式，基于SpringWebflux+Reactor+Netty

## SpringWebflux(基于函数式编程模型)

1. 在使用函数式编程模型操作时候，需要**自己初始化服务器**。
2. 基于函数式编程模型时候，有两个核心接口:RouterFunction(实现路由功能，请求转发给对应的 handler)和 HandlerFunction(处理请求生成响应的函数)。核心任务定义两个函数式接口的实现并且启动需要的服务器。
3. SpringWebflux 请求和响应不再是ServletRequest和servletResponse,而是ServerReguest 和 ServerResponse.

- 案例演示



1. 复制注解式的工程
2. 创建 Handler

```java
package com.uestc.demowebflux.handler;

import com.uestc.demowebflux.entity.User;
import com.uestc.demowebflux.service.UserService;
import org.springframework.http.MediaType;
import org.springframework.web.reactive.function.server.ServerRequest;
import org.springframework.web.reactive.function.server.ServerResponse;
import reactor.core.publisher.Flux;
import reactor.core.publisher.Mono;

import static org.springframework.web.reactive.function.BodyInserters.fromObject;

public class UserHandler {
    private final UserService userService;
    public UserHandler(UserService userService) {
        this.userService = userService;
    }
    // 根据id查询
    public Mono<ServerResponse> getUserById(ServerRequest request) {
        // id 获取
        int userId = Integer.valueOf(request.pathVariable("id"));
        // 空值处理
        Mono<ServerResponse> notFound = ServerResponse.notFound().build();
        // 调用service方法得到数据
        Mono<User> userMono = this.userService.getUserById(userId);
        // 把userMono进行转换返回
        // 使用Reactor操作符flatMap
        return userMono.flatMap(person -> ServerResponse.ok().contentType(MediaType.APPLICATION_JSON)
                .body(fromObject(person))
                .switchIfEmpty(notFound));
    }
    // 查询所有
    public Mono<ServerResponse> getAllUsers() {
        // 调用service得到结果
        Flux<User> users = this.userService.getAllUser();
        return ServerResponse.ok().contentType(MediaType.APPLICATION_JSON).body(users, User.class);
    }
    // 添加
    public Mono<ServerResponse> saveUser(ServerRequest request) {
        Mono<User> userMono = request.bodyToMono(User.class);
        return ServerResponse.ok().build(this.userService.saveUserInfo(userMono));
    }
}
```

3. 初始化服务器，编写 Routere

```java
package com.uestc.demowebflux;

import com.uestc.demowebflux.handler.UserHandler;
import com.uestc.demowebflux.service.impl.UserServiceImpl;
import org.springframework.http.MediaType;
import org.springframework.http.server.reactive.HttpHandler;
import org.springframework.http.server.reactive.ReactorHttpHandlerAdapter;
import org.springframework.web.reactive.function.server.RouterFunction;
import org.springframework.web.reactive.function.server.ServerResponse;
import reactor.netty.http.server.HttpServer;

import java.io.IOException;

import static org.springframework.http.MediaType.APPLICATION_JSON;
import static org.springframework.web.reactive.function.server.RequestPredicates.GET;
import static org.springframework.web.reactive.function.server.RequestPredicates.accept;
import static org.springframework.web.reactive.function.server.RouterFunctions.toHttpHandler;

public class Server {
    public static void main(String[] args) throws IOException {
        Server server = new Server();
        server.createReactorServer();
        System.out.println("enter");
        System.in.read();
    }
    // 1 创建Router路由
    public static RouterFunction<ServerResponse> routingFunction() {
        UserServiceImpl userService = new UserServiceImpl();
        UserHandler userHandler = new UserHandler(userService);
        // 设置路由
        return RouterFunction.route(GET("/users/{id}").and(accept(APPLICATION_JSON)), userHandler::getUserById)
                .addRoute(GET("/users/").and(accept(APPLICATION_JSON)), userHandler::getAllUsers);

    }
    // 2 创建服务器完成适配
    public void createReactorServer() {
        // 路由和handler适配
        RouterFunction<ServerResponse> route = routingFunction();
        HttpHandler httpHandler = toHttpHandler(route);
        ReactorHttpHandlerAdapter adapter = new ReactorHttpHandlerAdapter(httpHandler);
        // 创建服务器
        HttpServer httpServer = HttpServer.create();
        httpServer.handle(adapter).bindNow();

    }
}
```

4. 使用 WebClient 调用,

```java
package com.uestc.demowebflux.client;

import com.uestc.demowebflux.entity.User;
import org.springframework.boot.autoconfigure.security.SecurityProperties;
import org.springframework.http.MediaType;
import org.springframework.web.reactive.function.client.WebClient;
import reactor.core.publisher.Flux;

public class Client {
    public static void main(String[] args) {
        // 调用服务器地址
        WebClient webClient = WebClient.create("http://127.0.0.1:5794");
        // 查询id
        String id = "1";
        User user = webClient.get().uri("/users/{id}", id).accept(MediaType.APPLICATION_JSON).retrieve().bodyToMono(User.class)
                .block();
        System.out.println(user.getName());

        // 查询所有
        Flux<User> results = webClient.get().uri("/users").accept(MediaType.APPLICATION_JSON).retrieve().bodyToFlux(User.class);
        results.map(stu -> stu.getName()).buffer().doOnNext(System.out::println).blockFirst();
    }
}

```

