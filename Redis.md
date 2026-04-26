# Redis入门
    Redis是一个基于内存的key-value结构的数据库
    - 基于内存存储，读写性能高
    - 适合存储热点新闻
## 修改配置文件redis.windows.conf来修改密码
requirepass 123456  #将密码设置为123456
1. 启动服务器 redis-server.exe redis.windows.conf
2. 启动客户端 redis-cli.exe -h localhost -p 6379 -a 123456  #连接服务器并输入密码
   
# Redis数据类型
## 5种常用数据类型
Redis存储的是key-value结构的数据，其中key 是 字符串类型，value有5种常用的数据类型：
1. String（字符串）普通字符串
2. Hash（哈希）也叫做散列，类似于HashMap结构
3. 列表list 按照插入顺序排序。可以有重复元素，类似LinkedList
4. 集合set 无序集合，没有重复元素，类似HashSet
5. 有序集合sorted set/zset 集合种每个元素关联一个分数，根据分数升序排序，没有重复元素
## Redis常用命令
1. 字符串类型常用命令
   Redis字符串类型常用命令:
   - SET key value 设置指定key的值
   - GET key 获取指定key的值
   - SETEX key seconds value 设置指定Key的值，并将key的过期时间设为seconds秒
   - SETNX key value 如果key不存在，则设置key的值为value
2. 哈希操作命令
    - HSET key field value 设置指定key的field的值value
    - HGET key field 获取指定key的field的值
    - HDEL key field 删除指定key的field
    - HKEYS key 获取哈希表种所有的字段
    - HVALS key 获取哈希表种所有的值 
3. 列表操作命令
    - LPUSH key value [value2]将值value插入到列表key的头部
    - LRANGE key start stop 获取列表指定范围内的元素
    - RPOP key 移除并获取列表最后一个元素
    - LLEN key 获取列表的长度
4. 集合操作命令
   Redis set 是string类型的无序集合。集合成员是唯一的，集合中不能出现重复的数据
   - SADD key member [member2] 将一个或多个成员元素加入到集合key当中
   - SMEMBERS key 获取集合key中的所有成员
   - SCARD key 获取集合key的基数(元素的数量)
   - SINTER key1 [key2] [key3] 交集
   - SUNION key1 [key2] [key3] 并集
   - SREM key member1 [member2] 从集合key中移除一个或多个成员元素
5. 有序集合操作命令
  Redis有序集合是string类型元素的集合，每个元素都关联一个double类型的分数。有序集合中的元素根据分数排序，分数可以相同。
  - ZADD key score1 member1 [score2 member2] 将一个或多个成员元素及其分数值加入到有序集合key中,按照分数score进行升序排列
  - ZRANGE key start stop [WITHSCORES] 获取有序集合key中指定范围内的元素，并可以同时获取元素的分数值
  - ZINCRBY key increment member 增加有序集合key中指定成员的分数值
  - ZREM key member [member] 移除有序集合中的一个或多个成员
6. 通用命令
   - KEYS pattern 查找所有符合给定模式的key
   - EXISTS key 检查给定的key是否存在
   - TYPE key 获取给定key的类型
   - DEL key1 [key2] 删除一个或多个key
  
# 在java中操作Redis
## Redis的java客户端
JEDIS\Lettuce\Spring Data Redis
## Spring Data Redis的使用方法
操作步骤：
1. 导入Spring Data Redis的maven坐标
   ```xml
   <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-redis</artifactId>
        </dependency>
    ```
2. 配置Redis数据源
   ```yml
   spring:
      redis:
        host: ${sky.redis.host }
        port: ${sky.redis.port}
        #password:123456
        database: ${sky.redis.database}
      redis:
        host: localhost
        port: 6379
        #password:123456
        database: 0
    ```
3. 编写配置类，创建RedisTemplate对象
   ```java
   @Configuration
@Slf4j
public class RedisConfiguration {
    @Bean
    public RedisTemplate redisTemplate (RedisConnectionFactory redisConnectionFactory ){
        log.info("开始创建redis模板对象");
        RedisTemplate redisTemplate =new RedisTemplate() ;
        //设置redis的连接工厂对象
        redisTemplate.setConnectionFactory(redisConnectionFactory );
        //设置redis key的序列化器
        redisTemplate .setKeySerializer(new StringRedisSerializer() );
        return redisTemplate ;
    }
}
    ```
4. 使用RedisTemplate对象操作Redis
   

# 店铺营业状态设置

