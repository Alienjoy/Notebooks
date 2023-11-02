# Redis

一个数据库，非关系型数据库，项目暂时不需要

也是用json（字符串）来存储到Redis中去

```java
public String findAllJson() {
        //1.1获取redis客户端连接
        Jedis jedis = JedisPoolUtil.getJedis();

        String province = jedis.get("province");
        if (province==null||province.length()==0){
            System.out.println("没有数据，需要进行查询数据库");
            //redis中没有数据
            ProvinceDao provinceDao = new ProvinceDaoImpl();
            //从数据中查询
            List<Province> list = provinceDao.findAll();
            //将list序列化为json
            ObjectMapper mapper = new ObjectMapper();
            try {
                province = mapper.writeValueAsString(list);
            } catch (JsonProcessingException e) {
                e.printStackTrace();
            }
            //将json存入到redis中
            jedis.set("province",province);

        }else {
            //redis中有数据，不需要进行查询，直接返回就行
            System.out.println("有数据，不需要进行查询。");
        }
        return province;
    }
```





1. Homebrew安装https://gitee.com/cunkai/HomebrewCN
2. redis安装 https://blog.csdn.net/qq_37603434/article/details/113842407
2. Homebrew安装 redis安装https://blog.csdn.net/realize_dream/article/details/106227622

<img src="/Users/zhangshuheng/Desktop/Notebooks/JAVA/javaWeb/15Redis.assets/截屏2021-09-19 下午3.34.53.png" alt="截屏2021-09-19 下午3.34.53" style="zoom:50%;" />

## 命令操作

1. 开启redis服务器`redis-server`，不要关闭，或者可是使用brew启动`brew services start redis`
1. 打开另一个终端，进入 Redis 客户端：redis-cli
1. **关闭 Redis 客户端与服务器的连接：QUIT**
1. 利用redis-cli程序关闭redis服务器： **redis-cli shutdown**

### 命令

五种数据类型 S L H实例化String set sortset list hash

基本语法：COMMAND KEY_NAME [value] 就是一个命令，一个key

```
 字符串类型 string
		1. 存储： set key value
			如 set name zhangshuheng
		2. 获取： get key
			如get name
		3. 删除： del key
			如 del name
```

```
哈希类型 hash
		1. 存储： hset key field value(其中file 就相当于hashmap中的key)
			127.0.0.1:6379> 如 hset myhashmap username zhangshuheng 
			(integer) 1
			127.0.0.1:6379> hset myhashmap password 123
			(integer) 1
			也可以使用hmset 一个添加多个field value
			如 hmset myhashmap name zhangshuheng age 24
		2. 获取： 
			* hget key field: 获取指定的field对应的值
				127.0.0.1:6379> hget myhash username
				"lisi"
			* hgetall key：获取所有的field和value
				127.0.0.1:6379> hgetall myhash
				1) "username"
				2) "lisi"
				3) "password"
				4) "123"
				
		3. 删除： hdel key field
			127.0.0.1:6379> hdel myhash username
			(integer) 1
```

```
列表类型 list:可以添加一个元素到列表的头部（左边）或者尾部（右边），可以重复
		1. 添加：
			1. lpush key value: 将元素加入列表左表
				
			2. rpush key value：将元素加入列表右边
				
				127.0.0.1:6379> lpush myList a
				(integer) 1
				127.0.0.1:6379> lpush myList b
				(integer) 2
				127.0.0.1:6379> rpush myList c
				(integer) 3
		2. 获取：
			* lrange key start end ：范围获取
				127.0.0.1:6379> lrange myList 0 -1
				1) "b"
				2) "a"
				3) "c"
		3. 删除：
			* lpop key： 删除列表最左边的元素，并将元素返回
			* rpop key： 删除列表最右边的元素，并将元素返回
```

```
集合类型 set ： 不允许重复元素
		1. 存储：sadd key value
			127.0.0.1:6379> sadd myset a
			(integer) 1
			127.0.0.1:6379> sadd myset a
			(integer) 0
		2. 获取：smembers key:获取set集合中所有元素
			127.0.0.1:6379> smembers myset
			1) "a"
		3. 删除：srem key value:删除set集合中的某个元素	
			127.0.0.1:6379> srem myset a
			(integer) 1
```

```
有序集合类型 sortedset：不允许重复元素，且元素有顺序.每个元素都会关联一个double类型的分数。redis正是通过分数来为集合中的成员进行从小到大的排序。

		1. 存储：zadd key score value
			127.0.0.1:6379> zadd mysort 60 zhangsan
			(integer) 1
			127.0.0.1:6379> zadd mysort 50 lisi
			(integer) 1
			127.0.0.1:6379> zadd mysort 80 wangwu
			(integer) 1
		2. 获取：zrange key start end [withscores]
			127.0.0.1:6379> zrange mysort 0 -1
			1) "lisi"
			2) "zhangsan"
			3) "wangwu"

			127.0.0.1:6379> zrange mysort 0 -1 withscores
			1) "zhangsan"
			2) "60"
			3) "wangwu"
			4) "80"
			5) "lisi"
			6) "500"
		3. 删除：zrem key value
			127.0.0.1:6379> zrem mysort lisi
			(integer) 1
```

```
通用命令，其中keyName就是要替换成redis key-value的key
		1. keys * : 查询所有的键
		2. type keyName ： 获取键对应的value的类型
		3. del keyName：删除指定的key value
```

## 持久化方式

```
	1. RDB：默认方式，不需要进行配置，默认就使用这种机制
			* 在一定的间隔时间中，检测key的变化情况，然后持久化数据
			1. 编辑redis.windwos.conf文件
				#   after 900 sec (15 min) if at least 1 key changed
				save 900 1
				#   after 300 sec (5 min) if at least 10 keys changed
				save 300 10
				#   after 60 sec if at least 10000 keys changed
				save 60 10000
				
			2. 重新启动redis服务器，并指定配置文件名称
				D:\JavaWeb2018\day23_redis\资料\redis\windows-64\redis-2.8.9>redis-server.exe redis.windows.conf	
			
		2. AOF：日志记录的方式，可以记录每一条命令的操作。可以每一次命令操作后，持久化数据
			1. 编辑redis.windwos.conf文件
				appendonly no（关闭aof） --> appendonly yes （开启aof）
				
				# appendfsync always ： 每一次操作都进行持久化
				appendfsync everysec ： 每隔一秒进行一次持久化
				# appendfsync no	 ： 不进行持久化
```

# Jedis

是java操作redis数据库的工具

## Jedis操作redis

