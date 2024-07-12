# Maven

# Maven简介

- 现有的技术

<img src=".\Maven工具的MarkDown笔记图片\现有技术结构.png" alt="现有技术结构" style="zoom: 67%;" />

- 现有技术结构的缺点[why]

1. 一个项目就是一个工程
   - 项目庞大不适合继续使用package来划分模块。最好每一个模块对应一个工程，利于分工协作。
   - 借助于Maven就可以将一个项目拆分成多个工程。
2. 项目中需要的jar包必须手动“复制”、“粘贴”到WEB-INF/lib目录下
   - jar包重复出现在不同工程中
   - 借助Maven，可以将jar包仅仅保存在“仓库”中,有需要使用的工程“引用”这个文件接口，并不需要真的把jar包复制过来。
3. jar包需要提前准备/官网下载
   - 借助于Maven可以以一种规范的方式下载jar包。因为所有知名框架或第三方工具的jar包以及按照统一的规范存放在了Maven的中央仓库中。
4. 一个jar包依赖的其他jar包需要自己手动加入到项目中
   - Maven会自动将被依赖的jar包导入进来。

- Maven是什么[What]

1. Maven是一款服务于Java平台的自动化构建工具。
   - Make->Ant->Maven->Gradle
2. 构建管理：
   - 概念:以“Java源文件"、"框架配置文件"、"JSP"、"HTML"、“图片”等资源为“原材料”，去“生产”一个可以运行的项目的过程。

3. 依赖管理:

- Maven软件工作原理模型图

![Maven概念模型](.\Maven工具的MarkDown笔记图片\Maven概念模型.png)

# Maven安装和配置

- Maven文件结构

1. bin:含有Maven的运行脚本
2. boot:含有plexus-classworlds类加载器框架
3. conf:含有Maven的核心配置文件
4. lib:含有Maven运行时所需要的Java类库
5. LICENSE、NOTICE、README.txt:针对Maven版本，第三方软件等简要介绍

- Maven环境配置

1. 配置MAVEN_HOME

![Maven_环境配置1](.\Maven工具的MarkDown笔记图片\Maven_环境配置1.png)

2. 配置Path

![Maven_环境配置2](.\Maven工具的MarkDown笔记图片\Maven_环境配置2.png)

3. 也可以直接在Path配置添加Maven/bin目录

## Maven功能配置

- 功能配置

1. 通过修改maven/conf/settings.xml配置文件，来修改maven的一些默认配置。主要修改三个配置：

2. 依赖本地缓存位置(本地仓库位置)

   ```xml
     <!--无中文目录-->
   <localRepository>C:\app_study\MavenLocalRepository</localRepository>
   ```

3. maven下载镜像/国内阿里镜像

   ```xml
   <mirror>
         <id>alimaven</id>
         <mirrorOf>central</mirrorOf>
         <name>aliyun maven</name>
         <url>https://maven.aliyun.com/nexus/content/groups/public/</url>
         <blocked>true</blocked>
       </mirror>
   ```

4. maven选用编译项目的jdk版本

   ```java
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
   ```

## IDEA配置本地Maven软件

- 基本使用流程

1. 创建Empty project
2. 设置Maven
   - Setting->Build, Execution, Deployment->Build Tools->Maven
   - 设置Maven home path/User settings file/Local repository:

# 基于IDEA创建Maven工程

## 1概念梳理Maven工程的GAVP

Maven 中的 GAVP 是指 Groupld、Artifactld、Version、Packaging 等四个属性的缩写，其中前三个是必要的,而 Packaging 属性为可选项。这四个属性主要为每个项目在maven仓库中做一个标识，类似人的姓-名!有了具体标识，方便后期项目之间相互引用依赖等!

1. GrouplD 格式:com.{公司/BU }.业务线.[子业务线]，最多 4级。
   - com.taobao.tddl或com.alibaba.sourcing.multilang
2. ArtifactlD 格式:产品线名-模块名。语义不重复不遗漏，先到仓库中心去查证一下
   - 正例:tc-client/uic-api/tair-tool / bookstore
3. Version版本号格式推荐:主版本号.次版本号.修订号
   - 1)主版本号:当做了不兼容的 API修改，或者增加了能改变产品方向的新功能。
   - 2)次版本号:当做了向下兼容的功能性新增(新增类、接口等)
   - 3)修订号:修复 bug，没有修改方法签名的功能加强，保持 AP| 兼容性。
   - 例如:初始→1.0.0 修改bug→ 1.0.1 功能调整 → 1.1.1等
4. 指示将项目打包为什么类型的文件，idea根据packaging值，识别maven项目类型!
   - packaging 属性为jar(默认值)，代表普通的java工程，打包以后是,jar结尾的文件
   - packaging 属性为 war，代表]ava的web工程，打包以后.war结尾的文件,
   - packaging 属性为 pom，代表不会打包，用来做继承的父工程。

5. 首次使用会保存，需要下载maven的支持插件

## 2ldea构建Maven Java SE工程

1. 创建工程

![Maven_创建SE工程1](.\Maven工具的MarkDown笔记图片\Maven_创建SE工程1.png)

2. New Module
3. pom.xml内添加依赖
   - maven官网获取包的标签

## 3Idea构建Maven Java Web工程

- 手动创建

1. 创建SE工程

2. 添加Web

   - 手动添加：在Project Structure/Modules中添加web目录

   - 配置/依赖文件添加：pom.xml中添加以下标签，Project Structure(刷新)会自动生成web目录：分别设置wen.xml配置文件和资源路径

     - 资源路径自动生成
     
     ```xml
     <packaging>war</packaging>
     ```

     - 手动添加web.xml文件

       ![Maven_创建web工程](.\Maven工具的MarkDown笔记图片\Maven_创建web工程.png)
     
       - web.xml建议保存在Web Resource Directories的默认目录下

- JBLJavaToWeb插件可以一键完成
  - webapp文件必须有小蓝点

- 直接创建Maven工程：web.xml的比较低

![Maven_创建web工程3](.\Maven工具的MarkDown笔记图片\Maven_创建web工程3.png)

- 设置tomcat方式与web工程设置方式一致

## 4Maven工程项目结构说明

![Maven_文件结构说明](.\Maven工具的MarkDown笔记图片\Maven_文件结构说明.png)

# 基于IDEA进行Maven工程构建

## 1.构建概念和构建过程

- 项目构建是指将源代码、依赖库和资源文件等转换成可执行或可部署的应用程序的过程，在这个过程中包括编译源代码、链接依赖库、打包和部署等多个步骤。
- 项目构建是软件开发过程中至关重要的一部分，它能够大大提高软件开发效率，使得开发人员能够更加专注于应用程序的开发和维护，而不必关心应用程序的构建细节。
- 同时，项目构建还能够将多个开发人员的代码汇合到一起，并能够自动化项目的构建和部署，大大降低了项目的出错风险和提高开发效率。常见的构建王具包括 Maven、Gradle、Ant等。

![Maven_构建过程](.\Maven工具的MarkDown笔记图片\Maven_构建过程.png)

## 2.命令方式项目构建

| 命令             | 描述                                                         |
| :--------------- | ------------------------------------------------------------ |
| mivn compile     | **编译**项目，生成target文件                                 |
| mvn package      | 打包项目，生成jar(java工程)或war(web工程)文件保存在target目录 |
| mvn clean        | **清理**编译或打包后的项目结构                               |
| mvn install      | 打包后上传到maven本地仓库                                    |
| mvn deploy       | 只打包，上传到maven私服仓库                                  |
| mvn site         | 生成站点                                                     |
| mvn test         | 执行测试源码                                                 |
| mvn test-compile | 编译测试源码                                                 |

- Maven通过是否是test开头识别测试方法，建议类名以test结尾

- surefire-reports记录的测试结果
- mvn package只对核心程序打包，测试程序不打包

- mvn打war包可能出现插件和jdk版本不匹配

## 3.构建插件、命令、生命周期命令之间关系

- 构建生命周期

1. 触发周期后的命令会自动触发周期前的命令
   - 如 mvn clear package
   - 包含命令 clear compile - test - package - install - deploy

# 基于IDEA 进行Maven依赖管理

## 1.依赖管理概念

1. Maven 依赖管理是 Maven 软件中最重要的功能之一。
2. 我们通过定义 POM 文件，Maven 能够自动解析项目的依赖关系，并通过 Maven 仓库自动下载和管理依赖，从而
   避免了手动下载和管理依赖的繁琐工作和可能引发的版本冲突问题。

## 2.Maven工程核心信息配置和解读(GAVP)

- pom.xml配置文件

![Maven_GAVP信息](.\Maven工具的MarkDown笔记图片\Maven_GAVP信息.png)

## 3.Maven工程依赖管理配置

1. Maven中央仓库查找依赖

2. 添加到dependencies标签中

3. < scope >标签表示依赖范围(有些依赖不存在依赖范围(标签) -- 通常不建议修改

4. 自定义属性：设置一系列相同版本依赖的版本

   - < properties >标签中添加 ：依赖很多时，只用管理properties中的标签即可

     ```xml
     <spring.version>6.0.2</junit.version>
     ```

   - 修改version标签

     ```xml
     <version>${spring.version}</version>
     ```

     

## 4.依赖范围

- 通过设置坐标的依赖范围(scope)，可以设置 对应jar包的作用范围:编译环境、测试环境、运行环境

| 依赖范围     | 描述                                                         |
| ------------ | ------------------------------------------------------------ |
| **compile**  | **编译**依赖范围，scope 元素的缺省值(**默认值**)。使用此依赖范围的 Maven 依赖，对于三种 classpath 均有效，即该 Maven 依赖在上述三种 classpath 均会被引入。例如，log4j在编译、测试、运行过程都是必须的。 |
| **test**     | **测试**依赖范围。使用此依赖范围的 Maven 依赖，只对测试 classpath 有效。例如，lunit 依赖只有在测试阶段才需要。 |
| **provided** | 已提供依赖范围。使用此依赖范围的 Maven 依赖，只对**编译** classpath 和**测试** classpath 有效。例如，servlet-api依赖对于编译、测试阶段而言是需要的，但是运行阶段，由于**外部容器已经提供(服务器提供)**，故不需要 Maven 重复引入该依赖。 |
| runtime      | **运行时依赖范围**。使用此依赖范围的 Maven 依赖，只对**测试** classpath、**运行** classpath 有效例如，JDBC驱动实现依赖，其在编译时只需JDK提供的JDBC接口即可，只有测试、运行阶段才需要实现了JDBC 接口的驱动。 |
| system       | **系统**依赖范围，其效果与 **provided 的依赖范围一致**。其用于添加非 Maven 仓库的本地依赖，通过依赖元素 dependency 中的 systemPath 元素指定本地依赖的路径。鉴于使用其会导致项目的可移植性降低，一般不推荐使用。 |
| import       | 导入依赖范围，该依赖范围只能与**dependencyManagement** 元素配合使用，其功能是将目标pom.xml文件中 dependencyManagement 的配置导入合并到当前 pom.xml的dependencyManagement中。合并父工程和子工程的依赖。 |

## 5.Maven工程依赖下载失败错误解决(重点)

- 在使用 Maven 构建项目时，可能会发生依赖项下载错误的情况，主要原因有以下几种:

1. 下载依赖时出现**网络故障或仓库服务器宕机**等原因，导致无法连接至 Maven 仓库，从而无法下载依赖。
2. 依赖项的**版本号或配置文件**中的版本号错误，或者依赖项没有正确定义，导致 Maven 下载的依赖项与实际需要的不一致，从而引发错误。
3. 本地 Maven **仓库或缓存被污染或损坏**，导致 Maven 无法正确地使用现有的依赖项。

- 解决方案:

1. 检査网络连接和 Maven 仓库服务器状态。
2. 确保依赖项的版本号与项目对应的版本号匹配，并检査 POM 文件中的依赖项是否正确。
3. 清除抓地, Maven 仓库缓存(lastUpdated 文件)，因为只要存在lastupdated缓存文件，刷新也不会重新下载。本地仓库中，根据依赖的gav属性依次向下查找文件夹，最终删除内部的文件，刷新重新下载即可!
   例如: pom.xml依赖
4. 清除lastUpdated文件的操作写在一个**脚本文件**中。

## 6.Maven工程Build构建配置

- 项目构建是指将源代码、依赖库和资源文件等转换成可执行或可部署的应用程序的过程，在这个过程中包括编译源代码、链接依赖库、打包和部署等多个步骤。

- 默认情况下，构建不需要额外配置，都有对应的缺省配置。
- resources文件下的配置文件都会打包，打包需要额外的配置文件要设置< resources >标签

```xml
<build>
    <!--    自定义名称    -->
    <finalName>maven_java-1.0</finalName>
    <resources>
        <resource>
            <directory>src/main/java</directory>
            <includes>
                <!--      设置包含的资源类型：所有包下的所有.xml文件          -->
                <include>**/*.xml</include>
            </includes>
        </resource>
    </resources>
</build>
```

- 配置依赖插件

1. dependencies标签下引入开发需要的jar包!我们可以在build/plugins/plugin标签引入插件!
2. 常用的插件:修改jdk版本、tomcat插件、mybatis分页插件、mybatis逆向工程插件等等!

```xml
<!--      添加插件：在Maven目录下直接运行tomcat      -->
<plugins>
    <!--      tomcat插件      -->
    <plugin>
        <groupId>org.apache.tomcat.maven</groupId>
        <artifactId>tomcat7-maven-plugin</artifactId>
        <version>2.2</version>
        <configuration>
            <port>8090</port>
            <path>/</path>
            <uriEncoding>UTF-8</uriEncoding>
            <server>tomcat7</server>
        </configuration>
    </plugin>
</plugins>
```

# Maven依赖传递和依赖冲突

## Maven依赖传递特性

- 依赖传递基本概念

假如有Maven项目A，项目B依赖A，项目C依赖B。那么我们可以说(依赖A。也就是说，依赖的关系为:C->B->A，那么我们执行项目C时，会自动把B、A都下载导入到C项目的jar包文件夹中，这就是依赖的传递性。

- 传递的原则
  在 A依赖 B，B 依赖C的前提下，C是否能够传递到 A，取决于B依赖C时使用的依赖范围以及配置

1. B 依赖C时使用 compile 范围:可以传递
2. B 依赖C时使用 **test 或 provided 范围:不能传递**，所以需要这样的 jar 包时，就必须在需要的地方明确配置依赖才可以。
3. B 依赖C时，若配置了以下标签，则不能传递

```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid</artifactid>
    <version>1.2.15</version>
    <!--  optional标签阻止依赖传递      -->
    <optional>true</optional>
</dependency>
```

- 依赖传递终止

1. 非compile范围进行依赖传递
2. 使用optional配置终止传递
3. 依赖冲突(传递的依赖已经存在)

## Maven依赖冲突特性

- 依赖冲突：当直接引用或者间接引用出现了相同的iar包。一个项目就会出现相同的重复jar包，这就算作冲突。
- 依赖冲突避免出现重复依赖，并且终止依赖传递!

![Maven_依赖冲突](.\Maven工具的MarkDown笔记图片\Maven_依赖冲突.png)

- 解决依赖冲突(如何选择重复依赖)方式:

1. 自动选择原则

   - **路短优先**原则(**第一原则**)
     A->B->C->D->E->X(version 0.0.1)
     A->F->X(version 0.0.2)
     则A依赖于X(version 0.0.2)。

   - 依赖**路径长度相同**情况下，则“**先声明优先**”(第二原则)
     A->E->X(version 0.0.1)
     A->F->X(version 0.0.2)
     在< depencies> < / depencies >中，idea中同时变灰色，先声明的，路径相同，会优先选择!

     

![Maven_依赖冲突_第二原则](.\Maven工具的MarkDown笔记图片\Maven_依赖冲突_第二原则.png)

2. 手动排除:< exclusions >标签

```xml
<dependencies>
    <dependency>
        <groupId>com.atguigu.maven</groupId>
        <artifactId>maven B</artifactId>
        <version>1.0-SNAPSHOT</version>
        <!--依赖排除-->
        <exclusions>
            <exclusion>
                <groupId>com.alibaba</groupId>
                <artifactId>druid</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
</dependencies>
```



# Maven工程继承和聚合关系

## Maven工程继承关系

- 继承概念

Maven 继承是指在 Maven 的项目中，让一个项目从另一个项目中**继承配置信息**的机制。继承可以让我们在多个项目中共享同一配置信息，简化项目的管理和维护工作。

- 继承作用：在父工程中统一管理项目中的依赖信息。

1. 背景:

   - 对一个比较大型的项目进行了模块拆分。
   - 一个project 下面，创建了很多个module。
   - 每一个 module 都需要配置自己的依赖信息。

2. 需求是:

   - 在每一个 modue 中各自维护各自的依赖信息很容易发生出入，不易统一管理。
   - 使用同一个框架内的不同 jar 包，它们应该是同一个版本，所以整个项目中使用的框架版本需要统一。
   - 使用框架时所需要的 jar 包组合(或者说依赖信息组合)需要经过长期摸索和反复调试，最终确定一个可用组合。这个耗费很大精力总结出来的方案不应该在新的项目中重新摸索。
   - 通过在父工程中为整个项目维护依赖信息的组合既保证了整个项目使用规范、准确的jar 包;又能够将以往的经验沉淀下来，节约时间和精力。

3. 继承语法

   - 父工程

   ```xml
   <!--  由于父工程不需要参与打包(没有Java文件)，因此打包方式pom  -->
   <!--  可以直接删除父工程的src文件  -->
       <packaging>pom</packaging>
   ```

   - 子工程：在父工程的module下创建

   ```java
   <!--  设置父工程的坐标信息(自动生成)  -->
       <parent>
           <groupId>com.uestc.maven</groupId>
           <artifactId>maven_parent</artifactId>
           <version>1.0-SNAPSHOT</version>
       </parent>
   ```

- 父工程中的< dependencies >依赖会无条件继承给子工程。所有通常使用< dependencyManagement >管理< dependencies >

```xml
<!--父工程中的dependency管理标签-->
    <dependencyManagement>
        <dependencies>
            <!-- https://mvnrepository.com/artifact/org.junit.jupiter/junit-jupiter-api -->
            <dependency>
                <groupId>org.junit.jupiter</groupId>
                <artifactId>junit-jupiter-api</artifactId>
                <version>5.9.2</version>
                <scope>test</scope>
            </dependency>
            <!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api -->
            <dependency>
                <groupId>javax.servlet</groupId>
                <artifactId>javax.servlet-api</artifactId>
                <version>4.0.1</version>
                <scope>provided</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
```

```xml
<!--  子类工程设置需要依赖的包，不用选择版本<groupId><artifactId>  -->
<dependencies>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
    </dependency>
    <!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api -->
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
    </dependency>
</dependencies>
```

## Maven工程聚合关系

- 聚合概念
  Maven 聚合是指将多个项目组织到一个父级项目中，以便**一起构建和管理的机制**。聚合可以帮助我们更好地管理一组相关的子项目，同时简化它们的构建和部署过程。
- 聚合作用：对父工程进行操作，子工程也会进行同步的操作

1. 管理多个子项目:通过聚合，可以将多个子项目组织在一起，方便管理和维护。
2. 构建和发布一组相关的项目:通过聚合，可以在一个命令中构建和发布多个相关的项目，简化了部署和维护工作。
3. 优化构建顺序:通过聚合，可以对多个项目进行顺序控制，避免出现构建依赖混乱导致构建失败的情况。
4. 统一管理依赖项:通过聚合，可以在父项目中管理公共依赖项和插件，避免重复定义。

- 聚合语法：父项目中包含的子项目列表。

```xml
<project>
    <groupId>com.example</groupId>
    <artffactId>parent-project</artifactId>
    <packaging>pom</packaging>
    <version>1.0.0</version>
    <!--  idea会自动生成  -->
    <modules>
        <!--  module内添加子工程的目录/路径  -->
        <module>child-project1</module>
        <module>child-project2</module>
    </modules>
</project>
```

# Maven私服

## 1Maven私服简介

- 私服简介

Maven 私服是一种特殊的Maven远程仓库，它是架设在**局域网**内的仓库服务，用来代理位于外部的远程仓库(中央仓库、其他远程公共仓库)。

- 建立了 Maven 私服后，当局域网内的用户需要某个**构件/依赖**时，会按照如下顺序进行请求和下载。

1. 请求**本地仓库**，若本地仓库不存在所需构件，则跳转到第 2步;
2. 请求 **Maven 私服**，将所需构件下载到本地仓库，若私服中不存在所需构件，则跳转到第3步。
3. 请求**外部的远程仓库**，将所需构件下载并**缓存到 Maven 私服**，若外部远程仓库不存在所需构件，则 Maven 直接报错。
4. 此外，一些无法从外部仓库下载到的构件，也能从本地上传到私服供其他人使用。

![Maven_私服工作过程](.\Maven工具的MarkDown笔记图片\Maven_私服工作过程.png)

- Maven私服的优势

1. 节省外网带宽
   消除对外部远程仓库的大量重复请求(会消耗很大量的带宽)，降低外网带宽压力。
2. 下载速度更快
   Maven私服位于局域网内，从私服下载构建更快更稳定。
3. 便于部署第三方构件
   有些构件无法从任何一个远程仓库中获得(如:公司或组织内部的私有构件、Oracle的IDBC驱动等)，建立私服之后，就可以将这些构件部署到私服中，供内部Maven项目使用。
4. 提高项目的稳定性，增强对项目的控制
   如果不建立私服，那么Maven项目的构件就高度依赖外部的远程仓库，若外部网络不稳定，则项目的构建过程也会变得不稳定。建立私服后，即使外部网络状况不佳甚至中断，只要私服中已经缓存了所需的构件，Maven也能够正常运行。私服软件(如:Nexus)提供了很多控制功能(如:权限管理、RELEASE/SNAPSHOT版本控制等)，可以对仓库进行一些更加高级的控制。
5. 降低中央仓库得负荷压力
   由于私服会缓存中央仓库得构件，避免了很多对中央仓库的重复下载，降低了中央仓库的负荷





## 2私服软件:Nexus

- Nexus安装

1. 解压置配中文目录
2. cmd管理cd置安装目录
3. nexus /run 启动

- 配置

1. sign up 设置密码
2. 选择是否允许匿名

- Nexus上的各种仓库

![Maven_Nexus_仓库](.\Maven工具的MarkDown笔记图片\Maven_Nexus_仓库.png)

| 仓库类型 | 说明                                         |
| -------- | -------------------------------------------- |
| proxy    | 某个远程仓库的代理                           |
| group    | 存放:通过 Nexus 获取的第三方 jar 包          |
| hosted   | 存放:本团队其他开发人员部署到 Nexus 的jar 包 |

| 仓库说明        | 说明                                                         |
| --------------- | ------------------------------------------------------------ |
| maven-central   | Nexus 对 Maven 中央仓库的代理                                |
| maven-public    | Nexus 默认创建，供开发人员下载使用的组仓库                   |
| maven-releases  | Nexus 默认创建，供开发人员部署自己jar 包的宿主仓库 要求 releases 版本 |
| maven-snapshots | Nexus 默认创建，供开发人员部署自己jar 包的宿主仓库 要求 snapshots 版本 |

## 3通过 Nexus 下载 jar 包

- 修改Maven的配置文件

1. 创建新的本地仓库地址

```xml
<localRepository>C:\app_study\MavenLocalRepositoryNexus</localRepository>
```

2. 修改原来的aliyun镜像地址为自己的Nexus地址

![Maven_Nexus_仓库地址](.\Maven工具的MarkDown笔记图片\Maven_Nexus_仓库地址.png)

```xml
<mirror>
    <id>nexus-mine</id>
    <name>Nexus mine</name>
    <url>http://localhost:8081/repository/maven-public/</url>
    <mirrorOf>central</mirrorOf>
</mirror>
```

3. 若允许匿名访问到此即可。禁止了匿名访问则需要配置

```xml
<server>
    <!--   id对应mirror中的id   -->
    <id>nexus-mine</id>
    <username>admin</username>
    <password>z123456</password>
</server>
```

- 若Nexus默认的远程仓库下载缓慢，可以替换为aliyun

1. setting -> Repositories -> Remote storage
2. 修改为新的地址

## 4将jar 包部署到 Nexus

- 在项目的pom.xml文件中设置，通过mvn deploy 部署。

```xml
<distributionManagement>
    <snapshotRepository>
        <!--      与上传的私服id一致      -->
        <id>nexus-mine</id> 
        <name>Nexus Snapshot</name>
        <url>http://localhost:8081/repository/maven-snapshots/</url>
    </snapshotRepository>
</distributionManagement>
```



## 5.引用别人部署的 jar 包

- maven工程/项目中配置:

```xml
<repositories>
    <repository>
        <id>nexus-mine</id>
        <name>nexus-mine</name>
        <url>http://localhost:8081/repository/maven-snapshots/</url>
        <snapshots>
            <enabled>true</enabled>
        </snapshots>
        <releases>
            <enabled>true</enabled>
        </releases>
    </repository>
</repositories>
```

# Maven综合案例

## 1.项目需求和结构分析

![Maven_Nexus案例_需求分析](.\Maven工具的MarkDown笔记图片\Maven_Nexus案例_需求分析.png)

- 需求案例:搭建一个电商平台项目，该平台包括用户服务、订单服务、通用工具模块等
- 项目架构:

1. 用户服务:负责处理用户相关的逻辑，例如用户信息的管理、用户注册、登录等
   - spring-context 6.0.6
   - spring-core 6.0.6
   - spring-beans 6.0.6
   - common-service
2. 订单服务:负责处理订单相关的逻辑，例如订单的创建、订单支付、退货、订单查看等。
   - spring-context 6.0.6
   - spring-core 6.0.6
   - spring-beans 6.0.6
   - spring-security 6.0.6
   - common-service
3. 通用模块:负责存储其他服务需要通用工具类，其他服务依赖此模块。
   - commons-io 2.11.0
   - junit 5.9.2

## 2.项目搭建和统一构建

- 创建父工程，父工程目录下创建子工程，设置对应的依赖和依赖关系/设置依赖的继承权限

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>com.uestc</groupId>
        <artifactId>micro-shop</artifactId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <packaging>war</packaging>

    <artifactId>common-service</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
        </dependency>
        <dependency>
            <groupId>commons-io</groupId>
            <artifactId>commons-io</artifactId>
            <optional>true</optional>
        </dependency>
        <!--配置junit，继承父工程版本-->
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-api</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

</project>
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>com.uestc</groupId>
        <artifactId>micro-shop</artifactId>
        <version>1.0-SNAPSHOT</version>
    </parent>

    <artifactId>order-service</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
    <dependencies>
        <dependency>
            <groupId>com.uestc</groupId>
            <artifactId>common-service</artifactId>
            <version>1.0-SNAPSHOT</version>
        </dependency>
    </dependencies>

</project>
```



- 父工程聚合，ideal自动完成

```xml
<packaging>pom</packaging>
<modules>
    <module>common-service</module>
    <module>User-service</module>
    <module>order-service</module>
</modules>
```

