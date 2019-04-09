# Linux
## 常用
- 仓库配置目录 /etc/yum.repos.d
- 修改目录的用户和用户组 sudo chown user:group -R directory
- 启动栏app /usr/share/applications

## 软件安装
- 查看rpm包安装路径 rpm -qpl xxx.rpm
- 查看yum安装的软件路径 1. 查看软件完整的名称 rpm -qa|grep tomcat 2. 查看路径 rpm -ql xxx

### rpm
rpm -i 需要安装的包文件名

## iptables
- 查看定义规则的详细信息  
iptables -L -n -v
- 开发3306端口  
iptables -I INPUT -p tcp --dport 3306 -j ACCEPT
- 只允许指定ip连接指定端口
iptables -I INPUT -p tcp --dport 8080 -j DROP
iptables -I INPUT -s 127.0.0.1 -p tcp --dport 8080 -j ACCEPT

## 用户管理
创建用户 useradd luis

设置密码 passwd luis

删除用户 userdel luis

切换用户 su luis

## 组
查看组 groups
添加组 groupadd docker
添加用户到组 gpasswd -a ${USER} docker

### 用户添加sudo权限
1. 使用root账户使用以下命令为sudoers添加写权限 chmod u+w /etc/sudoers
2. 添加 <user> ALL=(ALL) ALL
3. 去掉文件写权限 chmod u-w /etc/sudoers

sudo service mysqld start
sudo systemctl start mysqld.service

## Linux
* 仓库配置目录 
/etc/yum.repos.d

* 修改目录的用户和用户组
sudo chown Luis:Luis -R /opt/ibm/WebSphere/AppServer

VPN连内外问题解决：
sudo ifconfig vpn0 mtu 1362 up

RSA Exit code=160解决：
export MOZILLA_FIVE_HOME=/usr/lib64/firefox

启动栏app：
cd /usr/share/applications

启动RSA：
sudo /opt/ibm/SDP/eclipse -product com.ibm.rational.rsa4ws.product.v80.ide

启动IBMIM：
sudo /opt/ibm/InstallationManager/eclipse/IBMIM

## WAS相关
* 安装目录：
cd /opt/ibm/WebSphere/AppServer
* 启动was:
`sudo /opt/ibm/WebSphere/AppServer/profiles/AppSrv01/bin/startServer.sh server1 -profileName AppSrv01 -username wasadmin -password wasadmin`
`sudo /opt/ibm/WebSphere/AppServer/profiles/AppSrv01/bin/stopServer.sh server1 -profileName AppSrv01 -username wasadmin -password wasadmin`

`sudo /opt/ibm/WebSphere/AppServer/profiles/AppSrv02/bin/startServer.sh server1 -profileName AppSrv02 -username wasadmin -password wasadmin`
`sudo /opt/ibm/WebSphere/AppServer/profiles/AppSrv02/bin/stopServer.sh server1 -profileName AppSrv02 -username wasadmin -password wasadmin`
-username wasadmin -password wasadmin

tail -2000 /projects/w3alpha/logs/isc/sdpi/SdpiAll_server1.log 
* was控制台：
https://localhost:9044/ibm/console/login.do

* was profile管理工具
sudo /opt/ibm/WebSphere/AppServer/bin/ProfileManagement/pmt.sh

* WAS安装java7：
IBM网站下载以下软件，然后通过im安装
IBM WebSphere SDK Java (TM) Technology Edition V7.0 (1 of 3) (for WebSphere Application Server V8.5) Multiplatform Multilingual 	CI717ML
IBM WebSphere SDK Java (TM) Technology Edition V7.0 (2 of 3) (for WebSphere Application Server V8.5) Multiplatform Multilingual 	CI718ML
IBM WebSphere SDK Java (TM) Technology Edition V7.0 (3 of 3) (for WebSphere Application Server V8.5) Multiplatform Multilingual 	CI719ML

* 切换was到java7：
参考 https://www.ibm.com/support/knowledgecenter/en/SSWLGF_8.5.5/com.ibm.sr.doc/twsr_java17.html
sudo /opt/ibm/WebSphere/AppServer/bin/managesdk.sh -enableProfile -profileName AppSrv01 -sdkname 1.7_64

* 查看所有profiles
sudo /opt/ibm/WebSphere/AppServer/bin/manageprofiles.sh -listProfiles

* 删除profile
sudo /opt/ibm/WebSphere/AppServer/bin/manageprofiles.sh -delete -profileName AppSrv01

### SDPI
* 地址：
http://localhost:9081/isc/sdpi

## DB2相关
* DB2下载：
IBM DB2 Enterprise Server Edition V10.5 Fix Pack 7 for Linux AMD64 & Intel EM64T (X64) Multilingual (CND6QML )

* DB2命令：
1. 查看实例：
db2ilist
2. 查看当前实例：
db2 get instance
3. 切换db2实例用户：
su - db2inst1
4. 启动关闭db2：
db2start
db2stop 
5. 强制重启：
	1. db2 force application all
	db2stop
	2. db2stop force

## redis
server启动：
sudo /usr/local/bin/redis-server /home/Luis/config/redis/redis.conf
客户端启动：
/usr/local/bin/redis-cli
关闭redis：
sudo /usr/local/bin/redis-cli shutdown

