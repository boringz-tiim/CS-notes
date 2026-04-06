# 配置
## Spring Boot 中支持三种格式的配置文件
   - application.properties server.port=8081
   - application.yml (主流)
         server:
     port: 8082
    - application.yaml
         server:
         port: 8083
### 除了支持配置文件配置属性，还支持java系统属性和命令行参数的方式进行属性配置
- java系统属性：-Dspring.profiles.active=dev
- 命令行参数：--spring.profiles.active=dev
        
# Bean 管理
## 获取bean
```java
//注入IOC容器对象
 @Autowired
    private ApplicationContext applicationContext;

    @Test
    public void testGetBean(){
        //根据bean的名称获取
        DeptController bean1= (DeptController) applicationContext.getBean("deptController");
        System.out.println(bean1);
        //根据bean的类型获取
        DeptController bean2=applicationContext.getBean(DeptController.class);

        System.out.println(bean2);
        //根据bean的名称以及类型进行获取
        DeptController bean3=applicationContext.getBean("deptController",DeptController.class);
        System.out.println(bean3);


    }
```
## bean的作用域
Spring 支持五种作用域，后三种在wen环境中才生效,只关注前两种即可
- singleton：单例模式，在整个spring容器中，只会存在一个bean实例，默认就是singleton，同名称的bean只有一个实例
- prototype：原型模式，每次获取bean都会产生一个新的实例，每次使用bean的时候都会创建新的实例
- request：请求域，在一次请求中，只会存在一个bean实例，不同请求之间，bean实例不同
- session：会话域，在一次会话中，只会存在一个bean实例，不同会话之间，bean实例不同
- application：应用域，在整个web应用中，只会存在一个bean实例，不同web应用之间，bean实例不同

### 可以通过@Scope注解来指定bean的作用域
```java
//放在controller类上，表示该类中的所有bean的作用域都是prototype
@Scope("prototype")//每次都会实例化一个新的bean
```
```java
@Test
public void testScope(){
    //获取bean
    for(int i=0;i<10;i++){
        DeptController bean=applicationContext.getBean(DeptController.class);
        System.out.println(bean);
    }
}
```
## 第三方bean
    如果要管理的bean来自第三方（不是自定义的），是无法用@Component及衍生注解声明bean的，就要用到@Bean注解
    ```java
     //声明第三方bean
    @Bean//将当前方法的返回值对象交给IOC容器，成为IOC容器bean
    //通过@Bean注解的name/value属性指定bean名称，如果未指定，默认是方法名
    ```
# SpringBoot 原理
起步依赖，自动配置
## 自动配置原理
```java
//引入第三方提供依赖
<dependency>
    <groupId>com.example</groupId>
    <artifactId>itheima-utils</artifactId>
    <version>1.0.0</version>
</dependency>

