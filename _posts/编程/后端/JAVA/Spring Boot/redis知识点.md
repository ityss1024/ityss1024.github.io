### boot整合redis

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
    <version>2.6.7</version>
</dependency>
```

#### redis为什么高性能?

```
基于内存,单线程,使用多路I/O服用模型 非阻塞IO
```

### redis应用场景

```js
1.缓存
将热点数据放到内存中，实现高性能
2.分布式锁的实现
redis自带的setnx命令实现分布式锁
3.会话缓存
使用redis来统一存储多台应用服务器的会话信息。从而更容易实现高可用。
```

### 过期键删除策略

```js
1.定期过期:每个设置过期时间的key都需要创建一个定时器，到时立即清除
2.惰性过期:当某个key被访问到时，才会判断该key是否已过期，过期则清除。
```

#### 过期时间和永久设置分别怎么设置?

```
expire:设置过期时间
persist:永久有效
```

### 集群方案

参考 https://www.cnblogs.com/spec-dog/p/12501895.html

```
Redis支持三种集群方案

主从复制模式  
Sentinel（哨兵）模式
Cluster模式
```

#### 1.主从复制

```js
一个主数据库实例（master）与一个或多个从数据库实例（slave）,客户端可对主数据库进行读写操作，对从数据库进行读操作，主数据库写入的数据会实时自动同步给从数据库。

优点：
master能自动将数据同步到slave，可以进行读写分离，分担master的读压力
master、slave之间的同步是以非阻塞的方式进行的，同步期间，客户端仍然可以提交查询或更新请求

缺点：
不具备自动容错与恢复功能，master或slave的宕机都可能导致客户端请求失败，需要等待机器重启或手动切换客户端IP才能恢复
master宕机，如果宕机前数据没有同步完，则切换IP后会存在数据不一致的问题
难以支持在线扩容，Redis的容量受限于单机配置
```

#### 2.哨兵模式

```js
哨兵模式基于主从复制模式，只是引入了哨兵来监控与自动处理故障
哨兵顾名思义，就是来为Redis集群站哨的，一旦发现问题能做出相应的应对处理。其功能包括
监控master、slave是否正常运行
当master出现故障时，能自动将一个slave转换为master（大哥挂了，选一个小弟上位）
多个哨兵可以监控同一个Redis，哨兵之间也会自动监控

优点:
哨兵模式基于主从复制模式，所以主从复制模式有的优点，哨兵模式也有
哨兵模式下，master挂掉可以自动进行切换，系统可用性更高

缺点:
同样也继承了主从模式难以在线扩容的缺点，Redis的容量受限于单机配置
需要额外的资源来启动sentinel进程，实现相对复杂一点，同时slave节点作为备份节点不提供服务
```

#### Cluster模式

```js
哨兵模式解决了主从复制不能自动故障转移，达不到高可用的问题，但还是存在难以在线扩容，Redis容量受限于单机配置的问题。Cluster模式实现了Redis的分布式存储，即每台节点存储不同的内容，来解决在线扩容的问题。
```

#### 总结

```js
本文介绍了Redis集群方案的三种模式，其中主从复制模式能实现读写分离，但是不能自动故障转移；哨兵模式基于主从复制模式，能实现自动故障转移，达到高可用，但与主从复制模式一样，不能在线扩容，容量受限于单机的配置；Cluster模式通过无中心化架构，实现分布式存储，可进行线性扩展，也能高可用，但对于像批量操作、事务操作等的支持性不够好。三种模式各有优缺点，可根据实际场景进行选择。
```

### redis数据类型

#### 1.String(字符串)

```js
string类型的key/value最大能存储 512MB

添加新的String键值对
set key value
根据相应的key获取到value
get key
```

#### 2.Hash (哈希)

```js
string 类型的 field 和 value 的映射表，hash 特别适合用于存储对象

添加新的Hash键值对
HMSET runoob field1 "Hello" field2 "World"
获取到相应的key中的属性值
HGET runoob field1   \\ "Hello"

HMSET 设置了两个 field=>value 对, HGET 获取对应 field 对应的 value。
每个 hash 可以存储 2^32 -1 键值对（40多亿）
```

#### 3.List(列表)

```js
列表是简单的字符串列表，按照插入顺序排序.

// 向runoob列表  加入redis
lpush runoob redis
// 向runoob列表  加入mongodb
lpush runoob mongodb

//获取列表的值
lrange runoob 0 10
"mongodb"
"redis"

列表可以存储 2^32 -1 键值对（40多亿）
```

#### 4.Set(集合)

```js
Set 是 string 类型的无序集合。集合是通过哈希表实现的，所以添加，删除，查找的复杂度都是 O(1)

// 向集合中添加redis
sadd runoob redis
// 向集合中添加mongodb
sadd runoob mongodb

// 显示runoob 集合
smembers runoob

"redis"
"rabbitmq"

集合中元素不重复。集合中最大的成员数为 2^32 - 1
```

#### 5.zset(有序集合)

```js
zset 和 set 一样也是string类型元素的集合,且不允许重复的成员。
不同的是每个元素都会关联一个double类型的分数。redis正是通过分数来为集合中的成员进行从小到大的排序。
zset的成员是唯一的,但分数(score)却可以重复。

zadd 命令
添加元素到集合，元素在集合中存在则更新对应score
zadd key score member 

// 向有序集合中添加新的元素
zadd testzset 0 redis
zadd testzset 2 rabbitmq
// 显示集合中元素
zrangebyscor testzset 0 1000

输出
redis
rabbitmq
```

各个数据类型应用场景：

| 类型                 | 简介                                                   | 特性                                                         | 场景                                                         |
| :------------------- | :----------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| String(字符串)       | 二进制安全                                             | 可以包含任何数据,比如jpg图片或者序列化的对象,一个键最大能存储512M | ---                                                          |
| Hash(字典)           | 键值对集合,即编程语言中的Map类型                       | 适合存储对象,并且可以像数据库中update一个属性一样只修改某一项属性值(Memcached中需要取出整个字符串反序列化成对象修改完再序列化存回去) | 存储、读取、修改用户属性                                     |
| List(列表)           | 链表(双向链表)                                         | 增删快,提供了操作某一段元素的API                             | 1,最新消息排行等功能(比如朋友圈的时间线) 2,消息队列          |
| Set(集合)            | 哈希表实现,元素不重复                                  | 1、添加、删除,查找的复杂度都是O(1) 2、为集合提供了求交集、并集、差集等操作 | 1、共同好友 2、利用唯一性,统计访问网站的所有独立ip 3、好友推荐时,根据tag求交集,大于某个阈值就可以推荐 |
| Sorted Set(有序集合) | 将Set中的元素增加一个权重参数score,元素按score有序排列 | 数据插入集合时,已经进行天然排序                              | 1、排行榜 2、带权重的消息队列                                |



### redis常用命令

参考 https://blog.csdn.net/qq_38174263/article/details/80009943

#### key 相关命令

```js
key pattern 查询相应的key
redis允许模糊查询key　　有3个通配符  *、?、[]　　
type key：返回key存储的类型
exists key：判断某个key是否存在
del key：删除key
rename key newkey：改名
renamenx key newkey：如果newkey不存在则修改成功
move key 1：将key移动到1数据库
ttl key：查询key的生命周期（秒）
expire key 整数值：设置key的生命周期以秒为单位
pexpire key 整数值：设置key的生命周期以毫秒为单位
pttl key：查询key 的生命周期（毫秒）
perisist key：把指定key设置为永久有效
```

#### 字符串类型的操作

```
（1）set key value [ex 秒数] [px 毫秒数] [nx/xx]　　
如果ex和px同时写，则以后面的有效期为准
nx：如果key不存在则建立
xx：如果key存在则修改其值

（2）get key：取值

（3）mset key1 value1 key2 value2 一次设置多个值

（4）mget key1 key2 ：一次获取多个值

（5）setrange key offset value：把字符串的offset偏移字节改成value，如果偏移量 > 字符串长度，该字符自动补0x00

（6）append key value ：把value追加到key 的原值上

（7）setex key time value：设置key对应的值value，并设置有效期为time秒
```

#### 链表操作

```
Redis的list类型其实就是一个每个子元素都是string类型的双向链表，链表的最大长度是2^32。list既可以用做栈，也可以用做队列。

　　list的pop操作还有阻塞版本，主要是为了避免轮询

　　（1）lpush key value：把值插入到链表头部

　　（2）rpush key value：把值插入到链表尾部

　　（3）lpop key ：返回并删除链表头部元素

　　（4）rpop key： 返回并删除链表尾部元素

　　（5）lrange key start stop：返回链表中[start, stop]中的元素

　　（6）lrem key count value：从链表中删除value值，删除count的绝对值个value后结束

　　　　count > 0 从表头删除　　count < 0 从表尾删除　　count=0 全部删除

　　（7）ltrim key start stop：剪切key对应的链接，切[start, stop]一段并把改制重新赋给key

　　（8）lindex key index：返回index索引上的值

　　（9）llen key：计算链表的元素个数

　　（10）linsert key after|before search value：在key 链表中寻找search，并在search值之前|之后插入value

　　（11）rpoplpush source dest：把source 的末尾拿出，放到dest头部，并返回单元值

　业务逻辑： rpoplpush task bak
  接收返回值并做业务处理。如果成功则rpop bak清除任务，如果不成功，下次从bak表取任务

　　（12）brpop，blpop key timeout：等待弹出key的尾/头元素，timeout为等待超时时间，如果timeout为0则一直等待下去
应用场景：长轮询ajax，在线聊天时能用到
```

#### hashes类型及操作

```
Redis hash 是一个string类型的field和value的映射表，它的添加、删除操作都是O(1)（平均）。hash特别适用于存储对象，将一个对象存储在hash类型中会占用更少的内存，并且可以方便的存取整个对象。

　　配置： hash_max_zipmap_entries 64 #配置字段最多64个

　　　　　 hash_max_zipmap_value 512 #配置value最大为512字节

　　（1）hset myhash field value：设置myhash的field为value

　　（2）hsetnx myhash field value：不存在的情况下设置myhash的field为value

　　（3）hmset myhash field1 value1 field2 value2：同时设置多个field

　　（4）hget myhash field：获取指定的hash field

　　（5）hmget myhash field1 field2：一次获取多个field

　　（6）hincrby myhash field 5：指定的hash field加上给定的值

　　（7）hexists myhash field：测试指定的field是否存在

　　（8）hlen myhash：返回hash的field数量

　　（9）hdel myhash field：删除指定的field

　　（10）hkeys myhash：返回hash所有的field

　　（11）hvals myhash：返回hash所有的value

　　（12）hgetall myhash：获取某个hash中全部的field及value　
```

#### 集合结构操作

```
特点：无序性、确定性、唯一性

　　（1）sadd key value1 value2：往集合里面添加元素

　　（2）smembers key：获取集合所有的元素

　　（3）srem key value：删除集合某个元素

　　（4）spop key：返回并删除集合中1个随机元素（可以坐抽奖，不会重复抽到某人）　　　

　　（5）srandmember key：随机取一个元素

　　（6）sismember key value：判断集合是否有某个值

　　（7）scard key：返回集合元素的个数

　　（8）smove source dest value：把source的value移动到dest集合中

　　（9）sinter key1 key2 key3：求key1 key2 key3的交集

　　（10）sunion key1 key2：求key1 key2 的并集

　　（11）sdiff key1 key2：求key1 key2的差集

　　（12）sinterstore res key1 key2：求key1 key2的交集并存在res里　
```

#### 有序集合

```
概念：它是在set的基础上增加了一个顺序属性，这一属性在添加修改元素的时候可以指定，每次指定后，zset会自动按新的值调整顺序。可以理解为有两列的mysql表，一列存储value，一列存储顺序，操作中key理解为zset的名字。

　　和set一样sorted，sets也是string类型元素的集合，不同的是每个元素都会关联一个double型的score。sorted set的实现是skip list和hash table的混合体。

　　当元素被添加到集合中时，一个元素到score的映射被添加到hash table中，所以给定一个元素获取score的开销是O(1)。另一个score到元素的映射被添加的skip list，并按照score排序，所以就可以有序地获取集合中的元素。添加、删除操作开销都是O(logN)和skip list的开销一致，redis的skip list 实现是双向链表，这样就可以逆序从尾部去元素。sorted set最经常使用方式应该就是作为索引来使用，我们可以把要排序的字段作为score存储，对象的ID当元素存储。

　　（1）zadd key score1 value1：添加元素

　　（2）zrange key start stop [withscore]：把集合排序后,返回名次[start,stop]的元素  默认是升续排列  withscores 是把score也打印出来

　　（3）zrank key member：查询member的排名（升序0名开始）

　　（4）zrangebyscore key min max [withscores] limit offset N：集合（升序）排序后取score在[min, max]内的元素，并跳过offset个，取出N个

　　（5）zrevrank key member：查询member排名（降序 0名开始）

　　（6）zremrangebyscore key min max：按照score来删除元素，删除score在[min, max]之间

　　（7）zrem key value1 value2：删除集合中的元素

　　（8）zremrangebyrank key start end：按排名删除元素，删除名次在[start, end]之间的

　　（9）zcard key：返回集合元素的个数

　　（10）zcount key min max：返回[min, max]区间内元素数量

　　（11）zinterstore dest numkeys key1[key2..] [WEIGHTS weight1 [weight2...]] [AGGREGATE SUM|MIN|MAX]

　　　　　　求key1，key2的交集，key1，key2的权值分别是weight1，weight2

　　　　　　聚合方法用 sum|min|max

　　　　　　聚合结果 保存子dest集合内

　　　　　　注意：weights,aggregate如何理解？

　　　　　　答：如果有交集，交集元素又有score，score怎么处理？aggregate num->score相加，min最小score，max最大score，另外可以通过weights设置不同的key的权重，交集时  score*weight
```

#### 服务器相关命令

```js
ping：测定连接是否存活
echo：在命令行打印一些内容
select：选择数据库
quit：退出连接
dbsize：返回当前数据库中key的数目
info：获取服务器的信息和统计
monitor：实时转储收到的请求
config get 配置项：获取服务器配置的信息
config set 配置项  值：设置配置项信息
flushdb：删除当前选择数据库中所有的key
flushall：删除所有数据库中的所有的key
time：显示服务器时间，时间戳（秒），微秒数
bgrewriteaof：后台保存rdb快照
bgsave：后台保存rdb快照
save：保存rdb快照
lastsave：上次保存时间
shutdown [save/nosave]

	注意：如果不小心运行了flushall，立即shutdown nosave，关闭服务器，然后手工编辑aof文件，去掉文件中的flushall相关行，然后开启服务器，就可以倒回原来是数据。如果flushall之后，系统恰好bgwriteaof了，那么aof就清空了，数据丢失。

（17）showlog：显示慢查询
  问：多慢才叫慢？
  答：由slowlog-log-slower-than 10000，来指定（单位为微秒）
  问：服务器存储多少条慢查询记录
  答：由slowlog-max-len 128，来做限制　
```

### Stream类型  

参考 https://www.runoob.com/redis/redis-stream.html

```
Redis Stream 提供了消息的持久化和主备复制功能，可以让任何客户端访问任何时刻的数据，并且能记住每一个客户端的访问位置，还能保证消息不丢失。
```

**消息队列相关命令：**

```js
- XADD - 添加消息到末尾
- XTRIM - 对流进行修剪，限制长度
- XDEL - 删除消息
- XLEN - 获取流包含的元素数量，即消息长度
- XRANGE - 获取消息列表，会自动过滤已经删除的消息
- XREVRANGE - 反向获取消息列表，ID 从大到小
- XREAD - 以阻塞或非阻塞方式获取消息列表
```

**消费者组相关命令：**

```js
- XGROUP CREATE - 创建消费者组
- XREADGROUP GROUP - 读取消费者组中的消息
- XACK - 将消息标记为"已处理"
- XGROUP SETID - 为消费者组设置新的最后递送消息ID
- XGROUP DELCONSUMER - 删除消费者
- XGROUP DESTROY - 删除消费者组
- XPENDING - 显示待处理消息的相关信息
- XCLAIM - 转移消息的归属权
- XINFO - 查看流和消费者组的相关信息；
- XINFO GROUPS - 打印消费者组的信息；
- XINFO STREAM - 打印流信息
```

#### xadd命令

```
使用 XADD 向队列添加消息，如果指定的队列不存在，则创建一个队列，XADD 语法格式：
XADD key ID field value [field value ...]

key ：队列名称，如果不存在就创建
ID ：消息 id，我们使用 * 表示由 redis 生成，可以自定义，但是要自己保证递增性。
field value ： 记录。
```

### 持久化机制

https://blog.csdn.net/chen772209/article/details/106861618/

#### 为什么要数据持久化?

```js
宕机后数据恢复
```

#### 持久化的实现方式

```js
1.快照持久化(RDB 默认)：将Redis某一时刻存在的所有数据都写入硬盘。

2.AOF持久化：每次处理完请求命令后都会将此命令追加到aof日志文件的末尾
```

##### 快照持久化(RDB)

```js
创建快照 来存储内存里面的数据 在某个时间点的副本 存的的RDB二进制文件

触发机制:
1.save（同步）
2.bgsave（异步）
3.自动

    1.save
    在数据量很大的时候，会存在阻塞，因为redis是单线程的。
    复杂度：O(N)，因为需要将redis中的所有数据都写在RDB文件中
    新RDB文件会替换老RDB文件

    致命的问题:持久化的时候redis服务阻塞（准确的说会阻塞当前执行save命令的线程，但是redis是单线程的，所以整个服务会阻塞），不能继对外提供请求，GG！数据量小的话肯定影响不大，数据量大呢？每次复制需要1小时，那就相当于停机一小时

    2.bgsave
    客户端向Redis发送bgsave命令，Redis调用fork创建一个子进程，然后子进程负责将快照写入硬盘，而父进程则继续处理命令请求。
    这个createRDB是由子进程来完成的。
    好处:
    一边进行持久化，一边对外提供读写服务，互不影响，新写的数据对我持久化不会造成数据影响，你持久化的过程中报错或者耗时太久都对我当前对外提供请求的服务不会产生任何影响。持久化完会将新的rdb文件覆盖之前的。

    3.自动
    通过配置，满足任何一个条件就会创建快照文件。

RDB存在的问题
耗时、耗性能：通过bgsave命令进行持久化的的时候，需要fork一个子进程，如果数据量很大的话，需要的内存也会相应的变大，内存的占用会导致Redis性能降低。
不可控、丢失数据：举个例子，上一次创建快照是11:00开始创建并创建成功。如果Redis在12:00开始创建新的快照，如果系统在未完成创建快照之前崩溃，11:00-12:00写入的数据将会丢失；如果系统在快照创建完成之后崩溃，那么12:00之后，创建快照的过程中的数据将会丢失。


```

##### AOF持久化

```js
每次处理完请求命令后都会将此命令追加到aof文件的末尾。

策略:
always：每条Redis写命令都同步写入硬盘。
everysec：每秒执行一次同步，将多个命令写入硬盘。
no：由操作系统决定何时同步。
比较:
always：同步持久化，每次发生数据变更会被立即记录到磁盘（性能较差，数据完整性较好）（效率最慢，但也是安全性最高的）
everysec：效率挺快的，就算出现故障，数据库也只是丢失一秒钟的命令数据。（默认推荐，，异步操作，每秒记录，若一秒钟内宕机，又数据丢失）
no：与 everysec效率相当，但是出现故障时，将丢失上次同步AOF文件之后的所有写命令数据


为了解决AOF文件不断膨胀的问题，需要移除AOF文件中的冗余命令来重写AOF。
实现方式:
bgrewriteaof命令
触发机制：
reids会记录上次重写时的AOF大小，默认配置是当AOF文件大小是上次rewrite后大小的一倍且文件>64M时触发。
AOF重写配置
```

#### 小总结

```
RDB：
RDB是一个非常紧凑的文件
RDB在保存RDB文件时，主进程唯一要做的是：fork出一个子进程，接下来的工作全部交由子进程来做，父进程不需要在做其他IO操作，所以，RDB持久化方式是可以最大化redis的性能。
与AOF相比，在恢复大数据集的时候，RDB文件会更快一些
数据丢失风险大
RDB需要经常fork子进程来保存数据集到硬盘上，当数据集比较大时，fork的进程是非常耗时的，可能会导致redis在一些毫秒级不能响应客户端的请求

AOF：
AOF文件是一个只进行追加的日志文件
redis可以在AOF文件体积变得过大时，自动地后台对AOF进行重写
AOF文件有序地保存了对数据执行的所有写入操作，这些写入操作以redis协议的格式保存，因此AOF文件的内容非常容易被人读懂，对文件进行分析是很轻松的
对于相同的数据集来说，AOF文件的体积通常>RDB文件的体积
根据所使用的fsync策略，AOF的速度可能会慢于RDB

RDB持久化是通过保存数据库中的键值对来记录数据库状态不同。而AOF持久化是通过保存redis服务器所执行的命令来记录数据库状态的。
```

### 缓存异常及预防方式

#### 缓存雪崩

```
缓存大面积失效 导致所有请求都要查询数据库 甚至宕机
预防:
1.设置缓存过期时间是随机的
2.给缓存数据加上缓存标记，记录缓存是否失效，如果失效则更新缓存数据。
```

#### 缓存穿透

```js
查询不存在的数据  所有请求都要查数据库 数据库可能会承受不了大量请求二奔溃
预防:
设置key规则  过滤不符合规则的key
```