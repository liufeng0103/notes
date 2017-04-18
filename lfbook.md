# lfbook
把平时常用的和一些学习笔记记录下来，方便以后查看

## Linux
### 常用
- 仓库配置目录 /etc/yum.repos.d
- 修改目录的用户和用户组 sudo chown user:group -R directory
- 启动栏app /usr/share/applications
### 软件安装
- 查看rpm包安装路径 rpm -qpl xxx.rpm
- 查看yum安装的软件路径 1. 查看软件完整的名称 rpm -qa|grep tomcat 2. 查看路径 rpm -ql xxx

## DB2
### 常用
- 查看实例 db2ilist
- 查看当前实例 db2 get instance
- 启动关闭 db2 db2start db2stop
- 强制关闭  
方式1： 1. db2 force application all 2. db2stop  
方式2： db2stop force  
- DB2 中的LONG VARCHAR类型 http://blog.csdn.net/yukiooy/article/details/4742904

## WebSphere Application Server(WAS)
### 常用(rhel7)
- 安装目录 /opt/ibm/WebSphere/AppServer
- 启动was sudo /opt/ibm/WebSphere/AppServer/profiles/AppSrv01/bin/startServer.sh server1 -profileName AppSrv01
- 关闭was sudo /opt/ibm/WebSphere/AppServer/profiles/AppSrv01/bin/stopServer.sh server1 -profileName AppSrv01 -username xxx -password xxx
- was控制台 https://localhost:9043/ibm/console/login.do
- 查看所有profiles sudo /opt/ibm/WebSphere/AppServer/bin/manageprofiles.sh -listProfiles
- 删除profile sudo /opt/ibm/WebSphere/AppServer/bin/manageprofiles.sh -delete -profileName AppSrv01

