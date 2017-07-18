# MySQL使用

MySQL中数据文件本身是一棵B+Tree，特别是对于InnoDB的数据文件本身就是索引文件，在物理上按照主键大小顺序存储

- [MySql5.7 InnoDB全文索引（针对中文搜索）](http://blog.csdn.net/qq_33663251/article/details/69612619?utm_source=itdadao&utm_medium=referral)
- [Windows下Mysql数据库服务的关闭和重启](http://blog.csdn.net/rickypc/article/details/4963025)

windows解压后复制my-default.ini为my.ini,配置basedir和datadir，my.ini为英文编码 重启后将使用my.ini配置

## 安装
### CentOS7 yum安装MySQL
参考[官网教程](https://dev.mysql.com/doc/mysql-yum-repo-quick-guide/en/)
1. 下载MySQL yum repository包  
`wget https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm`
2. 安装下载的包，把MySQL yum repository添加到系统repository列表  
`sudo rpm -Uvh mysql57-community-release-el7-11.noarch.rpm`
3. 安装MySQL,默认安装最新的，如果想选择版本安装，参考官网教程  
`sudo yum install mysql-community-server`
4. 开始MySQL  
启动MySQL  
`sudo service mysqld start`  
`sudo systemctl start mysqld.service`  
`sudo systemctl restart mysqld.service`  
查看MySQL server状态  
`sudo service mysqld status`  
`sudo systemctl status mysqld.service`  
MySQL服务器初始化（仅适用于MySQL 5.7）：在服务器初始启动时，如果服务器的数据目录为空，则会发生以下情况:  
server被初始化  
在data目录产生SSL证书和key文件  
validate_password插件被安装并启用  
超级用户'root'@'localhost'被创建。通过以下命令获取生成root的临时密码:  
`sudo grep 'temporary password' /var/log/mysqld.log`  
尽快修改这个临时的root账号密码  
`mysql -uroot -p`  
`ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass4!';`  
说明:  
MySQL的validate_password插件被默认安装，它将验证新密码需要至少一个大写，一个小写，一个数字，一个特殊字符，密码长度不低于8位的密码
5. 更新MySQL  
对于没有启用dnf-enabled的server，使用以下命令更新所有组件:    
`sudo yum update mysql-server`  
对于启用dnf-enabled的系统:  
`sudo dnf --refresh upgrade mysql-server`

### windows安装
1. 将下载下来的mysql解压到指定目录下(如:d:\mysql)
2. 安装服务，在命令行输入：
```
d:\mysql\bin\mysqld -install
启动服务
net start mysql
```
3. 卸载服务，在命令行输入：
```
net stop mysql
d:\mysql\bin\mysqld -remove
# 删除服务
sc delete MySQL
```

## MariaDB
MariaDB是MySQL的一个分支，CentOS7开始用MariaDB代替了MySQL数据库。

### 安装MariaDB
1. 安装MariaDB  
`yum -y install mariadb mariadb-server`
2. 启动MariaDB  
`systemctl start mariadb`
3. 停止MariaDB  
`systemctl stop mariadb`
4. 重启MariaDB  
`systemctl restart mariadb`
5. 设置开机启动  
`systemctl enable mariadb`
6. 安装启动后输入以下命令将引导设置root密码  
`mysql_secure_installation`

## 创建DB用户
1. 创建用户bnade,密码xxxx,%表示在任何情况下可以连接  
`CREATE USER 'bnade'@'%' IDENTIFIED BY 'xxxx';`
2. 查看用户权限  
`show grants for bnade;`
3. 给用户授权wow数据库下的表的权限  
`GRANT all ON wow.* TO 'bnade'@'%';`  
`GRANT select ON wow.* TO 'tomcat'@'%';`  
`GRANT insert ON wow.mt_item TO 'tomcat'@'%';`
4. 回收权限,如果权限不存在会报错  
`revoke  select on wow.*  from  bnade;`

### MariaDB目录
* usr/bin/mysql：mysql的运行路径
* var/lib/mysql：mysql数据库文件的存放路径
* usr/lib/mysql：mysql的安装路径
配置文件路径 /etc/my.cnf

### 共享表空间和独立表空间之间的转换
1. 查看当前数据库的表空间管理类型，ON代表独立表空间管理，OFF代表共享表空间管理  
`show variables like "innodb_file_per_table";`
2. 修改数据库的表空间管理方式，修改innodb_file_per_table的参数值即可，但是修改不能影响之前已经使用过的共享表空间和独立表空间  
innodb_file_per_table=1 为使用独占表空间  
innodb_file_per_table=0 为使用共享表空间
3. 共享表空间转化为独立表空间的方法（参数innodb_file_per_table=1需要设置）单个表的转换操作  
`alter table table_name engine=innodb;`

### 修改内存表的最大内存大小
MEMORY表最大值受系统变量 max_heap_table_size 限制，默认为16MB，要改变MEMORY表大小限制，需要改变max_heap_table_size 的值。该值在 CREATE TABLE 时生效并伴随表的生命周期，(当你使用 ALTER TABLE 或 TRUNCATE TABLE命令时，表的最大限制将改变，或重启MYSQL服务时, 所有已存在的MEMORY表的最大限制将使用max_heap_table_size 的值重置

系统变量 max_heap_table_size 用于设置内存表的大小上限。要控制单个表的最大值，需要在创建表之前设置会话变量。(不要设置全局max_heap_table_size 的值，除非你打算所有客户端创建的内存表都使用这个值)

下面的例子创建了两张内存表，它们的大小限制分别为 1MB 和 2MB  
`SET max_heap_table_size = 1024*1024;`
`CREATE TABLE t1 (id INT, UNIQUE(id)) ENGINE = MEMORY;`
`SET max_heap_table_size = 1024*1024*2;`
`CREATE TABLE t2 (id INT, UNIQUE(id)) ENGINE = MEMORY;`
查看max_heap_table_size  
```SELECT @@max_heap_table_size```

### 最大连接数
MySQL服务器最大连接数  
```show variables like 'max_connections';```  
服务器响应的最大连接数  
```show global status like 'Max_used_connections';```

### explain使用
各个属性的含义

* id  
select查询的序列号
* select_type  
select查询的类型，主要是区别普通查询和联合查询、子查询之类的复杂查询。
* table  
输出的行所引用的表。
* type  
联合查询所使用的类型。
type显示的是访问类型，是较为重要的一个指标，结果值从好到坏依次是：
system > const > eq_ref > ref > fulltext > ref_or_null > index_merge > unique_subquery > index_subquery > range > index > ALL
一般来说，得保证查询至少达到range级别，最好能达到ref。
* possible_keys  
指出MySQL能使用哪个索引在该表中找到行。如果是空的，没有相关的索引。这时要提高性能，可通过检验WHERE子句，看是否引用某些字段，或者检查字段不是适合索引。
* key  
显示MySQL实际决定使用的键。如果没有索引被选择，键是NULL。
* key_len  
显示MySQL决定使用的键长度。如果键是NULL，长度就是NULL。文档提示特别注意这个值可以得出一个多重主键里mysql实际使用了哪一部分。
* ref  
显示哪个字段或常数与key一起被使用。
* rows  
这个数表示mysql要遍历多少数据才能找到，在innodb上是不准确的。
* Extra  
如果是Only index，这意味着信息只用索引树中的信息检索出的，这比扫描整个表要快。
如果是where used，就是使用上了where限制。
如果是impossible where 表示用不着where，一般就是没查出来啥。
如果此信息显示Using filesort或者Using temporary的话会很吃力，WHERE和ORDER BY的索引经常无法兼顾，如果按照WHERE来确定索引，那么在ORDER BY时，就必然会引起Using filesort，这就要看是先过滤再排序划算，还是先排序再过滤划算。

### 优化表格
```optimize table xxx```

* MySQL官方建议不要经常(每小时或每天)进行碎片整理，一般根据实际情况，只需要每周或者每月整理一次即可。
* 在OPTIMIZE TABLE运行过程中，MySQL会锁定表。
* 当INNODB时，MYSQL会以ALTER TABLE去执行这个命令。 所以最终还是会看到 OK 的状态。
ALTER TABLE table.name ENGINE='InnoDB';

## 分区表
分区表需要在建表的时候创建，且分区列必须在主键中

```sql
-- 新增分区
ALTER TABLE auction ADD PARTITION (PARTITION p1 VALUES IN (1));
-- 删除分区
ALTER TABLE auction DROP PARTITION p1;
-- 查看分区
SELECT * FROM INFORMATION_SCHEMA.partitions WHERE TABLE_SCHEMA = SCHEMA() AND TABLE_NAME='auction';
```

数据库表和字段使用下划线分隔

## mysql常用命令

增加了密码后的登录格式如下：
　　mysql -u root -p
　　Enter password: (输入密码)

启动mysql 通过输入命令  mysqld --skip-grant-tables  回车，此时就跳过了mysql的用户验证

show databases;
create database SAMPLE;
use SAMPLE;
show tables;

mysql命令行执行sql文件
1. 登录mysql命令行 mysql -u xxx -p
2. 切换数据库 use xxx
3. 运行脚本 source /home/xxx/xx.sql

## 函数
- 时间戳转日期字符串 select FROM_UNIXTIME(`dateTime`/1000,'%Y-%m-%d')
