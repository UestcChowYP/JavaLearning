

# MyBatis学习笔记

# 零.课程背景

## 1.课程知识结构

![知识结构介绍](.\0_MyBatis的MarkDown笔记的图片\知识结构介绍.png)

## 2.MyBatis特性

1) MyBatis 是支持定制化 SQL、存储过程以及高级映射的优秀的持久层框架
2) MyBatis 避免了几乎所有的JDBC 代码和手动设置参数以及获取结果集
3) MvBatis可以使用简单的XML或注解用于配置和原始映射，将接口和Java的POJO(Plain Oldjava Objects，普通的Java对象)映射成数据库中的记录
4) MyBatis 是一个半自动的ORM(Object Relation Mapping)框架

## 3.MyBatis下载

[GitHub - mybatis/mybatis-3: MyBatis SQL mapper framework for Java](https://github.com/mybatis/mybatis-3)

## 4.和其它持久化层技术对比

- JDBC
  - SQL夹杂在Java代码中耦合度高，导致硬编码内伤
  - 维护不易且实际开发需求中 SQL有变化，频繁修改的情况多见
  - 代码冗长，开发效率低
- Hibernate 和JPA
  - 操作简便，开发效率高
  - 程序中的长难复杂 SQL 需要绕过框架
  - 内部自动生产的 SQL，不容易做特殊优化
  - 基于全映射的全自动框架，大量字段的 POJ0 进行部分映射时比较困难，
  - 反射操作太多，导致数据库性能下降
- MyBatis
  - 轻量级，性能出色
  - SQL和Java 编码分开，功能边界清晰。Java代码专注业务、SQL语句专注数据
  - 开发效率稍逊于Hibernate，但是完全能够接受

# 二.搭建MyBatis

## 1.创建maven工程

- 打包方式：jar
- 引入依赖

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.uestc.mybatis</groupId>
    <artifactId>MyBatis_d1</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging>
    <dependencies>
        <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.16</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/junit/junit -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
        <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.3</version>
        </dependency>


    </dependencies>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

</project>
```

## 2.创建MyBatis的核心配置文件

- 习惯上命名为mybatis-confg.xml，这个文件名仅仅只是建议，并非强制要求。将来整合Spring之后，这个配置文件可以省略，所以大家操作时可以直接复制、粘贴。
- 核心配置文件主要用于配置连接数据库的环境以及MyBatis的全局配置信息
- 核心配置文件存放的位置是src/main/resources日录下

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "https://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:4306/mybatis"/>
                <property name="username" value="root"/>
                <property name="password" value="z123456"/>
            </dataSource>
        </environment>
    </environments>
<!--引入映射文件-->
    <mappers>
        <mapper resource="org/mybatis/example/BlogMapper.xml"/>
    </mappers>
</configuration>
```

## 3.创建mapper接口

- MyBatis中的mapper接口相当于以前的dao。但是区别在于，mapper仅仅是**接口**，我们不需要提供实现类。

```java
package com.uestc.mybatis.mapper;

public interface UserMapper {
    /**
     * 添加用户信息
     */
    int insertUser(); // 插入语句
}
```

## 4.创建MyBatis的映射文件

- 关概念:ORM(Object Relationship Mapping)对象关系映射。
  - 对象:Java的实体类对象
  - 关系:关系型数据库
  - 映射:二者之间的对应关系

| Java概念 | 数据库概念 |
| -------- | ---------- |
| 类       | 表         |
| 属性     | 字段/列    |
| 对象     | 记录/行    |

1. 映射文件的命名规则:
   - 表所对应的**实体类的类名**+**Mapper.xml**
   - 例如:表t_user，映射的实体类为User，所对应的映射文件为UserMapper.xml
   - 因此一个映射文件对应一个实体类，对应一张表的操作
   - MyBatis映射文件用于编写SOL，访问以及操作表中的数据
   - MyBatis映射文件存放的位置是**src/main/resources/mappers**目录下
2. MyBatis中可以面向接口操作数据，要保证**两个一致**:
   - a>mapper接囗的全类名和映射文件的命名空间(namespace属性)保持一致(映射文件一致)
   - b>mapper接口中方法的方法名和映射文件中编写SQL的标签的id属性保持一致(映射方法一致)

- 实体类-表-Mybatis配置文件-Mapper

1. 实体类

```java
public class User {
    private Integer id;
    private String username;
    private String password;
    private Integer age;
    private String sex;
    private String email;
    ...
```

2. Mysql数据库对应的表
3. Mybatis配置文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "https://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:4306/mybatis"/>
                <property name="username" value="root"/>
                <property name="password" value="z123456"/>
            </dataSource>
        </environment>
    </environments>
<!--引入映射文件-->
    <mappers>
        <mapper resource="mappers/UserMapper.xml"/>
    </mappers>
</configuration>
```

4. Mapper

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "https://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--设置Mapper映射文件-->
<mapper namespace="com.uestc.mybatis.mapper.UserMapper">
<!--设置查询语句-->
<!--int insertUser();-->
    <insert id="insertUser">
        insert into t_user values(null, 'admin', '123456', 23, '男', '12345@qq.com')
    </insert>
</mapper>
```

## 5.通过junit测试功能

```java
package com.uestc.mybatis.test;

import com.uestc.mybatis.mapper.UserMapper;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.junit.Test;

import javax.annotation.Resource;
import java.io.IOException;
import java.io.InputStream;

public class MybatisTest {
    @Test
    public void testMybatis() throws IOException {
        // 加载核心配置文件
        InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
        // 获取SqlSessionFactoryBuilder
        SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new SqlSessionFactoryBuilder();
        // 获取SqlSessionFactory
        SqlSessionFactory sqlSessionFactory = sqlSessionFactoryBuilder.build(is);
        // 获取SqlSession
        SqlSession sqlSession = sqlSessionFactory.openSession();
        // 获取mapper接口对象
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        // 测试功能
        int result = mapper.insertUser();
        // 提交事务
        sqlSession.commit();
        System.out.println(result);
    }
}
```

- 说明：

1. SqlSession:代表]ava程序和**数据库**之间的会话。(HttpSession是]ava程序和浏览器之间的会话)
2. SqlSessionFactory:是“生产"SqlSession的"工厂"
3. 工厂模式:如果创建某一个对象，使用的过程基本固定，那么我们就可以把创建这个对象的相关代码封装到一个“工厂类”中，以后都使用这个工厂类来“生产“我们需要的对象。

- 可以设置自动提交事务

```java
// 获取SqlSession
        SqlSession sqlSession = sqlSessionFactory.openSession(true); // 默认不自动提交事务/设置为true自动提交
```

## 6.加入log4j日志功能

1. 添加依赖

```xml
<dependency>
    <groupId>log4j</groupId>
    <artifactId>log4j</artifactId>
    <version>1.2.17</version>
</dependency>
```

2. 加入log4j的配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE log4j:configuration SYSTEM "log4j.dtd">
<!--爆红不影响运行-->
<log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/">
<!-- 控制台Appender配置 -->
    <appender name="STDOUT" class="org.apache.log4j.ConsoleAppender">
        <param name="Encoding" value="UTF-8" />
        <layout class="org.apache.log4j.PatternLayout">
            <param name="ConversionPattern" value="%d{yyyy-MM-dd HH:mm:ss} %-5p %c{1}:%L - %m%n" />
        </layout>
    </appender>

    <!-- 为特定的包或类设置Logger -->
    <logger name="java.sql">
            <level value="debug"/>
    </logger>
    <logger name="org.apache.ibatis">
        <level value="info"/>
    </logger>
    <root>
        <level value="debug"/>
        <appender-ref ref="STDOUT"/>
    </root>
</log4j:configuration>
```

- 日志级别

1. FATAL(致命)>ERROR(错误)>WARN(警告)>INFO(信息)>DEBUG(调试)
2. 从左到右打印的内容越来越详细，显示大于等于当前级别的信息

## 7.测试增删改查

1. UserMapper.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "https://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--设置Mapper映射文件-->
<mapper namespace="com.uestc.mybatis.mapper.UserMapper">
<!--设置查询语句-->
<!--int insertUser();-->
    <insert id="insertUser">
        insert into t_user values(null, 'admin', '123456', 23, '男', '12345@qq.com')
    </insert>
<!--void updateUser();-->
    <update id="updateUser">
        update t_user set username = '张三' where id = 2
    </update>
<!--void deleteUser();-->
    <update id="deleteUser">
        delete from t_user where id = 3
    </update>
<!--User getUserById();-->
<!--
查询功能的标签必须设置resultType/resultMap
resultType设置返回值类型/默认映射关系 - 类的属性名 和 数据的字段名 一致则可以映射
resultMap设置自定义的映射关系 - 类的属性名 和 数据的字段名 不一致
-->
    <select id="getUserById" resultType="com.uestc.mybatis.pojo.User">
        select * from t_user where id = 2
    </select>
<!--List<User> getAllUser();-->
    <select id="getAllUser" resultType="com.uestc.mybatis.pojo.User">
        select * from t_user
    </select>
</mapper>
```

2. UserMapper Java接口

```java
package com.uestc.mybatis.mapper;

import com.uestc.mybatis.pojo.User;

import java.util.List;

public interface UserMapper {
    /**
     * MyBatis面向接口编程的两个一致:
     * 1.映射文件的namespace要和mapper接口的全类名保持一致
     * 2.映射文件中SQL语句的id要和mapper接口中的方法名一致
     */
    // 添加用户信息
    int insertUser(); // 插入语句
    // 更新用户信息
    void updateUser();
    // 删除用户信息
    void deleteUser();
    // 根据id查询用户信息
    User getUserById();
    // 查询所有对象
    List<User> getAllUser();
}
```

3. 测试程序

```java
package com.uestc.mybatis.test;

import com.uestc.mybatis.mapper.UserMapper;
import com.uestc.mybatis.pojo.User;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.junit.Test;

import javax.annotation.Resource;
import java.io.IOException;
import java.io.InputStream;
import java.util.List;

public class MybatisTest {
    public UserMapper getMapper() throws IOException {
        InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(is);
        SqlSession sqlSession = sqlSessionFactory.openSession(true);
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        return mapper;
    }
    @Test
    public void testMybatis() throws IOException {
        // 加载核心配置文件
        InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
        // 获取SqlSessionFactoryBuilder
        SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new SqlSessionFactoryBuilder();
        // 获取SqlSessionFactory
        SqlSessionFactory sqlSessionFactory = sqlSessionFactoryBuilder.build(is);
        // 获取SqlSession
        SqlSession sqlSession = sqlSessionFactory.openSession(true); // 默认不自动提交事务/设置为true自动提交
        // 获取mapper接口对象
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        // 测试功能
        int result = mapper.insertUser();
//        // 提交事务
//        sqlSession.commit();
        System.out.println(result);
    }
    @Test
    public void testUpdate() throws IOException {
        InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(is);
        SqlSession sqlSession = sqlSessionFactory.openSession(true);
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        mapper.updateUser();
    }
    @Test
    public void testDelete() throws IOException {
        InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(is);
        SqlSession sqlSession = sqlSessionFactory.openSession(true);
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        mapper.deleteUser();
    }
    @Test
    public void testGetUserById() throws IOException {
        InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(is);
        SqlSession sqlSession = sqlSessionFactory.openSession(true);
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        User user = mapper.getUserById();
        System.out.println(user);
    }
    @Test
    public void testGetAllUser() throws IOException {
        UserMapper mapper = getMapper();
        List<User> allUser = mapper.getAllUser();
        allUser.forEach(user -> System.out.println(user));
    }

}
```

# 三.核心配置文件详解



- (了解)在实际开发过程中由Spring统一管理

核心配置文件中的标签必须按照固定的顺序:
properties?,settings?,typeAliases?,typeHandlers?,objectFactory?,objectWrapperFactory?,reflectorFactory?,plugins?,environments?,databaseldProvider?,mappers?

## 1.environment

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "https://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
<!--配置连接数据库的环境-->
<!--
environments:配置多个连接数据库的环境
    属性:id:表示连接数据库的环境的唯一标识，不能重复
-->
    <environments default="development">
        <environment id="development">
<!--
transactionManager：设置事务管理方式
    type="JDBC/MANAGED
        JDBC：表示当前环境中，执行SQL时，使用的是JDBC中原生的事务管理方式，事务的提交或回滚需要手动处理
        MANAGED:被管理，例如Spring
-->
            <transactionManager type="JDBC"/>
<!--
dataSource:配置数据源
属性:
    type:设置数据源的类型
    type="POOLED/UNPOOLED/JNDI"
    POOLED:表示使用数据库连接池缓存数据库连接
    UNPOOLED:表示不使用数据库连接池
    JNDI:表示使用上下文中的数据源
-->
            <dataSource type="POOLED">
<!--                连接数据库的驱动-->
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <!--                连接数据库的地址-->
                <property name="url" value="jdbc:mysql://localhost:4306/mybatis"/>
                <property name="username" value="root"/>
                <property name="password" value="z123456"/>
            </dataSource>
        </environment>
    </environments>
<!--引入映射文件-->
    <mappers>
        <mapper resource="mappers/UserMapper.xml"/>
    </mappers>
</configuration>
```

## 2.用配置文件来设置数据库的连接

1. 写配置文件resources/jdbc.properties

```properties
jdbc.username=root
jdbc.password=z123456
jdbc.url=jdbc:mysql://localhost:4306/mybatis
jdbc.driver=com.mysql.jdbc.Driver
```

2. 添加配置文件:mybatis-config.xml

```xml
<properties resource="jdbc.properties" />
```

3. 修改配置

```xml
<property name="driver" value="${jdbc.driver}"/>
<property name="url" value="${jdbc.url}"/>
<property name="username" value="${jdbc.username}"/>
<property name="password" value="${jdbc.password}"/>
```

## 3.类型别名:typeAliases

- 使用别名标签:typeAliases

1. mybatis-config.xml中设置别名标签：

```xml
<typeAliases>
    <typeAlias type="com.uestc.mybatis.pojo.User" alias="User"/>
</typeAliases>
```

2. UserMapper.xml中使用别名:MyBatis范围内均可以使用/ 别名**不区分大小写**

```xml
<!--使用别名-->
<select id="getUserById" resultType="User">
    select * from t_user where id = 2
</select>
```

- 以包为单位引用

```xml
<!--设置类型别名-->
<typeAliases>
    <typeAlias type="com.uestc.mybatis.pojo.User" alias="User"/>
    <!--以包为单位，将包下所有的类型设置默认的类型别名，即类名且不区分大小写-->
    <package name="com.uestc.mybatis.pojo"/>
</typeAliases>
```

## 4.mappers

- 同样可以引入单个配置文件/引入配置包

1. 引入单个配置文件

```xml
<mappers>
    <mapper resource="com/uestc/mybatis/mapper/UserMapper.xml"/>
</mappers>
```

2. 引入配置包
   1. mapper接口所在的包要和映射文件所在的包一致
   2. mapper接口要和映射文件的名字一致

- 注意：resources目录下创建包需要用/来分隔

```xml
<!--引入映射文件-->
<mappers>
    <!--
以包为单位引入映射文件
要求:
1、mapper接口所在的包要和映射文件所在的包一致
2.mapper接口要和映射文件的名字一致
-->
    <package name="com.uestc.mybatis.mapper"/>
</mappers>
```

# 四.MyBatis获取参数值的两种方式(重点)

## 0.构建Maven工程

1. 创建项目
2. 添加依赖

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.uestc.mybatis</groupId>
    <artifactId>Mybatis_MBG</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging>
    <dependencies>
        <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.16</version>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.3</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/log4j/log4j -->
        <dependency>
            <groupId>log4j</groupId>
            <artifactId>log4j</artifactId>
            <version>1.2.17</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/junit/junit -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>

    </dependencies>
<!--控制Maven在构建过程中相关配置-->
    <build>
<!--构建过程中用到的插件-->
        <plugins>
<!--具体插件，逆向工程的操作是以构建过程中插件形式出现的-->
            <plugin>
                <groupId>org.mybatis.generator</groupId>
                <artifactId>mybatis-generator-maven-plugin</artifactId>
                <version>1.3.0</version>
                <dependencies>
                    <!-- https://mvnrepository.com/artifact/org.mybatis.generator/mybatis-generator-core -->
                    <dependency>
                        <groupId>org.mybatis.generator</groupId>
                        <artifactId>mybatis-generator-core</artifactId>
                        <version>1.3.2</version>
                    </dependency>

                    <!-- https://mvnrepository.com/artifact/com.mchange/c3p0 -->
                    <dependency>
                        <groupId>com.mchange</groupId>
                        <artifactId>c3p0</artifactId>
                        <version>0.9.5.2</version>
                    </dependency>
                    <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
                    <dependency>
                        <groupId>mysql</groupId>
                        <artifactId>mysql-connector-java</artifactId>
                        <version>5.1.3</version>
                    </dependency>
                </dependencies>
            </plugin>
        </plugins>
    </build>
    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
</project>
```

3. 创建mybatis-config.xml

- IDEA中setting的Editor/File and Code Templates 自己添加mybatis-config模板

  ```xml
  <?xml version="1.0" encoding="UTF-8" ?>
  <!DOCTYPE configuration
          PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
          "https://mybatis.org/dtd/mybatis-3-config.dtd">
  <configuration>
      <properties resource="jdbc.properties" />
      <typeAliases>
          <package name=" "/>
      </typeAliases>
      <environments default="development">
          <environment id="development">
              <transactionManager type="JDBC"/>
              <dataSource type="POOLED">
                  <property name="driver" value="${jdbc.driver}"/>
                  <property name="url" value="${jdbc.url}"/>
                  <property name="username" value="${jdbc.username}"/>
                  <property name="password" value="${jdbc.password}"/>
              </dataSource>
          </environment>
      </environments>
      <mappers>
          <mapper resource=" "/>
      </mappers>
  </configuration>
  ```

1. 设置Mapper模板

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE mapper
     PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
     "https://mybatis.org/dtd/mybatis-3-mapper.dtd">
   
   <mapper namespace=" ">
     
   </mapper>
   ```

## 1.Mybatis参数获取

- 1.MyBatis获取参数值的两种方式:${}和#{}

1. ${}的本质就是字符串拼接
2. #{}的本质就是占位符赋值
3. ${}使用字符串拼接的方式拼接sql，若为字符串类型或日期类型的字段进行赋值时，需要手动加单引号;但是#{}使用占位符赋值的方式拼接sql，此时为字符串类型或日期类型的字段进行赋值时，可以自动添加单引号

```xml
<!--User GetUserByUsername(String Username);-->
    <select id="GetUserByUsername" resultType="User">
<!--占位符赋值跟参数名无关，只与参数位置有关-->
<!--        select * from t_user where username= #{Username}-->
<!--${}是字符串拼接需要手动添加单引号-->
        select * from t_user where username= '${name}'
    </select>
```

- 2.多个参数的情况:此时myBatis会将这些参数放在一个ap集合中，以两种方式进行存储

1. 以arg0,arg1...为键，以参数为值
2. 以param1,param2...为键，以参数为值

```xml
<select id="checkLogin" resultType="User">
    <!--多个参数的情况，参数会放在map中需要用arg0, arg1访问 或 param0, param1访问-->
    <!--        select * from t_user where username = #{arg0} and password = #{arg1}-->
    select * from t_user where username = '${arg0}' and password = '${arg1}'
</select>
```

- 3.若mapper接口方法的参数有多个时，可以手动将这些参数放在一个map中存储
  - 自己构建键名与值

```xml
<!--User checkLoginByMap(Map<String, Object> map);-->
<select id="checkLoginByMap" resultType="User">
    select * from t_user where username = '${username}' and password = '${password}'
</select>
```

```java
@Test
public void checkLoginByMap() {
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    ParameterMapper mapper = sqlSession.getMapper(ParameterMapper.class);
    Map<String, Object> map = new HashMap<>();
    map.put("username", "张三");
    map.put("password", "123456");
    User user = mapper.checkLoginByMap(map);
    System.out.println(user);
}
```

- 4.mapper接口方法的参数是**实体类类型**

```xml
<insert id="insertUser">
    <!--通过get/set方法获取-->
    insert into t_user values(null, #{username}, #{password}, #{age}, #{sex}, #{email})
</insert>
```

```java
@Test
public void checkLoginByMap() {
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    ParameterMapper mapper = sqlSession.getMapper(ParameterMapper.class);
    Map<String, Object> map = new HashMap<>();
    map.put("username", "张三");
    map.put("password", "123456");
    User user = mapper.checkLoginByMap(map);
    System.out.println(user);
}
```

- 5.使用@Param注解命名参数

1. 以@Param("key")的key为键，参数为值，添加到map中
2. 以以param1,param2...为键，以参数为值

```java
User checkLoginByParam(@Param("username") String username, @Param("password") String password);
```

2. 直接使用key访问参数

```xml
<!--User checkLoginByParam(@Param("username") String username, @Param("password") String password);-->
<select id="checkLoginByParam" resultType="User">
    select * from t_user where username = '${username}' and password = '${password}'
</select>
```

3. 查询测试

```java
@Test
public void checkLoginByParam() {
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    ParameterMapper mapper = sqlSession.getMapper(ParameterMapper.class);
    User user = mapper.checkLoginByParam("张三", "123456");
    System.out.println(user);
}
```

- 推荐使用实体类/@Param的方式进行开发

- 数组和集合类型的参数后序讲解：[动态sql部分](##5.foreach)
  - 使用@Param



# 五.MyBatis的各种查询功能

- MyBatis的各种查询功能:

1. 若查询出的数据只有一条，
   - 可以通过实体类对象接收
   - 可以通过集合List/Map接收
2. 若查询出的数据有多条，一定不能通过实体类对象接收 
   - 可以通过实体类的List集合接收(此时会抛异常TooManyResultsException)
   - 可以通过map类的List集合接收

## 1.查询单个返回对象

1. 查询一个实体类对象
2. 查询用户信息的总记录数

- Java的常用数据类型都内置类的别名，不区分大小写

```xml
<!--Integer getCount();-->
<select id="getCount" resultType="java.lang.Integer">
    select count(*) from t_user
</select>
```

```java
@Test
public void testGetCount() {
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    SelectMapper mapper = sqlSession.getMapper(SelectMapper.class);
    Integer count = mapper.getCount();
    System.out.println( count );
}
```

3. 返回map以字段为key，以对应的属性值为value

```xml
Map<String, Object> getUserByIdToMap(@Param("id") Integer id);
```

```xml
<!--Map<String, Object> getUserByIdToMap(@Param("id") Integer id);-->
<select id="getUserByIdToMap" resultType="map">
    select * from t_user where id = #{id}
</select>
```

```java
@Test
public void testGetUserByIdToMap() {
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    SelectMapper mapper = sqlSession.getMapper(SelectMapper.class);
    Map<String, Object> map = mapper.getUserByIdToMap(4);
    System.out.println(map);
}
// 输出
// {password=z123456, sex=中, id=4, age=18, email=z123@qq.com, username=zyp}
```

## 2.查询多个对象返回集合

1. 查询所有用户信息使用List集合接收Map信息

```xml
<!--List<Map<String, Object>>-->
<select id="getAllUserToMap">
    select * from t_user
</select>
```

```java
@Test
public void testGetAllUserToMap() {
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    SelectMapper mapper = sqlSession.getMapper(SelectMapper.class);
    List<Map<String, Object>> list = mapper.getAllUserToMap();
    System.out.println(list);
}
```

2. @MapKey("id")指定id字段作为键

```java
@MapKey("id")
    Map<String, Object> getAllUserToMap();
```

```xml
<select id="getAllUserToMap" resultType="map">
    select * from t_user
</select>
```

```java
@Test
public void testGetAllUserToMap() {
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    SelectMapper mapper = sqlSession.getMapper(SelectMapper.class);
    Map<String, Object> map = mapper.getAllUserToMap();
    System.out.println(map);
}
```

# 六.特殊SQL的执行

## 1.模糊查询

1. 使用${}

```xml
select * from t_user where username like '%${username}%'
```

2. 使用sql的字符串拼接

```xml
select * from t_user where username like concat('%',#{username} , '%')
```

3. 最常用方式：双引号拼接

```xml
select * from t_user where username like "%"#{username}"%"
```

## 2.批量删除

- 使用${}

```xml
<!--int deleteMore(@Param("ids") String ids);-->
<delete id="deleteMore">
    delete from t_user where id in (${ids})
</delete>
```

```java
@Test
public void testDeleteMore() {
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    SQLMapper mapper = sqlSession.getMapper(SQLMapper.class);
    int i = mapper.deleteMore("1, 3, 5");
    System.out.println(i);
}
```

## 3.动态设置表名

- 使使用${}

```xml
<!--List<User> getUserByTableName(@Param("tableName") String tableName);-->
<select id="getUserByTableName" resultType="User">
    select * from ${tableName}
</select>
```

```java
@Test
public void testGetUserByTableName() {
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    SQLMapper mapper = sqlSession.getMapper(SQLMapper.class);
    List<User> list = mapper.getUserByTableName("t_user");
    System.out.println(list);
}
```

## 4.添加功能获取自增的主键

- 需求
  - t_clazz(clazz_id,clazz_name)
  - t_studenf(student_id,student_name,clazz_id)

1. 添加班级信息
2. 获取新添加的班级的id
3. 为班级分配学生，即将某学的班级id修改为新添加的班级的id

```xml
<!--
User InsertUser(User user);
useGeneratedKeys:设置当前标签中的sql使用了自增的主键 - id
keyProperty:将自增的主键的值赋给某个属性
-->
<insert id="InsertUser" useGeneratedKeys="true" keyProperty="id">
    insert into t_user values(null, #{username}, #{password}, #{age}, #{sex}, #{email})
</insert>
```

```java
@Test
public void testGInsertUser() {
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    SQLMapper mapper = sqlSession.getMapper(SQLMapper.class);
    User user = new User(null, "syj", "z123456", 18, "女", "yj@qq.com");
    mapper.InsertUser(user);
    System.out.println(user);
}
```

# 八.自定义映射resultMap

## 1.resultMap处理字段和属性的映射关系

- 数据库字段和pojo类属性名一致时自动注入

- 数据库字段和pojo类属性名不一致时

1. 方式一：为字段取别名--使字段别名和属性名一致

```xml
<!--List<Emp> getAllEmp();-->
<select id="getAllEmp" resultType="Emp">
    select eid, emp_name empName, age, sex, email, did from t_emp
</select>
```

2. 方式二：设置MyBatis全局配置：mybatis-config.xml文件。开启驼峰命名自动映射。

```xml
<settings>
    <!--开启驼峰命名自动映射，即从经典数据库列名 A_COLUMN 映射到经典 Java 属性名 aColumn-->
    <setting name="mapUnderscoreToCamelCase" value="true"/>
</settings>
```

```xml
<!--List<Emp> getAllEmp();-->
<select id="getAllEmp" resultType="Emp">
    select * from t_emp
</select>
```

3. 方式三：resultMap实现映射

```xml
    <resultMap id="empResultMap" type="Emp">
<!--type设置实体类类型-->
<!--id设置主键的映射关系/result设置普通属性的关系-->
<!--property对应属性名 column对应字段名-->
        <id property="eid" column="eid" />
        <result property="empName" column="emp_name" />
        <result property="age" column="age" />
        <result property="sex" column="sex" />
        <result property="email" column="email" />
    </resultMap>
<!--List<Emp> getAllEmp();-->
    <select id="getAllEmp" resultMap="empResultMap">
        select * from t_emp
    </select>
```

## 2.处理多对一的映射关系

1. 级联属性赋值

```xml
<!--Emp getEmpAndDeptByEid(@Param("eid") Integer eid);-->
    <resultMap id="empAndDeptResultMapOne" type="Emp">
        <id property="eid" column="eid"/>
        <result property="empName" column="emp_name" />
        <result property="age" column="age" />
        <result property="sex" column="sex" />
        <result property="email" column="email" />
        <result property="dept.did" column="did" />
        <result property="dept.deptName" column="dept_name" />
    </resultMap>
    <select id="getEmpAndDeptByEid" resultMap="empAndDeptResultMapOne">
        select * from t_emp left join t_dept on t_emp.did = t_dept.did where t_emp.eid = #{eid}
    </select>
```

```java
@Test
public void testGetEmpAndDeptByEid() {
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    EmpMapper mapper = sqlSession.getMapper(EmpMapper.class);
    Emp emp = mapper.getEmpAndDeptByEid(8);
    System.out.println(emp);
}
```

2. association标签

```xml
<resultMap id="empAndDeptResultMapTwo" type="Emp">
        <id property="eid" column="eid"/>
        <result property="empName" column="emp_name" />
        <result property="age" column="age" />
        <result property="sex" column="sex" />
        <result property="email" column="email" />
        <association property="dept" javaType="Dept">
            <id property="did" column="did"/>
            <result property="deptName" column="dept_name"/>
        </association>
    </resultMap>
    <select id="getEmpAndDeptByEid" resultMap="empAndDeptResultMapTwo">
        select * from t_emp left join t_dept on t_emp.did = t_dept.did where t_emp.eid = #{eid}
    </select>
```

3. 分步查询：通过两/多个sql查询

1. EmpMapper

```xml
<!--Emp getEmpAndDeptByStepOne(@Param("eid") Integer eid);-->
<resultMap id="empAndDeptByStepResultMap" type="Emp">
    <id property="eid" column="eid"/>
    <result property="empName" column="emp_name" />
    <result property="age" column="age" />
    <result property="sex" column="sex" />
    <result property="email" column="email" />
    <!--
select:sql语句的唯一标识/全类名.方法名
column:此处的column表示分布查询的条件
-->
    <association property="dept"
                 select="com.uestc.mybatis.mapper.DeptMapper.getEmpAndDeptByStepByStepTwo"
                 column="did">

    </association>
</resultMap>
<select id="getEmpAndDeptByStepOne" resultMap="empAndDeptByStepResultMap">
    select * from t_emp where eid = #{eid}
</select>
```

2. DeptMapper

```xml
<!--Dept getEmpAndDeptByStepByStepTwo(@Param("did") Integer did);-->
<select id="getEmpAndDeptByStepByStepTwo" resultType="Dept">
    select * from t_dept where did = #{did}
</select>
```

3. 测试程序

```java
@Test
public void testGetEmpAndDeptByStep() {
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    EmpMapper mapper = sqlSession.getMapper(EmpMapper.class);
    Emp emp = mapper.getEmpAndDeptByStepOne(8);
    System.out.println(emp);
}
```

- 分步查询的优点:可以实现延迟加载，但是必须在核心配置文件中设置全局配置信息:

1. azyLoadingEnabled:延迟加载的全局开关。当开启时，所有关联对象都会延迟加载
2. aggressiveLazyLoading:当开启时，任何方法的调用都会加载该对象的所有属性。 否则，每个属性会按需加载
3. 此时就可以实现按需加载，获取的数据是什么，就只会执行相应的sql。此时可通过association和collection中的fetchType属性设置当前的分步查询是否使用延迟加载，fetchType="lazy(延迟加载)eager(立即加载)”

- 开启延迟查询：使用到其他sql步骤查询的信息时才会执行其他步骤的sql语句

1. 添加设置信息：

   - 配置文件中设置延迟加载：全局开启

   ```xml
   <settings>
       <!--开启延迟加载-->
       <setting name="lazyLoadingEnabled" value="true"/>
   </settings>
   ```

   

   - 某些查询请求设置关闭延迟加载:fetchType="eager/lazy"

   ```xml
   <!--
   fetchType:(当开启了全局的延迟加载之后)，可通过此属性手动控制延迟加载的效果
   lazy:开启延迟加载
   eage：立即加载
   -->
   <association property="dept"
   		select="com.uestc.mybatis.mapper.DeptMapper.getEmpAndDeptByStepByStepTwo"
                column="did"
                fetchType="eager">
   </association>
   ```

   

2. 测试

```java
@Test
public void testGetEmpAndDeptByStepOne() {
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    EmpMapper mapper = sqlSession.getMapper(EmpMapper.class);
    Emp emp = mapper.getEmpAndDeptByStepOne(8);
    System.out.println(emp.getEmpName()); // 未使用第二步查询的信息
}
// 此时不执行查询的第二步
```

## 3.处理一对多的映射关系

1. 方法一：使用collection标签

```xml
<!--Dept getDeptAndEmp(@Param("did") Integer did);-->
    <resultMap id="deptAndEmpResultMap" type="Dept">
        <id property="did" column="did" />
        <result property="deptName" column="dept_name"/>
<!--
collection:处理一对多的映射关系
ofType:表示该属性所对应的集合中存储数据的类型
-->
        <collection property="emps" ofType="Emp">
            <id property="eid" column="eid" />
            <result property="empName" column="emp_name" />
            <result property="age" column="age" />
            <result property="sex" column="sex" />
            <result property="email" column="email" />
        </collection>
    </resultMap>
    <select id="getDeptAndEmp" resultMap="deptAndEmpResultMap">
        select * from t_dept left join t_emp on t_dept.did = t_emp.did where t_dept.did = #{did}
    </select>
```

```java
@Test
public void testGetDeptAndEmp() {
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    DeptMapper mapper = sqlSession.getMapper(DeptMapper.class);
    Dept dept = mapper.getDeptAndEmp(2);
    System.out.println(dept);
}
```

2. 方法二：分步查询

```xml
<!--Dept getDeptAndEmpByStepOne(@Param("did") Integer did);-->
<resultMap id="deptAndEmpByStepResultMap" type="Dept">
    <id property="did" column="did" />
    <result property="deptName" column="dept_name"/>
    <collection property="emps"
                select="com.uestc.mybatis.mapper.EmpMapper.getDeptAndEmpByStepTwo"
                column="did"/>
</resultMap>
<select id="getDeptAndEmpByStepOne" resultMap="deptAndEmpByStepResultMap">
    select * from t_dept where did = #{did}
</select>
```

```xml
<!--List<Emp> getDeptAndEmpByStepTwo(@Param("did") Integer did);-->
<select id="getDeptAndEmpByStepTwo" resultType="Emp">
    select * from t_emp where did = #{did}
</select>
```

```java
@Test
public void testGetDeptAndEmpByStepOne() {
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    DeptMapper mapper = sqlSession.getMapper(DeptMapper.class);
    Dept dept = mapper.getDeptAndEmpByStepOne(2);
    System.out.println(dept);
}
```

# 九.动态SQL

- Mybatis框架的动态SQL技术是一种根据特定条件动态拼装SQL语句的功能，它存在的意义是为了解决拼接SQL语
  句字符串时的痛点问题。 (多条件的时候如何拼接sql？)

## 1.if标签

- if:根据标签中test属性所对应的表达式决定标签中的内容是否需要拼接到SQL中
  - 使用一个恒成立的标签辅助sql拼接

```xml
<!--List<Emp> getEmpByConditionOne(Emp emp);-->
<select id="getEmpByConditionOne" resultType="Emp">
    select * from t_emp where 1 = 1
    <if test="empName != null and empName != ''">
        and emp_name = #{empName}
    </if>
    <if test="age != null and age != ''">
        and age = #{age}
    </if>
    <if test="sex != null and sex != ''">
        and sex = #{sex}
    </if>
    <if test="email != null and email  != ''">
        and email  = #{email }
    </if>
</select>
```

```java
@Test
public void testGetEmpByCondition(){
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    DynamicSQLMapper mapper = sqlSession.getMapper(DynamicSQLMapper.class);
    List<Emp> list = mapper.getEmpByCondition(new Emp(null, null, null, "M", null));
    System.out.println(list);
}
```

## 2.where标签

- 字段处理and/or关键字

1. 当where标签中有内容时，会自动生成where关键字，并且将**内容前多余**的and或or去掉
2. 当where标签中没有内容时，此时where标签没有任何效果
3. 注意:where标签不能将其中内容后面多余的and或or去掉
   - 反例：emp_name = #{empName} and

```xml
<!--List<Emp> getEmpByConditionTwo(Emp emp);-->
<select id="getEmpByConditionTwo" resultType="Emp">
    select * from t_emp
    <where>
        <if test="empName != null and empName != ''">
            emp_name = #{empName}
        </if>
        <if test="age != null and age != ''">
            and age = #{age}
        </if>
        <if test="sex != null and sex != ''">
            or sex = #{sex}
        </if>
        <if test="email != null and email  != ''">
            and email  = #{email }
        </if>
    </where>
</select>
```

## 3.trim标签

- trim:
- 若标签中有内容时:

1. prefix/suffix:将trim标签中内容前面或后面添加指定内容
2. suffixoverrides/prefixoverrides:将trim标签中内容前面或后面去掉指定内容

- 若标签中没有内容时，trim标签也没有任何效果

```xml
<!--List<Emp> getEmpByConditionThree(Emp emp);-->
<select id="getEmpByConditionThree" resultType="Emp">
    select * from t_emp
    <trim prefix="where" suffixOverrides="and|or">
        <if test="empName != null and empName != ''">
            emp_name = #{empName} and
        </if>
        <if test="age != null and age != ''">
            age = #{age} and
        </if>
        <if test="sex != null and sex != ''">
            sex = #{sex} and
        </if>
        <if test="email != null and email  != ''">
            email  = #{email }
        </if>
    </trim>
</select>
```

## 4.choose,when,otherwise标签

- 相当于Java中的 if/else if/ else
  - 选择最前面成立的标签加入

```xml
<!--List<Emp> getEmpByChoose(Emp emp);-->
<select id="getEmpByChoose" resultType="Emp">
    select * from t_emp
    <where>
        <choose>
            <when test="empName != null and empName != ''">
                emp_name = #{empName}
            </when>
            <when test="age != null and age != ''">
                age = #{age}
            </when>
            <when test="sex != null and sex != ''">
                sex = #{sex}
            </when>
            <when test="email != null and email  != ''">
                email  = #{email}
            </when>
        </choose>
    </where>
</select>
```

## 5.foreach

### 通过数组实现批量删除

1. 写法1：where in 关键字

```xml
<!--int deleteMoreByArray(@Param("eids") Integer[] eids);-->
<delete id="deleteMoreByArray">
    delete from t_emp where eid in
    <!--
collection: 集合参数
item：集合的成员
separator：分隔符号
open/close：开头和结尾
-->
    <foreach collection="eids" item="eid" separator="," open="(" close=")">
        #{eid}
    </foreach>
</delete>
```

2. 写法2：where or 关键字

```xml
<!--int deleteMoreByArray(@Param("eids") Integer[] eids);-->
<delete id="deleteMoreByArray">
    delete from t_emp where
    <foreach collection="eids" item="eid" separator="or">
        eid = #{eid}
    </foreach>
</delete>
```

### 通过list集合实现批量添加

```xml
<!--int insertMoreByList(@Param("emps") List<Emp> emps);-->
<insert id="insertMoreByList">
    insert into t_emp values
    <foreach collection="emps" item="emp" separator=",">
        (null, #{emp.empName}, #{emp.age}, #{emp.sex}, #{emp.email}, null)
    </foreach>
</insert>
```

## 6.sql标签

- 设置sql片段 -> 使用sql片段

```xml
<sql id="empColumns">eid, emp_name, age, sex, email</sql>
<select id="getEmpByChoose" resultType="Emp">
    select <include refid="empColumns" /> from t_emp
</select> 
```

# 十.MyBatis的缓存

- 缓存针对**查询**功能

## 1.MyBatis的一级缓存

- 一级缓存是SqlSession级别的，通过同一个SqlSession查询的数据会被缓存，下次查询相同的数据，就会从缓存中直接获取，不会从数据库重新访问

```java
@Test
public void testGetEmpById() {
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    CacheMapper mapper1 = sqlSession.getMapper(CacheMapper.class);
    Emp emp1 = mapper1.getEmpById(8);
    System.out.println(emp1);
    CacheMapper mapper2 = sqlSession.getMapper(CacheMapper.class);
    Emp emp2 = mapper2.getEmpById(8);
    System.out.println(emp2);
}
// 查询相同内容只有第一次会执行sql语句，第二次直接从缓存获取
```

- 使一级缓存失效的四种情况:

1. 不同的SqlSession对应不同的一级缓存
2. 同一个SqlSession但是**查询条件**不同
3. 同一个SqlSession两次查询期间执行了任何一次**增删改**操作
4. 同一个SqlSession两次查询期间手动清空了缓存

```java
// 增删改操作
@Test
public void testGetEmpById() {
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    CacheMapper mapper1 = sqlSession.getMapper(CacheMapper.class);
    Emp emp1 = mapper1.getEmpById(8);
    System.out.println(emp1);
    mapper1.insertEmp(new Emp(null, "z111", 18, "F", "z111@qq.com"));
    Emp emp2 = mapper1.getEmpById(8);
    System.out.println(emp2);
}
```

```java
// sqlSession.clearCache(); 清空缓存
@Test
public void testGetEmpById() {
    SqlSession sqlSession = SqlSessionUtils.getSqlSession();
    CacheMapper mapper1 = sqlSession.getMapper(CacheMapper.class);
    Emp emp1 = mapper1.getEmpById(8);
    System.out.println(emp1);
    sqlSession.clearCache();
    Emp emp2 = mapper1.getEmpById(8);
    System.out.println(emp2);
}
```



## 2.MyBatis的二级缓存

- 二级缓存是SqlSessionFactory级别，通过同一个SalSessionFactory创建的SqlSession查询的结果会被缓存;此后
  若再次执行相同的查询语句，结果就会从缓存中获取

```java

```



- 二级缓存开启的条件:

1. 在核心配置文件中，设置全局配置属性cacheEnabled="true"，**默认为true**，不需要设置
2. 在映射文件中设置标签< cache / >
3. 二级缓存必须在SqlSession**关闭或提交**之后有效
4. 查询的数据所转换的实体类类型必须实现**序列化的接口**Serializable

```xml
<cache />
<!--CacheMapper.xml中添加-->
```

```java
public class Emp implements Serializable {
...
}
// 实现接口
```

```java
@Test
public void testTwoCache() {
    InputStream is = null;
    try {
        is = Resources.getResourceAsStream("mybatis-config.xml");
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(is);
        SqlSession sqlSession1 = sqlSessionFactory.openSession(true);
        CacheMapper mapper1 = sqlSession1.getMapper(CacheMapper.class);

        System.out.println(mapper1.getEmpById(8));
        sqlSession1.close();
        SqlSession sqlSession2 = sqlSessionFactory.openSession(true);
        CacheMapper mapper2 = sqlSession2.getMapper(CacheMapper.class);

        System.out.println(mapper2.getEmpById(8));
        sqlSession2.close();
    } catch (IOException e) {
        throw new RuntimeException(e);
    }
}
```

- 使二级缓存失效的情况:
  两次查询之间执行了任意的**增删改**，会使一级和二级缓存同时失效

## 3.二级缓存的相关配置

在mapper配置文件中添加的cache标签可以设置一些属性:

- eviction属性:缓存回收策略

1. LRU(Least Recently Used)最近最少使用的:移除最长时间不被使用的对象。
2. FIFO(First in First out)先进先出:按对象进入缓存的顺序来移除它们。
3. SOFT软引用:移除基于垃圾回收器状态和软引用规则的对象。
4. WEAK弱引用:更积极地移除基于垃圾收集器状态和弱引用规则的对象。
5. 默认的是 LRU。

- flushInterval属性:刷新间隔，单位毫秒
  默认情况是不设置，也就是没有刷新间隔，缓存仅仅调用**增删改**语句时刷新
- size属性:引用数目，正整数
  代表缓存最多可以存储多少个对象，太大容易导致内存溢出
- readOnly属性:只读，true/false
  true:只读缓存;会给所有调用者返回缓存对象的相同实例。因此这些对象不能被修改。这提供了很重要的性能优势。
  false:读写缓存;会返回缓存对象的拷贝(通过序列化)。这会慢一些，但是安全，因此默认是 false.

## 4.MyBatis缓存查询的顺序

二级 -> 一级 -> 数据库

- 先查询二级缓存，因为二级缓存中可能会有其他程序已经查出来的数据，可以拿来直接使用。
- 如果二级缓存没有命中，再查询一级缓存
- 如果一级缓存也没有命中，则查询数据库
- SqlSession关闭之后，一级缓存中的数据会写入二级缓存

## 5.整合第三方缓存EHCache:（用不起）

1. 添加依赖

```xml
<!-- https://mvnrepository.com/artifact/org.mybatis.caches/mybatis-ehcache -->
<dependency>
    <groupId>org.mybatis.caches</groupId>
    <artifactId>mybatis-ehcache</artifactId>
    <version>1.2.1</version>
</dependency>
<dependency>
    <groupId>ch.qos.logback</groupId>
    <artifactId>logback-classic</artifactId>
    <version>1.2.3</version>
</dependency>
```

2. 各jar包功能

| Jar包名称       | 作用                            |
| --------------- | ------------------------------- |
| mybatis-ehcache | Mybatis和EHCache的整合包        |
| ehcache         | EHCache核心包                   |
| slf4j-api       | SLF4j日志门面包                 |
| logback-classic | 支持SLF4j门面接口的一个具体实现 |

3. 创建EHCache的配置文件ehcache.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="http://ehcache.org/ehcache.xsd">
<!--磁盘保存路径-->
    <diskStore path="C:\app_study\ehcache"/>
    <defaultCache
            maxElementsInMemory="1000"
            maxElementsonDisk="10000000"
            eternal="false"
            overflowToDisk="true"
            timeToIdleseconds="120"
            timeToLiveseconds="120"
            diskExpiryThreadIntervalseconds="120"
            memorystoreEvictionPolicy="LRU" />
</ehcache>
```

4. 设置二级缓存的类型:mapper.xml文件中

```xml
<cache type="org.mybatis.caches.ehcache.EhcacheCache"/>
```

5. 加入logback日志

- 存在SLF4J时，作为简易日志的log4j将失效，此时我们需要借助SLF4J的具体实现logback来打印日志。
- 创建logback的配置文件logback.xml

# 十一.MyBatis的逆向工程

- 正向工程:先创建java实体类，由框架负责根据实体类生成数据库表。Hibernate是支持正向工程的。
- 逆向工程:先创建数据库表，由框架负责根据数据库表，反向生成如下资源:

1. Java实体类
2. Mapper接囗
3. Mapper映射文件

## 1.创建逆向工程的步骤

1.  添加依赖和插件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.uestc.mybatis</groupId>
    <artifactId>Mybatis_MBG</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging>
    <dependencies>
        <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.16</version>
        </dependency>

    </dependencies>
<!--控制Maven在构建过程中相关配置-->
    <build>
<!--构建过程中用到的插件-->
        <plugins>
<!--具体插件，逆向工程的操作是以构建过程中插件形式出现的-->
            <plugin>
                <groupId>org.mybatis.generator</groupId>
                <artifactId>mybatis-generator-maven-plugin</artifactId>
                <version>1.3.0</version>
                <dependencies>
                    <!-- https://mvnrepository.com/artifact/org.mybatis.generator/mybatis-generator-core -->
                    <dependency>
                        <groupId>org.mybatis.generator</groupId>
                        <artifactId>mybatis-generator-core</artifactId>
                        <version>1.3.2</version>
                    </dependency>

                    <!-- https://mvnrepository.com/artifact/com.mchange/c3p0 -->
                    <dependency>
                        <groupId>com.mchange</groupId>
                        <artifactId>c3p0</artifactId>
                        <version>0.9.5.2</version>
                    </dependency>
                    <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
                    <dependency>
                        <groupId>mysql</groupId>
                        <artifactId>mysql-connector-java</artifactId>
                        <version>5.1.3</version>
                    </dependency>
                </dependencies>
            </plugin>
        </plugins>
    </build>
    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
</project>
```

2. 创建MyBatis的核心配置文件

3. 创建逆向工程的配置文件:
   - 文件名必须是:generatorConfig.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
        PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
<generatorConfiguration>
<!--
targetRuntime:执行生成的逆向工程的版本
MyBatis3simple:生成基本的CRUD(清新简洁版)
MyBatis3:生成带条件的CRUD(奢华尊享版)
-->
    <context id="DB2Tables"  targetRuntime="MyBatis3">
        <!-- 数据库连接驱动类,URL，用户名、密码 -->
        <jdbcConnection driverClass="com.mysql.jdbc.Driver"
                        connectionURL="jdbc:mysql://localhost:4306/mybatis"
                        userId="root"
                        password="z123456">
        </jdbcConnection>
        <!-- javaBean的生成策略 -->
        <javaModelGenerator targetPackage="com.uestc.mybatis.bean" targetProject="./src/main/java">
            <!-- 在targetPackage的基础上，根据数据库的schema再生成一层package，最终生成的类放在这个package下，默认为false -->
            <property name="enableSubPackages" value="true"/>
            <!-- 设置是否在getter方法中，对String类型字段调用trim()方法:去除字符串前后的空格-->
            <property name="trimStrings" value="true"/>
        </javaModelGenerator>
        <!--SQL映射文件的生成策略-->
        <!-- 生成xml映射文件：包名(targetPackage)、位置(targetProject) -->
        <sqlMapGenerator targetPackage="com.uestc.mybatis.mapper" targetProject=".\src\main\resources">
            <property name="enableSubPackages" value="true"/>
        </sqlMapGenerator>
        <!--Mapper接口的生成策略-->
        <!-- 生成DAO接口：包名(targetPackage)、位置(targetProject) -->
        <javaClientGenerator type="XMLMAPPER" targetPackage="com.uestc.mybatis.mapper" targetProject=".\src\main\java">
            <property name="enableSubPackages" value="true"/>
        </javaClientGenerator>

        <!--逆向分析的表-->
        <!-- tableName设置为*号，可以对应所有表，此时不写domainobjectName -->
        <!--domainobjectName属性指定生成出来的实体类的类名-->
        <table tableName="t_emp" domainObjectName="Emp" />
        <table tableName="t_dept" domainObjectName="Dept" />
    </context>
</generatorConfiguration>
```

- 查询功能

```java
@Test
public void TestMBG() {
    InputStream is = null;
    try {
        is = Resources.getResourceAsStream("mybatis-config.xml");
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(is);
        SqlSession sqlSession = sqlSessionFactory.openSession(true);
        EmpMapper mapper = sqlSession.getMapper(EmpMapper.class);
        // 查询所有
        //            List<Emp> list = mapper.selectByExample(null);
        //            list.forEach(emp -> System.out.println(emp));
        // 根据条件查询
        EmpExample empExample = new EmpExample();
        empExample.createCriteria().andEmpNameEqualTo("Bob Brown").andAgeEqualTo(23);
        empExample.or().andAgeEqualTo(35);
        List<Emp> list2 = mapper.selectByExample(empExample);
        list2.forEach(emp -> System.out.println(emp));
    } catch (IOException e) {
        throw new RuntimeException(e);
    }
}
```

- 修改功能:QBC

```java
@Test
public void TestMBGUpdate() {
    InputStream is = null;
    try {
        is = Resources.getResourceAsStream("mybatis-config.xml");
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(is);
        SqlSession sqlSession = sqlSessionFactory.openSession(true);
        EmpMapper mapper = sqlSession.getMapper(EmpMapper.class);
        // 修改 -- updateByPrimaryKey有null 会将信息改为空
        //            mapper.updateByPrimaryKey(new Emp(15, "z15", 18, "M", "987@qq.com", null));
        // 修改 -- updateByPrimaryKeySelective有null sql语句不会出现该字段
        mapper.updateByPrimaryKeySelective(new Emp(15, "z15", null, "M", "987@qq.com", null));
    } catch (IOException e) {
        throw new RuntimeException(e);
    }
}
```

# 十二.分页插件

## 1.分页插件使用步骤

1. 添加依赖

```xml
<!-- https://mvnrepository.com/artifact/com.github.pagehelper/pagehelper -->
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper</artifactId>
    <version>5.2.0</version>
</dependency>
```

2. 配置分页插件:在MyBatis的核心配置文件中配置插件

```xml
<plugins>
    <plugin interceptor="com.github.pagehelper.PageInterceptor"/>
    </plugins>
```

3. 使用分页功能

```java

```

4. 获取分页信息

```java
PageInfo<Emp> info = new PageInfo<>(list, 5);
// navigatepageNums=[1, 2, 3] 展示分页的访问页码
/*
PageInfo{pageNum=2, pageSize=5, size=5, startRow=6, endRow=10, total=14, pages=3, list=Page{count=true, pageNum=2, pageSize=5, startRow=5, endRow=10, total=14, pages=3, reasonable=false, pageSizeZero=false}[Emp{eid=6, empName='Diana Evans', age=27, sex='F', email='diana@example.com', did=2}, Emp{eid=7, empName='Ethan Harris', age=29, sex='M', email='ethan@example.com', did=3}, Emp{eid=8, empName='Fiona Green', age=26, sex='F', email='fiona@example.com', did=1}, Emp{eid=9, empName='George Hill', age=31, sex='M', email='george@example.com', did=2}, Emp{eid=10, empName='Hannah Lee', age=24, sex='F', email='hannah@example.com', did=3}], prePage=1, nextPage=3, isFirstPage=false, isLastPage=false, hasPreviousPage=true, hasNextPage=true, navigatePages=5, navigateFirstPage=1, navigateLastPage=3, navigatepageNums=[1, 2, 3]}
常用数据:
pageNum:当前页的页码
pageSize:每页显示的条数
size:当前页显示的真实条数
total:总记录数
pages:总页数
prePage:上一页的页码
nextPage:下一页的页码
isFirstPage/isLastPage:是否为第一页/最后一页
hasPreviousPage/hasNextPage:是否存在上一页/下一页
navigatePages:导航分页的页码数
navigatepageNums:导航分页的页码，[1,2,3,4,5]
/
```

