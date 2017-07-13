// AtomicLong原子量,java6中的新东西。有兴趣研究线程的时候在学。这里用它了自增一个id
private final AtomicLong counter = new AtomicLong();
counter.incrementAndGet()


## Quartz
Java定时任务调度工具

- [Java使用quartz实现作业调度](http://qiaowei.xyz/2016/05/11/Java%E4%BD%BF%E7%94%A8quartz%E5%AE%9E%E7%8E%B0%E4%BD%9C%E4%B8%9A%E8%B0%83%E5%BA%A6/)
- [Quartz-Cron Expression 使用介绍](https://my.oschina.net/u/1042053/blog/136090)

组成
- Job 实现业务逻辑的任务，参数JobExecutionContext，可以用来获取Quartz运行Job的环境信息， JobDataMap可以传入参数到Job

- JobDetail 存储job的相关ß属性，如name group jobClass jobDataMap
- JobBuilder 创建JobDetail
- JobStore
- Trigger
- TriggerBuilder
- ThreadPool
- Scheduler
- 监听器

核心
- Job
- Trigger
- Scheduler

1. 实现Job接口
2. 创建JobDetail
3. 创建Trigger
4. 创建Scheduler
