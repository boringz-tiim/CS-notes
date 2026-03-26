# AOP 面向切面编程 (Aspect-Oriented Programming)
## 事务管理
### 事务的概念 
事务是指作为一个单元的一组操作，要么都成功，要么都失败。事务管理是指管理事务的整个生命周期，包括事务的开始、结束、提交、回滚等。事务管理是数据库系统的重要组成部分，它负责确保数据的一致性、完整性和正确性，并在出现系统故障或其他错误时提供恢复机制。

### 事务的特性
事务具有四个属性：原子性、一致性、隔离性、持久性。
- 原子性（Atomicity）：事务是一个不可分割的工作单位，事务中包括的诸操作要么都做，要么都不做。
- 一致性（Consistency）：事务必须是数据库从一个一致性状态变到另一个一致性状态。一致性与原子性是密切相关的。
- 隔离性（Isolation）：一个事务的执行不能被其他事务干扰。即一个事务内部的操作及使用的数据对并发的其他事务是隔离的，并发执行的各个事务之间不能互相干扰。
- 持久性（Durability）：持续性也称永久性，指一个事务一旦提交，它对数据库中数据的改变就应该是永久性的。接下来的其他操作或故障不应该对其有任何影响。

开启事务 start transaction/begin，提交事务 commit，回滚事务 rollback。

### @Transactional 注解
@Transactional 注解是 Spring 框架提供的用于声明事务的方法。它可以应用到方法或类上，用于指示 Spring 在方法调用前后自动地开启或关闭事务。

@Transactional 注解可以应用到类上，这样 Spring 就能为该类的所有公共方法配置事务属性。如果某个方法需要事务支持，可以直接在方法上添加 @Transactional 注解。

**但是，在默认情况下只有出现运行时异常即RuntimeException才会导致事务回滚，而出现CheckedException则不会导致事务回滚。如果希望对CheckedException也进行事务回滚，可以设置 rollbackFor 属性。**


```java
//出现所有的错误都进行回滚
@Transactional(rollbackFor = Exception.class)
```

-- 事务的传播行为：propagation 属性用于设置事务的传播行为。
- REQUIRED：如果当前存在事务，则加入该事务；如果当前没有事务，则创建一个新的事务。这是默认值。
-- SUPPORTS：如果当前存在事务，则加入该事务；如果当前没有事务，则以非事务的方式继续运行。
-- REQUIRES_NEW：创建一个新的事务，无论当前是否存在事务。
```java
//无论是成功耗时失败都要记录操作日志
@Transactional(propagation = Propagation.REQUIRES_NEW)
@Override
public void insert(DeptLog deptLog){
    deptLogDao.insert(deptLog);
}
```

## AOP 基础
### 导入AOP依赖
```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-aop</artifactId>
        </dependency>
```
### 编写AOP程序：针对于特定方法根据业务需要进行编程
```java
@Aspect
@Component
@Around("execution(* com.example.demo.service.*.*(..))")//切入点表达式，表示对com.example.demo.service包下的所有方法进行增强
 public Object recordTime(ProceedingJoinPoint joinPoint) throws Throwable {
        //1.记录开始时间
        long begin=System.currentTimeMillis();
        //2.调用原始方法运行

        Object result=joinPoint.proceed();
        //3.记录结束时间，计算方法执行耗时
       long end= System.currentTimeMillis();
        log.info("方法执行耗时:{}ms",end-begin);
        return result;
    }
```
### AOP术语
    -- 连接点：JoinPoint，表示一个方法的执行点，可以获取方法名、参数等信息。
    -- 通知:Advice,指哪些重复的逻辑，也就是共性功能
    -- 切入点表达式:Pointcut,用来匹配JoinPoint，决定是否要执行Advice。
    -- 切面:Aspect，是切入点表达式和Advice的集合。
    -- 引入:Introduction，是一种特殊的Advice，可以为一个类型引入新的方法或属性。
    -- 目标对象:Target,被增强的对象。
    -- 代理对象:Proxy,增强后的对象。
    -- 织入:Weaving,指把增强应用到目标对象来创建代理对象的过程。
    -- 切入点表达式:Pointcut,用来匹配JoinPoint，决定是否要执行Advice。
### 通知类型
    1. @Before: 在目标方法调用前执行
    2. @After: 在目标方法调用后执行
    3. @AfterReturning: 在目标方法正常返回后执行,有异常不会执行
    4. @AfterThrowing: 在目标方法抛出异常后执行
    5. @Around: 在目标方法调用前后执行，可以控制目标方法是否执行，返回值或异常是否继续抛出。** 需要自己调用ProceedingJoinPoint.proceed()方法来执行目标方法其他通知不需要考虑目标方法执行 **
1. ```java
  //抽取切入点表达式
    @Pointcut("execution(* com.example.tails.service.impl.DeptServicelmpl.*(..))")
    private void pt(){}
   @Before("pt()")
   ```
### 动态代理