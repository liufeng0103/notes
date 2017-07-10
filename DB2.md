# DB2

[SQL 数据复制过程中控制表运行状况分析](http://tech.cncms.com/shujuku/db2/14003.html)

### 常用
- 查看实例 db2ilist
- 查看当前实例 db2 get instance
- 启动关闭 db2 db2start db2stop
- 强制关闭  
方式1： 1. db2 force application all 2. db2stop  
方式2： db2stop force  
- DB2 中的LONG VARCHAR类型 http://blog.csdn.net/yukiooy/article/details/4742904
- 确定DB2发行版和版本 db2level
- 查找DB2消息代码 db2=> ? sql0289
- 连接到数据库 connect to database user user ID using password
- 查看所有数据库 list db directory 或 list db directory show details
- 查看数据库管理器配置文件 db2=> get db cfg
- 查看数据库配置文件 db2=> get db cfg for <database>
- 查看DB2注册表 db2set -all

### DPROP(IBM InfoSphere Data Replication Center)
- 启动 db2rc

### catalog db
db2 uncatalog node <node name>
db2 uncatalog database <db alise name>
db2 catalog tcpip node <node name> remote <ip> server <port>
db2 catalog db <db name> as <db alise name> at node <node name>
db2 terminate
db2 connect to <db alise name> user <user> using <password>

## DB2相关文章
* [用db2_install命令行安装DB2数据库 ](http://blog.csdn.net/flcandclf/article/details/7634754) - 安装DB2数据库，以及实例和DB2管理服务器的创建

## DB2管理服务器(DB2 Administration Server - DAS)
- 创建DB2管理服务器  
```
cd /opt/ibm/db2/V10.5/instance  
./dascrt -u dasusr1
DBI1070I  Program dascrt completed successfully.
```
- 启动DB2管理服务器  
```
su dasusr1  
db2admin start
SQL4409W The DB2 Administration Server is already active.
```

### 下面列举了一些用于管理DAS服务的命令：
- DB2ADMIN START：用于启动DAS
- DB2ADMIN STOP：用于终止DAS
- DASICRT：在UNIX环境下创建DAS
- DASIDROP：在UNIX环境下删除DAS
- DB2ADMIN：CREATE 在Windows环境下创建DAS
- DB2ADMIN：DROP在Windows环境下删除DAS
- DB2 GET ADMIN CFG：用于显示DAS的数据库管理器配置
- DB2 UPDATE ADMINCFG：用于更改DAS的数据库管理器配置文件的参数（需要执行DB2ADMINSTOP和DB2ADMINSTART命令之后才能生效）
- DB2 RESET ADMIN CFG：用于将DAS的配置参数设置为默认值（需要执行DB2ADMINSTOP和DB2ADMINSTART命令之后才能生效）

## 函数
```sql
-- 获取月初日期
CONCAT(LEFT(VARCHAR_FORMAT(CURRENT DATE,'yyyy-mm-dd'),8),'01')
-- 获取下个月月初日期
CONCAT(LEFT(VARCHAR_FORMAT(CURRENT DATE+ 1 MONTHS,'yyyy-mm-dd'),8),'01')
-- CURRENT DATE获取的日期在不同的db2里格式可能不一致，需要格式化一下统一格式
```
