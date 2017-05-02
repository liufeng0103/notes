## DB2
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