# 1.分模块设计与开发

# 2.继承与聚合
## 2.1 继承
-- 创建maven模块的tilas-parent,该工程为父工程，设置打包方式pom
-- 在子工程的pom.xml文件中，配置继承关系
-- 在父工程中配置各个工程共有的依赖，子工程会自动继承父工程依赖
```xml
<!-- 父工程pom.xml -->
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>3.2.5</version>
    <relativePath/> <!-- lookup parent from repository -->
  </parent>


  <groupId>com.itheima</groupId>
  <artifactId>tilas.parent</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>pom</packaging>
  <!-- 将打包方式设置为pom -->
```
```xml
 <!-- 子工程pom.xml -->
<parent>
    <groupId>com.itheima</groupId>
    <artifactId>tilas.parent</artifactId>
    <version>1.0-SNAPSHOT</version>
    <relativePath>../tlias-parent/pom.xml</relativePath>
    <!-- 相对路径，指明父工程的位置 -->
  </parent>

```
### 常见的打包方式
- jar: 普通模块打包，springboot项目基本上都是jar包内嵌tomcat
- war: web模块打包，需要部署在外部的tomcat服务器上
- pom: 父工程或聚合工程，该模块不屑代码仅仅进行依赖管理
### 版本锁定
- 在maven中，可以在父工程的pom文件中通过<dependencyManagement>来统一管理依赖版本，子工程引入依赖的时候，无需指定<version>版本号，父工程统一管理，变更依赖版本，只需在父工程中同一变更
```xml
<!--统一管理依赖版本-->
  <dependencyManagement>
    <dependencies>
      <dependency>
        <groupId>org.mybatis.spring.boot</groupId>
        <artifactId>mybatis-spring-boot-starter-test</artifactId>
        <version>4.0.1</version>
        <scope>test</scope>
      </dependency>

    </dependencies>
  </dependencyManagement>
  ```
  - dependencyManagement仅仅用来进行版本的管理，并没有引入依赖
  - 可在properties中集中定义版本属性，集中管理版本号
  ```xml
   <properties>
    <mybatis.version>4.0.1</mybatis.version>
  </properties>

  <!-- 引用的时候${mybatis.version} -->
  <groupId>org.mybatis.spring.boot</groupId>
        <artifactId>mybatis-spring-boot-starter-test</artifactId>
        <version>${mybatis.version}</version>
        <scope>test</scope>
  ```

  **<depenencyManagement>和<depenencies>的区别是什么**
  - <depenencyManagement>是同一管理依赖版本，不会直接依赖，还需要再子工程中引入需要的依赖，但无需指定版本号
  - <depenencies>是直接依赖，在父工程配置了依赖，子工程会直接继承下俩

## 2.2 聚合
- 聚合：将多个模块组织成一个整体，同时进行项目的构建
- 聚合工程，有且仅有一个pom文件，在项目中，父工程即是聚合工程
- maven中可以通过<modules>设置当前聚合工程所包含的子模块的名称
  ```xml
  <!--  聚合其他模块-->
  <modules>
    <module>../tails-pojo</module>
    <module>../tails-utils</module>
  </modules>
  ```
# 3.私服
依赖查找顺序：本地仓库 -> 私服 -> 中央仓库 -> 其他私服
- release发行版本：功能趋于稳定，当前停止更新，可以用于发行的版本，存储在私服中的RELEASE仓库中
- snapshot快照版本：功能开发中，当前最新版本，可以用于测试的版本，存储在私服中的SNAPSHOT仓库中
