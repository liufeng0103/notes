# Redis

后台运行，修改配置文件设置daemonize为yes

## Java使用Redis
使用Jedis操作Redis

JedisPool
JedisConfig

为什么需要NoSQL
- High performance
- Huge Storage
- High Scalability && High Availability 高可扩展性和高可用性

NoSQL数据库的4大分类
- key-value 如Redis 优势快速查询，缺点存储的数据缺少结构化
- 列存储 如HBase 优势查询快易扩展，缺点功能局限
- 文档数据库 如MongoDB 优势保存格式随意 缺点查询速度不是特别快 缺少统一的语法
- 图形数据库 infogrid

NoSQL特点
- 易扩展
- 灵活的数据模型
- 大数据量 高性能
- 高可用

Redis应用场景
- 缓存
- 任务队列
- 网站访问统计
- 数据过期处理
- 应用排行榜
- 分布式集群架构中的session分离

make
make prefix=/usr/local/redis install 指定安装目录

flushall 清空redis数据库
del key 删除一个key  
keys * 查看所有key  
incr key 指定key的value+1
decr key value-1
incrby key 5 指定key的value+5

hash类型
hset key name jack
hset key age 18
hmset key2 name rose age 21
hget key name
hmget key name age
hgetall key
hdel key name age
hincrby key age 5
hexists key name 存在返回1
hlen key
hkeys key
hvals key

list类型
ArrayList数组
LinkedList双向链表
lpush key a b c
rpush key 1 2 3
lrange key 0 5 查看元素从0到5个元素， -1是最后的意思
lpop key 弹出并返回元素
llen key
lpushx key x 仅key存在才插入x
lrem key 2 3 删除2个值为3元素
lset key 3 mm 在位置3的地方添加mm
linsert key before b 11

set
set不允许出现重复元素
sadd key a b c
srem key a b
smembers key
sismember key a
sdiff key key2
sinter key key2
sunion key key3
scard key
srandmember key
sdiffstore key1 key2 key3
sinterstore key1 key2 key3

有序集合sorted-set
zadd key 70 zs 90 ww
zadd key 100 zs
zscore key zs
zcard key 获取有序集合的成员数
zrem key zs
zrange key 0 -1
zrange key 0 -1 withscores
zrevrange key 0 -1 withscores
zremrangebyrank key 0 4
zremrangebyscore key 80 100
zincrby key 3 ls
zsore key ls

试用场景
玩家实时排行
构建索引数据

keys通用操作
keys *
keys my？
del my1 my2 my3
exists my1
get compamy
rename key newkey
expire key 1000
ttl key 查看剩余生存时间
type key

Redis特性
- 多数据库 一个最多16个数据库
select 1
- 事务
multi 开启事务
exec 提交
discard 回滚

Redis持久化
- RDB
在指定间隔把内存数据保存到硬盘
- AOF
记录日志，来恢复操作，打开redis.conf
appendonly yes
appendfsync always/everysec/no 策略
- 无持久化
- RDH AOF一起使用

Redis数据结构
- String
- list
- sorted set
- hash
- set
